# Who should read this #

  * To follow at this point, you need be familiar with the "add" methods of NResponder. You can find all information about this here AddMethods.

# Introduction #

Base on the following table, let's see 3 exclusive features of NResponder: **Number of replies**, **delay time** and **ordinate**.

| Used without instance |
|:----------------------|
| Used with instance |
| Specify number of dispatch arguments |
| Dynamic dispatch arguments |
| Change dispatch arguments in Run-Time |
| Remove all |
| _**Set the number of replies**_ |
| _**Specify a delay time**_ |
| _**Ordenate**_ |
| Can associate with a target |
| Can pause without remove |
| Can stop propagation |
| Change attributes in Run-Time |
| Garbage Collect |


---


# Number of replies #

This is one of the most useful features of NResponder. With number of replies you can specify how many times the NResponder will perform, after the last time, the NResponder will automatically remove itself and will clean all memories allocated to it.

For example, is a very common technique use a ADDED\_TO\_STAGE event in the constructor of the view classes (display objects) to prevent access to the stage property before the right time. But you need to remove that listener after the object is in the display list.
With **number of replies** you can specify 1(one) in the `addNative()` method and don't worry more about anything.

Or, for example, in a game that user need to push a button 5 times, all that you need is specify the number of replies of the MOUSE\_DOWN to 5 and NResponder will do everything else.

In all create methods ("add" methods and the constructor) the following parameter of "listener" is the "replies". You just need to inform a number (uint). Remember that 0 (zero) is the default and represent "infinity" replies.

To the example of ADDED\_TO\_STAGE, use something like this:
```
NResponder.addNative(this, Event.ADDED_TO_STAGE, init, 1);
```

To example of MOUSE\_DOWN, use something like this:
```
NResponder.addNative(pushButton, MouseEvent.MOUSE_DOWN, clickHandler, 5);
```

Remember that like some other features, "replies" can be changed in the run-time. So if you need to change this number, use the instantiated mode:
```
var nrButton:NResponder = NResponder.addNative(pushButton, MouseEvent.MOUSE_DOWN, clickHandler, 5);

...

nrButton.replies = 10;
```


---


# Delay time #

The delay time indicate the time, in seconds, that NResponder needs to wait between two consecutive dispatches. For example, you can use the delay time to "transform" an ENTER\_FRAME loop in a periodic loop of 2 seconds. Or you can have a button (MOUSE\_UP) that can only be pressed each 1.5 second.

To do these two example all that you will need is set just one parameter in NResponder. The following parameter of "replies" is the "delay". Delay expect a number (Number). Remember that 0 (zero) is the default and represent "no delay" between consecutives dispatches.

To the example of ENTER\_FRAME, use something like this:
```
NResponder.addNative(this, Event.ENTER_FRAME, loopHandler, 0, 2);
```

To example of MOUSE\_UP, use something like this:
```
NResponder.addNative(pushButton, MouseEvent.MOUSE_UP, clickHandler, 0, 1.5);
```

Remember that like some other features, "delay" can be changed in the run-time. So if you need to change this number or prefer set the "delay" after some other event (following example), use the instantiated mode:
```
var nrButton:NResponder = NResponder.addNative(pushButton, MouseEvent.MOUSE_UP, clickHandler);

...

nrButton.delay = 0.5;
```


---


# Ordenate #

Like native Event API of Flash, NResponder can has a complex order if you want. In native Event API you use the "priority" property to change the order. To "priority" higher numbers are dispatched first. This don't make some sense to me, because you need to set 10 to dispatch an event first than other with 3.

NResponder work with order in the inverse way! Think in it like an Array. First indexes are dispatched first. Just it. 0(zero) are the first, after came the 1... after 10, and so on.

To set the order of a NResponder you can set the property "order" or use the parameter in the "add" methods. The following parameter of "delay" is the "order". Order expect a number (uint). Remember that 0 (zero) is the default and represent the first order.

To set the order in parameter, use something like this:
```
NResponder.add('bannerChange', bannerHandler, 0, 0, 1); // This will be dispatched last.
NResponder.add('bannerChange', bannerSelect, 0, 0, 0); // This listener will be dispatched first.
```


Remember that like some other features, "order" can be changed in the run-time. So if you need to change this number or prefer set the "order" after some other event (following example), use the instantiated mode:
```
var nrButton:NResponder = NResponder.add('bannerChange', bannerHandler);
NResponder.add('bannerChange', bannerSelect); // This don't need to be instanciated because I will not change anything in this NResponder in the future.
...

nrButton.order = 1; // Now, this NResponder will be dispatched after the first.
```

If two or more NResponders have the same order, they will be dispatched in the order that it was added.


---


If you have some doubts about this content, leave you comment, check the full documentation here [ASDoc](http://db-in.com/frameworks/nineveh/doc/) or [email me](mailto:diney@db-in.com).

Will be a pleasure to help.