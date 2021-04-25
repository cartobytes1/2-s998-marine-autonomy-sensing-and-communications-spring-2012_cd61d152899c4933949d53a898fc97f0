---
course_id: 2-s998-marine-autonomy-sensing-and-communications-spring-2012
layout: course_section
parent_title: Labs
title: Lab 4 Updates
type: course
uid: 3c8cb2f78c9ef1cbb7398f038f22de49

---

This page describes the use of a few methods written in C++ for parsing strings. They are defined in lib\_mbutils/MBUtils.h. You can either link to this library or go to the library and copy the code snippets into your own program.

The three functions defined on this page are (from MBUtils.h):

```
vector<string> parseString(string, char); string         biteString(string&, char); string         stripBlankEnds(string);
```

Block color coding on this page:

```
source code snippet output
```

### Common lines

Each of the code snippets below also have the following four lines at the top.

```
#include "MBUtils.h" #include <string> #include <iostream> using namespace std;
```

### Parsing a comma-separated list

```
#include <vector>  string str = "apples,pears,bananas"; cout << "Initial string is: " << str << endl;  vectors<string> svector = parseString(str, ','); unsigned int i, vsize = svector.size(); for(i=0; i<vsize; i++) {    cout << "Entry[" << i << "]: " svector[i] << endl;  }
```

```
Initial string is: apples,pears,bananas Entry[0]: apples Entry[1]: pears Entry[2]: bananas
```

### Parsing a parameter=value pair

```
string str = "temperature=98.6"; cout << "Initial string is: " << str << endl;  string param = biteString(str, '='); cout << "Param: " << param << endl; cout << "Value: " << str   << endl;
```

```
Param: temperature Value: 98.6
```

### Stripping blank ends from a string

```
string str = "   Hello World!  "; cout << "Initial string is: [" << str << "]" << endl;  string new_str = stripBlankEnds(str); cout << "New string is: [" << new_str << "]" << endl;
```

```
Initial string is: [   Hello World!  ] New string is: [Hello World!]
```

Random Number Script
--------------------

Below is a uTimerScript script for generating a random 15 digit number every quarter second, followed a random 9,7 and 5-digit number, and posted to the MOOSDB by the variable name **RAND\_NUMBER.**

```
// Note: 2**48 = 281,474,976,710,656  ProcessConfig = uTimerScript {   AppTick   = 4   CommsTick = 4    paused     = false   event      = var=RAND_NUMBER, val=$(15), time=0.25   event      = var=RAND_NUMBER, val=$(9), time=0.50   event      = var=RAND_NUMBER, val=$(7), time=0.75   event      = var=RAND_NUMBER, val=$(5), time=1.00   reset_max  = nolimit   reset_time = all-posted }
```

Converting long strings to numbers:

```
#include <cstdlib> unsigned long int val = strtoul(str.c_str(),NULL,0);
```

Since 2\*\*64 is 18,446,744,073,709,551,616, the above should work on all strings up to 19 digits.

**Note:** The use of **$(15)** in the uTimerScript event represents a new feature of uTimerScript. You will need to do an _svn update_ in the moos-ivp tree and recompile. The forms $(1) through $(20) are supported.

```
$ cd moos-ivp $ svn update       // You should be at revision 4182 or higher $ ./build-ivp.sh
```

MOOS App Output Format
----------------------

Regarding the output strings from your two MOOS apps in lab 4: the specs left some room for design in the output format, leaving it up to you to handle whatever format you chose in your first app in your tester app. The TAs would like to write a tester MOOS app suitable for testing the output for all student apps. Therefore we need to be a bit more specific:

For the pSequence app, the following format should be used:

```
SEQUENCE_RESULT = "values=3:63:5:21:119,output=odd"
```

For the pPrimeFactor app, the following format should be used:

```
PRIME_RESULT = "orig=30030,received=34,calculated=33,solve_time=2.03,                   primes=2:3:5:7:11:13,username=jane"
```

Submit Format
-------------

Lab 04 assignments should be uploaded to the course site. You should upload ONE file, using either tar, zip or equivalent. Assuming you started with a moos-ivp-extend folder, rename your folder to moos-ivp-xyz, where xyz is your mit mail prefix.

The folder format should have the naming and file organization as indicated below:

```
moos-ivp-yourname/    src/pPrimeFactor       /pPrimeFactorTester       /pSequence       /pSequenceTester     missions/sequence/sequence.moos            /primes/primes.moos
```