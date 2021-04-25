---
course_id: 2-s998-marine-autonomy-sensing-and-communications-spring-2012
layout: course_section
parent_title: Labs
title: Lab 7 Updates
type: course
uid: 0e1c4f169177fa2407c942dd4fa282be

---

In launching more than one vehicle in simulation, it starts to become more convenient to use a shell script to launch things. Here's a very simple script, followed by a more fancy one for launching a mission consisting of a shoreside community (shoreside.moos) and a single vehicle (alpha.moos).

A Simple Launch Script
----------------------

### The script:

The script first checks for a numerical value in the command line arguments. If it finds one, it interprets this a request for a time warp. Then it does nothing more than launch pAntler for the two vehicles, and send a bit of output to the screen. The first line in the script is standard for shell scripts and indicates which shell is to be used for executing the script. To run the script, just type **./launch.sh 12** on the command line, to launch things with a time warp of 12.

```
  #!/bin/bash     WARP=1   #-------------------------------------------------------   #  Part 1: handle command-line args   #-------------------------------------------------------   for ARGI; do       if [ "${ARGI//[^0-9]/}" = "$ARGI" ]; then            WARP=$ARGI       fi   done    #-------------------------------------------------------   #  Part 2: Launch the processes   #-------------------------------------------------------    printf   "Launching ... (WARP=%s) \n" $WARP   pAntler alpha.moos --MOOSTimeWarp=$WARP >& /dev/null &   sleep 1   pAntler shoreside.moos --MOOSTimeWarp=$WARP >& /dev/null &   printf "Done Launching... \n" 
```

Misc. Other Updates
-------------------

*   Geometry library linking: If you choose to use any of the objects in the lib\_geometry library from the moos-ivp tree, e.g., the XYSegList class for waypoints, you will need to add the **geometry** and **mbutil** libraries to the list of libraries linked in your CMakeLists.txt file.
    
*   Launch script bug: Around line 92 of the launch.sh launch script in the baseline mission, the gilda.bhv file is mistakenly configured with START\_POS=$START\_POS1, and this should be START\_POS2 instead.
    
*   Path planning start: The pGenPath MOOS module accepts a sequence of VISIT\_POINT postings. There is the question of when the app should stop waiting for more postings and just begin its path calculation. Implement your app such that it interprets VISIT\_POINT="last", as its cue to disregard future incoming mail and begin its calculation of shortest path.
    

Partial Solutions
-----------------

[Example solutions to lab exercises (TGZ)](/coursemedia/2-s998-marine-autonomy-sensing-and-communications-spring-2012/134b04d34970bbd3bc39e0783368fec6_lab07-mid-sln.tgz) (the ones given as precursors to the hand-in assignments).

To untar:

```
tar xvfz filename.tgz
```

[Example solutions to exercise in Section 3.1 in Lab 07 (TGZ)](/coursemedia/2-s998-marine-autonomy-sensing-and-communications-spring-2012/9e70e0c76eb51378431d30b35418c6ab_lab07miss_files.tgz).

To untar:

```
tar xvfz filename.tgz
```