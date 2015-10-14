---
layout: page
title: Setup base jobs in bacula
date: '2015-10-14 23:20'
categories:
  - howto
tags:
  - apache
teaser: De-duplicating common files across your bacula backups
---

## What's Bacula?

[Bacula](http://www.bacula.org) is an open-source set of tools (client and server) for network file-level backup and restore.

Features I like are:

* Optional encrypted transmission and storage (at rest) of data.
* Flexibility re backup scheduling, levels, target files, etc.
* Backs into a MySQL / PostgreSQL database, which makes custom reporting and monitoring possible.

Recently I've been working on updating our design from version 5.0.0 to update to version [7.0.5](http://blog.bacula.org/release-7-0-5/), and one of the features I wanted to leverage was the ability do "de-duplicate" backups using [base jobs](http://www.bacula.org/7.0.x-manuals/en/main/File_Deduplication_using_Ba.html).

## De-duplication with Base Jobs

By using base jobs, it's possible to avoid backing up identical files on multiple hosts - in our case, we have tens of hosts running CentOS 6, all with ~800MB of operating system files, which are identical across hosts. By using a base job, I can backup all the OS files once (the base job), and all other backups will simply refer to the base job rather than backing up the files again.

Bacula's documentation is a little sparse on this, so I'm including a working example below.

## Working example

A base job:

    # This exists to define a base for CentOS 6 hosts
    Job {
      Name = "base-centos6"
      JobDefs = "jd-base"
      Schedule = base
      Level = Base
      Client = <base-machine-hostname>-fd
    }

A normal job which depends on the base job:

    Job {
      Name = "<bacula-client-hostname>-daily"
      JobDefs = "jd-daily"
      Client = <bacula-client-hostname>-fd
      Base = <base os backup>
      Write Bootstrap = "/var/spool/bacula/<bacula-client-hostname>.bsr"
    }


And the job definition. Note that this **must** be an "Accurate" job. If you leave out the "Accurate" directive, a base job will not be used.

    JobDefs {
      Name = "jd-daily"
      Type = Backup
      Level = Incremental
      Client = <bacula-server-hostname>-fd
      FileSet = "fs-linux"
      Schedule = "daily"
      Storage = vchanger
      Messages = Daemon
      Pool = daily
      Priority = 10
      Max Run Time = 360 minutes
      # Required for dedupe using base jobs
      Accurate = yes
      # Required to avoid putting jobs in DB before completion (avoids cancelled jobs in the DB)
      Spool Attributes = yes
    }

## Sample output

You know your base job is working, if your job output includes the following on starting:

    14-Oct 23:08 bacula-dir JobId 21: Using Device "vchanger-0" to write.
    14-Oct 23:08 bacula-dir JobId 21: Using BaseJobId(s): 1
    14-Oct 23:08 bacula-dir JobId 21: Sending Accurate information to the FD.

And the following on completion:

    14-Oct 23:10 bacula-fd JobId 21: Space saved with Base jobs: 1665 MB
