---
layout: post
category: postmortem
date: 2016-08-19 12:40:50
title: "Spacecraft and IT systems fail for the same reasons"
teaser: "Surprisingly common factors affect the failure of both"
tags: failure, bias
---

In [SOHO MISSION INTERRUPTION FAILURE INVESTIGATION](http://umbra.nascom.nasa.gov/soho/SOHO_final_report.html), I read the fascinating postmortem of the near-loss of the SOHO observatory due to what can only be described as basic operational process fails. (The craft was later [spectacularly recovered](http://soho.nascom.nasa.gov/about/Recovery/))

The story of the fail, commented, below:

![SOHO observatory](https://www.funkypenguin.co.nz/images/soho-observatory.jpg)

## What went wrong
In summary, human error compounded on human error, and resulting poor judgement resulted in the wrong corrective action being taken, which ultimately resulted in loss of all telemetry to the spacecraft.

> Problems encountered in other programs using similar gyros led to introduction of additional changes following launch to further preserve gyro lifetime.

​The standards were changed during the life of the program.

> The difference with the events leading to this incident was that the operation had been compressed into a continuous sequence. This required a new script and first time utilization of paths within previously modified procedures.

​Amount of change to a routine well-known process was a contributing factor, as was the "compressed" timeline (do more in less time, which pressures staff to take shortcuts)

> Due to an omission in the modified predefined command sequence actually used, the onboard software function that activates the gyro needed by ESR was not enabled. This omission resulted in the removal of the functionality of the normal safe mode and ultimately caused the catastrophic sequence of events.

​Omissions are harder to detect than errors, and even careful peer-reviews can miss them. Automated monitoring (in addition to human expertise) is required to prevent minor oversights becoming massive disasters.

> Following the momentum management maneuver, Gyro B, which is used for fault detection, was erroneously left in its high gain setting, resulting in an indicated roll rate of 20 times greater than actual. The incorrect gain was due to an error in another predefined command sequence; this error resulted in an on-board fault detection output that triggered an ESR.

​When you change routine processes, or use established processes in new ways, previously unknown issues can surface, and given the right circumstances, combine to create failure. Mitigation is ensuring review and standards are applied to even routine processes, every time.

> The personnel on the ground were not aware of either of these facts at that time.

​Monitoring that's not detailed enough (or too noisy!) can drown out the critical information, reducing the value of the monitoring.

> A rapid decision was made that Gyro B was faulty because its output disagreed with the rate indicated by Gyro A. This decision led to the commanding off of Gyro B.

My takeaway here is that the decision was ___rapid___ - a knee-jerk response without careful examination and evaluation. As we'll note later, the information on the state of Gyro A was available, but was "too hard to interpret" or was not evaluated carefully, due to assumption bias (the cause of the discrepancy was believed to be known, so alternative possibilities were not tested). 

A correlation to IT from [Prophecy](http://www.prophecy.net.nz)'s experience is that when a virtual machine exhibits symptoms associated with under-resourcing (sluggish response, high CPU load), simply adding more resource can either create [further problems](http://www.gabesvirtualworld.com/how-too-many-vcpus-can-negatively-affect-your-performance/), or simply mask an underlying root cause (like an actual software fault).

> The incorrect diagnosis of a Gyro B fault and the subsequent ground response to this diagnosis ultimately resulted in loss of attitude control, subsequent loss of telemetry, and loss of power and thermal control

​There you go. The faulty diagnosis is the root of all further failures (although there were other contributing factors)

> At any time during the over five hour emergency situation, the verification of the spinning status of Gyro A would have precluded the mishap.

​Monitoring is invaluable. But you have to ___look___ at it, ___interpret___ it, and ___trust___ it.
​
## Contributing factors

> Though some of these modifications were made at the request of the SOHO Science Team, they were not necessarily driven by any specific requirement changes. The procedure modifications appear to have not been adequately controlled by ATSC configuration board, properly documented, nor reviewed and approved by ESA and/or NASA. The verification process was accomplished using a NASA computer-based simulator. There was no code walk-through as well as no independent review either by ESA, MMS, or an entity directly involved in the change implementation. No hard copy of the command procedure set exists, and the latest versions are stored electronically without adequate notification of procedure modifications.

This is huge. The takeaway:

1. Changes were made without clear requirements / justification.
2. Insufficient care was taken to ensure that the changes would not have a negative impact.
3. When procedures were updated, they were simply refreshed electronically, and there was no formal notification that the processes had changed.

> multiple ground operations procedures were modified. Each change was considered separately, and there appears to have been little evaluation performed to determine whether any of the modifications had system reliability or contingency mode implications; or whether the use of this modified procedure set should have been accompanied with operational constraints.

### Lack of change control￼
### Pressure causes poor decision-making￼
### Early failure indications were ignored￼
## Established processes were not followed￼
## Actions to avoid future failure￼