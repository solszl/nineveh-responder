# NResponder #

<b>NResponder</b> is the most advanced and fast way to work with events in ActionScript 3.0 (AS3).
Responder grown based on idea of Objective-C Event Flow.
For this reason the name is Responder, like Responders in Objective-C.

Responder have features to work with events in an advanced way. This is very helpful to do complex applications, like games and rich interactive applications.


---


## Direct to the Point ##

Don't worry with memory manage or garbage collection to the listeners.

```
NResponder.add('anActionName', myListener);
```

To all native Flash Events:

```
// Instead this
myObject.addEventListener(Event.ADDED_TO_STAGE, initialize, false, 0, true);

// Use this
NResponder.addNative(myObject, Event.ADDED_TO_STAGE, initialize);
```

Check all features below, like replies, delay, multiple and combined removes, dispatches Run-Time changes and more. If you are interested in learn how to say "Bye, Bye" to addEventListener, removeEventListener and hasEventListener or even the entire EventDispatcher class, see the videos below or check the docs.


---


## How to use it: ##

Watch the videos tutorials and learn how to use NResponder in you applications.

### **Youtube 5 chapters: http://www.youtube.com/v/dGQHxya0qeA** ###


---


## Nineveh Responder Data Flow ##

<img src='http://db-in.com/imgs/nresponder_pipeline.png' width='800' height='600' />


---


## Reasons why: ##

**NResponder** is a Singleton class capable to control all events in an application, either in different SWFs! You can dispatch listeners across applications and domains.

<br />
### Features Comparison ###
| **Feature** | **Event API** <br /> ﻿(Adobe® Flash®) | **Signals** <br /> (Robert Penner) | **NResponder** <br /> (Diney Bomfim) |
|:------------|:------------------------------------------|:-----------------------------------|:-------------------------------------|
| **Used without instance** | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Used with instance** | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Specify number of dispatch arguments** | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Dynamic dispatch arguments** | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Change dispatch arguments in Run-Time** | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Remove all** | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | limited to instance | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Set the number of replies** | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | Just 1 | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Specify a delay time** | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Ordenate** | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Can associate with a target** | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> | only NativeSignal | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Can pause without remove** | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Can stop propagation** | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Change attributes in Run-Time** | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |
| **Garbage Collect** | only weak references | <img src='http://db-in.com/imgs/no.gif' alt='NO' title='NO' /> | <img src='http://db-in.com/imgs/yes.gif' alt='YES' title='YES' /> |

<br />
### Tests Comparison ###
| **Test Area** | **Event API** <br /> ﻿(Adobe® Flash®) | **Signals** <br /> (Robert Penner) | **NResponder** <br /> (Diney Bomfim) |
|:--------------|:------------------------------------------|:-----------------------------------|:-------------------------------------|
| **Size Added to SWF** | 350 bytes | 2.4 KB + 3.3 KB | 3.6 KB |
| **Memory of Class** | 4.5 KB | 2.7 KB + 3.3 KB | 3.2 KB |
| **Memory of Each Instance** | 88 bytes | 28 bytes + 24 bytes | 52 bytes |
| **Performance to Add** (1) | 1.9 sec. | 2.2 sec. | 2.6 sec. | 3.6 sec. |
| **Performance to Dispatch** (2) | 2.4 sec. | 2.7 sec. | 4.8 sec. | 1.8 sec. |
| **Performance to Remove** (3) | 0 sec. | 0 sec. | 0 sec. | 0 sec. |

(1) Add methods in an exaustive mode 10 different listeners added for 1.000.000 times. A real world application never will do this exaustive work.

(2) Dispatch methods in an exaustive mode 10 different listeners dispatched for 1.000.000 times. A real world application never will do this exaustive work.

(3) Remove methods for 10 different listeners 1.000.000 times. This method never will be exaustive in any of 3 APIs because in the first loop all the added listeners of the test was be removed. And these APIs works fine with cleaning the removed instances.



---


## Notices ##


_05/23/2010:_
<br />**Launch of NResponder with version 1.0**



---


### About author ###
| **Author:** |Diney Bomfim|
|:------------|:-----------|
| **Version:** |1.0|
| **Contact:** |diney@db-in.com|
| **Copyright:** |DB-Interactive|

Our Golden Rule is:
## Keep it simple ##

All Nineveh Framework classes are produced by DB-Interactive. For more information visit [db-in.com](http://www.db-in.com)