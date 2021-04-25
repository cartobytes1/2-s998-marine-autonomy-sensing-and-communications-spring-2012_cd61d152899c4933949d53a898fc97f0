---
course_id: 2-s998-marine-autonomy-sensing-and-communications-spring-2012
layout: course_section
menu:
  leftnav:
    identifier: 72c27940a2e02452abf2720d0762289d
    name: Launching the MOOSDB
    parent: dab1dc4f1da21ac2f60143a182449e27
    weight: 140
parent_title: MOOS Basics
title: Launching the MOOSDB
type: course
uid: 72c27940a2e02452abf2720d0762289d

---

This page describes how to launch the MOOSDB from the perspective of the first-time user. We'll describe two minimalist methods, starting with the most bare-bones.

A Bare-Bones Launching of the MOOSDB
------------------------------------

In a bare-bones manner, the MOOSDB may be launched from the command line without any arguments. Normally the MOOSDB needs to know at least two pieces of configuration information, (a) the machine (IP address) on which to run, and (b) the port number on which to serve clients. It will default to running on the localhost and port 9000. But it will complain a bit:

```
 $ MOOSDB
  Warning no mission file found - still serving but with trepidation
  ***************************************************
  *       This is MOOS Server for Community "#1"      
  *       c. P Newman 2001                           
  *                                                  
  *       Binding on 9000                              
  *                                                  
  *       This machine is Little endian                 
  ***************************************************
					
  ------------CONNECT-------------
  New client connected from machine "localhost"
  Handshaking....done
  clients name is "DBWebServer"
  There are now 1 clients connected.
  --------------------------------

  *****************************************************
    serving webpages HTTP on http://fred.csail.mit.edu:9080
  *****************************************************
```

At this point the MOOSDB is running on the local machine, serving clients on port 9000. There is also "DBWebServer" on port 9080. You can click on (your version of) the above URL in your browser and see a current state of the MOOSDB.

A More Civilized Launching of the MOOSDB
----------------------------------------

Virtually all MOOS applications are launched with a "mission configuration" file, a.k.a. a "dot-moos" file. The below mission file **moosdb\_alpha.moos** provides the minimal configuration parameters the MOOSDB likes to see upon starting.

```

// (wget http://oceanai.mit.edu/2.S998/examples/moosdb_alpha.moos)
ServerHost = localhost
ServerPort = 9000
Community  = alpha
```

Passing the **moosdb\_alpha.moos** file as a command line argument produces a somewhat happier output (no warnings of trepidation).

```
$ MOOSDB moosdb_alpha.moos
  ***************************************************
  *       This is MOOS Server for Community "alpha"      
  *       c. P Newman 2001                           
  *                                                  
  *       Binding on 9000                              
  *                                                  
  *       This machine is Little endian                 
  ***************************************************

  ------------CONNECT-------------
  New client connected from machine "localhost"
  Handshaking....done
  clients name is "DBWebServer"
  There are now 1 clients connected.
  --------------------------------

  *****************************************************
    serving webpages HTTP on http://fred.csail.mit.edu:9080
  *****************************************************
```