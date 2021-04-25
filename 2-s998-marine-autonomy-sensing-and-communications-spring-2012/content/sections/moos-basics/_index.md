---
course_id: 2-s998-marine-autonomy-sensing-and-communications-spring-2012
layout: course_section
menu:
  leftnav:
    identifier: dab1dc4f1da21ac2f60143a182449e27
    name: MOOS Basics
    weight: 130
title: MOOS Basics
type: course
uid: dab1dc4f1da21ac2f60143a182449e27

---

Getting Started with MOOS Basics
--------------------------------

These pages contain a handful of introductory MOOS topics designed for the absolutely new MOOS user.

*   [Launching the MOOSDB]({{< baseurl >}}/sections/moos-basics/launching-the-moosdb):
    
    The MOOSDB is the heart of MOOS. This page describes how it may be simply launched from the command line. Later we'll see that typically the MOOSDB is launched as part of a group MOOS apps with the pAntler tool. But this a good page to start for someone who has never before launched the MOOSDB.
    
*   [Scoping the MOOSDB]({{< baseurl >}}/sections/moos-basics/scoping-the-moosdb):
    
    This page describes how to scope the MOOSDB. Scoping refers to the idea of having a view into the current state (or even recent history) of the MOOSDB. This page describes the uXMS and uMS tools, among the several ways to scope the MOOSDB.
    
*   [Poking the MOOSDB]({{< baseurl >}}/sections/moos-basics/poking-the-moosdb):
    
    This page describes how to poke the MOOSDB. Poking refers to the idea of publishing a variable-value pair to the MOOSDB. Poking implies a publication that perhaps was not planned, or outside the normal mode of business. It is often very useful for debugging. Here we describe the uPokeDB tool.
    
*   [Launching a Mission with pAntler]({{< baseurl >}}/sections/moos-basics/launching-a-mission-with-pantler):
    
    This page describes how to launch a set of MOOS applications with pAntler. In theory, a set of N applications may be launched from N terminal windows, but this is cumbersome in practice. The pAntler tool allows a block to be declared in a mission file (.moos file) listing all the apps to be launched in one go.
    
*   [Scripted Pokes to the MOOSDB]({{< baseurl >}}/sections/moos-basics/scripted-pokes-to-the-moosdb):
    
    This page describes MOOS scripting: configuring a set of pre-arranged pokes, at pre-arranged times to the MOOSDB. This may be useful for a number of reasons besides debugging. The primary tool described here is the uTimerScript MOOS application.
    
*   [A Simple Example with pXRelay]({{< baseurl >}}/sections/moos-basics/a-simple-example-with-pxrelay):
    
    pXRelay is a simple MOOS app designed solely to illustrate basic functions of a MOOS app. It registers for a single variable, and upon receipt mail for that variable, it publishes another variable incremented by 1. It provides a framework for illustrating few other introductory topics.