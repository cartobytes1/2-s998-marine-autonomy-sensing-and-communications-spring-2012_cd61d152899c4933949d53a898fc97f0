---
course_id: 2-s998-marine-autonomy-sensing-and-communications-spring-2012
layout: course_section
parent_title: Labs
title: Lab 6 Updates
type: course
uid: 59c5b6bb44a9c4b9974da4b1f5553132

---

Depth Configurations
--------------------

In the Alpha example, the moos-ivp version of a Hello World program, the vehicle is a simulated surface craft. To simulated a UUV, a few modifications are required of three MOOS applications, including the helm. Once this is done, behaviors reasoning about depth may be used in the helm.

### Modifications to the uSimMarine MOOS module:

More information on the uSimMarine simulator and configuration options can be found in the ![This resource may not render correctly in a screen reader.](/images/inacessible.gif)[moos-ivp autonomy utilities documentation (PDF - 29.2MB)](http://oceanai.mit.edu/moos-ivp-pdf/moosivp-tools.pdf).

```
     BUOYANCY_RATE        = 0.025     MAX_DEPTH_RATE       = 5     MAX_DEPTH_RATE_SPEED = 2.0     DEFAULT_WATER_DEPTH  = 400 
```

### Modifications to the pMarinePID MOOS module:

More information on the uSimMarine simulator and configuration options can be found in the utilities ![This resource may not render correctly in a screen reader.](/images/inacessible.gif)[moos-ivp autonomy documentation (PDF - 29.2MB)](http://oceanai.mit.edu/moos-ivp-pdf/moosivp-tools.pdf).

```
     DEPTH_CONTROL = true        //Pitch PID controller     PITCH_PID_KP                   = 1.5     PITCH_PID_KD                   = 1.0     PITCH_PID_KI                   = 0     PITCH_PID_INTEGRAL_LIMIT       = 0        //ZPID controller     Z_TO_PITCH_PID_KP              = 0.12     Z_TO_PITCH_PID_KD              = 0     Z_TO_PITCH_PID_KI              = 0.004     Z_TO_PITCH_PID_INTEGRAL_LIMIT  = 0.05     MAXPITCH     = 15     MAXELEVATOR  = 13 
```

### Modifications to the pHelmIvP MOOS module:

More information on configuring the IvPHelm decision domain may be found on p. 47 in the ![This resource may not render correctly in a screen reader.](/images/inacessible.gif)[helm documentation (PDF - 29.2MB)](http://oceanai.mit.edu/moos-ivp-pdf/moosivp-tools.pdf).

```
Domain     = depth:0:100:101
```

### Modifications to the pNodeReporter MOOS module:

The modification below to pNodeReporter is mostly cosmetic. It changes the vehicle type to "UUV" so you see a UUV icon in your simulator diving, rather than a kayak. More information on pNodeReporter and configuration options can be found in the ![This resource may not render correctly in a screen reader.](/images/inacessible.gif)[moos-ivp autonomy utilities documentation (PDF - 29.2MB)](http://oceanai.mit.edu/moos-ivp-pdf/moosivp-tools.pdf).

```
VESSEL_TYPE   = UUV
```