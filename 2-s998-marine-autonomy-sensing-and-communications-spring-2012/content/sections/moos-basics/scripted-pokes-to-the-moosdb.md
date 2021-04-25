---
course_id: 2-s998-marine-autonomy-sensing-and-communications-spring-2012
layout: course_section
menu:
  leftnav:
    identifier: 8ffb37ccbdb1028acf644b911bacbd7d
    name: Scripted Pokes to the MOOSDB
    parent: dab1dc4f1da21ac2f60143a182449e27
    weight: 180
parent_title: MOOS Basics
title: Scripted Pokes to the MOOSDB
type: course
uid: 8ffb37ccbdb1028acf644b911bacbd7d

---

This page addresses the concept of having a script of pre-arranged pokes to the MOOSDB. This may be useful for a number of reasons besides debugging. The primary tool described here is the uTimerScript MOOS application. It is capable of (a) scripted pokes at a pre-defined times after launch, (b) pokes times specified to fall randomly within an specified interval, (c) pokes having numerical values falling with a uniformly random interval, and several other features including conditioning the running of the script based on other MOOS variables.

Basic uTimerScript Usage
------------------------

uTimerScript is configured with its own block in the MOOS configuration file. The general format is below. The primary entries are the events themselves, defined by a MOOS variable, value, and time or time-range when the event is to occur. There are many options for configuring the script. These options are described in the [IvP Helm Documentation and MOOS Documentation](http://oceanai.mit.edu/moos-ivp/docs.html), but a quick look at the options can be seen by typing "uTimerScript—example" on the command line.

```
 ProcessConfig = uTimerScript
 {
   event = var=, val=, time=
   event = var=, val=, time=
   ...
   event = var=, val=, time=

    [OPTIONS]
 } 
```

Further options exist beyond the vanilla launch configuration described above, including (a) the ability to launch a given app under an aliased name, (b) specifying command-line arguments to app at launch time and more. See the [MOOS documentation](http://www.robots.ox.ac.uk/~mobile/MOOS/wiki/pmwiki.php/Main/Documentation).

A Simple Example with uTimerScript
----------------------------------

The below mission file contains a uTimerScript script for repeatedly posting the variable 'COUNTER\_A' with values 1–10 in ascending order roughly once every half second. The last event in the script is posted at time chosen from a random five second interval.

```
 // (wget http://oceanai.mit.edu/2.S998/examples/utscript.moos)
 ServerHost = localhost
 ServerPort = 9000
 Community  = alpha

  ProcessConfig = ANTLER
 {
   MSBetweenLaunches = 200

   Run = MOOSDB       @ NewConsole = false
   Run = uXMS         @ NewConsole = true
   Run = uTimerScript @ NewConsole = false
 }

  ProcessConfig = uXMS
 {
   VAR            = COUNTER_A, DB_CLIENTS, DB_UPTIME
   COLOR_MAP      = COUNTER_A, red
   HISTORY_VAR    = COUNTER_A
 }

  ProcessConfig = uTimerScript
 {
   paused = false

   event  = var=COUNTER_A, val=1,  time=0.5
   event  = var=COUNTER_A, val=2,  time=1.0
   event  = var=COUNTER_A, val=3,  time=1.5
   event  = var=COUNTER_A, val=4,  time=2.0
   event  = var=COUNTER_A, val=5,  time=2.5
   event  = var=COUNTER_A, val=6,  time=3.0
   event  = var=COUNTER_A, val=7,  time=3.5
   event  = var=COUNTER_A, val=8,  time=4.0
   event  = var=COUNTER_A, val=9,  time=4.5
   event  = var=COUNTER_A, val=10, time=5:10

    reset_max  = nolimit
   reset_time = all-posted
 } 
```

The mission may be launched from the command-line with:

```
 $ pAntler utscript.moos 
```

This should open a new console window for uXMS displaying the variables COUNTER\_A variable repeatedly incrementing from 1 to 10. Note that reaching 10 happens somewhere between 0.5 and 5.5 seconds after reaching 9.