---
course_id: 2-s998-marine-autonomy-sensing-and-communications-spring-2012
layout: course_section
parent_title: Labs
title: Lab 9 Updates
type: course
uid: 5aedfcb8509b2d0709c23215d8218deb

---

Producing a Hazard Report
-------------------------

There is a change in the requested format of the reporting information to be produced by the vehicle. Rather than a sequence of reports such as described in the original lab:

```
HAZARD_REPORT = x=45,y=88,hazard=true,label=04 HAZARD_REPORT = x=15,y=18,hazard=false,label=16
```

You should instead produce a single report. There is a class called XYHazardSet that may be used as follows for easily constructing this report:

```
#include "XYHazardSet.h"   XYHazardSet my_hazard_set;   my_hazard_set.setSource("archie");  my_hazard_set.addHazard(45,88,"hazard","04");  my_hazard_set.addHazard(15,18,"benign","16");   string my_report = my_hazard_set.getSpec();   m_Comms.Notify("HAZARD_REPORT", my_report);
```

This will result in the post:

```
HAZARD_REPORT = "source=archie # x=45,y=88,type=hazard,label=04 #                  x=15,y=18,type=benign,label=16"
```

Note that you must include the _geometry_ library in your build. Just add _geometry_ to your list of link libraries in your CMakeLists.txt file, presumably in pHandleSensorData.

Knowing the Field Position of Other Vehicles
--------------------------------------------

If you'd like one vehicle to know the position of another vehicle, you may want to consider using the NODE\_REPORT information sent between vehicles. The NODE\_REPORT is typically sent from all vehicles to the shoreside. This is what allows the pMarineViewer app to know and render the vehicle information. The node reports are also used by uFldNodeComms to know the vehicle locations to reason about what messages are allowed to be sent between vehicles. uFldNodeComms also bridges NODE\_REPORT information back out to the vehicles to that vehicles may know each other's position. The NODE\_REPORT sharing is only done when "in range" of the other vehicle. The range is defined by the same ranged used for messaging. You can parse this string yourself, or use the NodeRecordUtils.h utilities found in the lib\_contacts library in the moos-ivp tree. A typical node report looks like:

```
NODE_REPORT = NAME=alpha,TYPE=UUV,TIME=1252348077.59,X=51.71,Y=-35.50,               LAT=43.824981,LON=-70.329755,SPD=2.0,HDG=118.8,                        YAW=118.8,DEPTH=4.6,LENGTH=3.8,MODE=MODE@ACTIVE:LOITERING
```

Receiving uFldHazardSensor Information on the Vehicle
-----------------------------------------------------

The uFldHazardSensor produces a sensor report, for a vehicle JAKE, in the form of UHZ\_HAZARD\_REPORT\_JAKE, posted to the local shoreside MOOSDB. This report is bridged out to the vehicle JAKE as the variable UHZ\_HAZARD\_REPORT. To enable this bridging, the uFldShoreBroker needs the following configuration line (omitted from the la09two\_baseline mission):

```
BRIDGE = src=UHZ_HAZARD_REPORT_$V, alias=UHZ_HAZARD_REPORT BRIDGE = src=UHZ_CONFIG_ACK_$V,    alias=UHZ_CONFIG_ACK
```

To send a NODE\_MESSAGE with a string value containing a comma, surround the string value with double-quotes. This reflects a fix in the moos-ivp tree, so please do an svn update and recompile on the tree before using this fix. For example:

```
NODE_MESSAGE_LOCAL=src_node=alpha,dest_node=bravo,var_name=MSG, \                    string_val="foo,bar"
```