---
course_id: 2-s998-marine-autonomy-sensing-and-communications-spring-2012
layout: course_section
parent_title: Labs
title: Lab 5 Updates
type: course
uid: 0454fc225af4a2952ae31e0b6d301cff

---

MOOS App Launch Alias
---------------------

In order for your MOOS app to be able to connect to the MOOSDB under an alias name (using the pAntler ~ syntax), your app must handle argv\[2\] as an alias specification. The two lines below were omitted from the main.cpp file in the GenMOOSApp script. Make sure you have them implemented in your program.

```
int main(int argc, char *argv[]) {   string mission_file = "";   string run_command  = argv[0];   bool   help_requested = false;   bool   vers_requested = false;   bool   exam_requested = false;    int    i;   for(i=1; i<argc; i++) {     string argi = argv[i];     if((argi=="−v") || (argi=="−−version") || (argi=="−version"))       vers_requested = true;     else if((argi=="−e") || (argi=="−−example") || (argi=="−example"))       exam_requested = true;     else if((argi == "−−help")||(argi=="−h"))       help_requested = true;     else if(strEnds(argi, ".moos") || strEnds(argi, ".moos++"))       mission_file = argv[i];     else if(strBegins(argi, "−−alias="))       run_command = argi.substr(8);     else if(i==2)                                      // Add these      run_command = argi;                               // two lines!  }    if(vers_requested) {     cout << "${2}${1} Version 0.1" << endl;     return(0);   }    if(exam_requested) {     showExampleConfig();     return(0);   }    ${1} ${1};   ${1}.Run(run_command.c_str(), mission_file.c_str());    return(0); } 
```