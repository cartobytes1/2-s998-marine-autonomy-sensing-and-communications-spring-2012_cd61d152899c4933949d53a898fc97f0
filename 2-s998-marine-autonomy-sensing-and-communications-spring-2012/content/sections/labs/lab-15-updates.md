---
course_id: 2-s998-marine-autonomy-sensing-and-communications-spring-2012
layout: course_section
parent_title: Labs
title: Lab 15 Updates
type: course
uid: aa913400ed17d39229c84ed62f8bc733

---

Setting Behavior Priority Weight
--------------------------------

A step is missing in the BHV\_SimpleWaypoint behavior that you were asked to use as a template.

The very last line of the onRunState() function in the SimpleWaypoint behavior returns the newly built IvP function:

```
return(ipf);
```

Prior to returning the IvP function you also need to apply the behavior weight as follows:

```
if(ipf)     ipf->setPWT(m_priority_wt);
```

You can regard this as boilerplate, but here's a couple notes in case you're curious:

1) the check "if(ipf)" is done in case the IvP function returned by the ZAIC tool returned null. If it were null, the second line would result in a crash.

2) the priority weight (m\_priority\_wt) is a member variable of the IvPBehavior superclass and is set automatically in the IvPBehavior::setParam() function handling parameters from your .bhv file.

3) the reason why the user applies the priority weight explicitly rather than being handled automatically, is that the behavior author may not want to just use the priority weight from the config file, but may want to instead use this as a guide in its own priority weight policy. For example the collision avoidance behavior will set its own weight between zero and m\_priority\_wt depending on the proximity to the contact.

One last point: to get your ZigLeg behavior to exert its influence over the vehicle trajectory, remember that it's running alongside the waypoint behavior. You will need to give your ZigLeg bahavior a priority weight higher than the waypoint behavior (set in the .bhv file).