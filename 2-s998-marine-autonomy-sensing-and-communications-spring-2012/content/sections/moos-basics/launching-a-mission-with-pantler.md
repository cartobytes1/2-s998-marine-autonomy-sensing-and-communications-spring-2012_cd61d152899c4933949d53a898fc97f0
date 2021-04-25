---
course_id: 2-s998-marine-autonomy-sensing-and-communications-spring-2012
layout: course_section
menu:
  leftnav:
    identifier: f084e04ee786d502fe78239c1e543b2c
    name: Launching a Mission with pAntler
    parent: dab1dc4f1da21ac2f60143a182449e27
    weight: 170
parent_title: MOOS Basics
title: Launching a Mission with pAntler
type: course
uid: f084e04ee786d502fe78239c1e543b2c

---

This page describes how to launch a set of MOOS applications with pAntler. In theory, a set of N applications may be launched from N terminal windows, but this is cumbersome in practice. The pAntler tool allows a block to be declared in a mission file (.moos file) listing all the apps to be launched in one go.

Where to get more information:

*   pAntler: [The MOOS Documents page](http://www.robots.ox.ac.uk/~mobile/MOOS/wiki/pmwiki.php/Main/Documentation)

Basic pAntler Usage
-------------------

The Antler block is typically the first configuration block in a .moos file, declared with **ProcessConfig = ANTLER** as below. The **MSBetweenLaunches** parameter specifies the number of milliseconds between launching processes. Each line thereafter specifies an app to be launched and whether a dedicated console window should be opened for the application.

```

ProcessConfig = ANTLER
{
  MSBetweenLaunches = 200

  Run = MOOSDB       @ NewConsole = true/false
  Run = AnotherApp   @ NewConsole = true/false
  ...
  Run = AnotherApp   @ NewConsole = true/false
}
```

Further options exist beyond the vanilla launch configuration described above, including (a) the ability to launch a given app under an aliased name, (b) specifying command-line arguments to app at launch time and more. See the [documentation](http://www.robots.ox.ac.uk/~mobile/MOOS/wiki/pmwiki.php/Main/Documentation).

An Example: Launching the MOOSDB along with uXMS
------------------------------------------------

In the example below we use pAntler to launch the MOOSDB and the uXMS Scope from a single mission file. The user preferences for uXMS are provided in its configuration block. Type "uXMS—example" on the command line for further options.

```

// (wget http://oceanai.mit.edu/2.S998/examples/db_and_uxms.moos)
ServerHost = localhost
ServerPort = 9000
Community  = alpha

ProcessConfig = ANTLER   
{   
  MSBetweenLaunches = 200

  Run = MOOSDB     @ NewConsole = false
  Run = uXMS       @ NewConsole = true
}

ProcessConfig = uXMS
{
  AppTick   = 4
  CommsTick = 4

  VAR            = DB_CLIENTS, DB_UPTIME, DB_TIME
  DISPLAY_SOURCE = true
  DISPLAY_TIME   = true
  COLOR_MAP      = DB_CLIENTS,red
}
```

The mission may be launched from the command-line with:

```
 $ pAntler db_and_uxms.moos 
```

This should open a new console window for uXMS displaying the variables posted by the DB, with the (S)ource and (T)ime columns expanded, but not the (C)ommunity column.