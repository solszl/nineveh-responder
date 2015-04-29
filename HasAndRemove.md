# Who should read this #

  * To follow at this point, you need be familiar with the "add" methods of NResponder. You can find all information about this here AddMethods.
  * You need be familiar with the dispatch method too. You can find all information about this here DispatchBasic.

# Introduction #

Using the `has()` method you can check if a NResponder or a combination with some NResponders exist. The `remove()` can exclude a NResponder or a combination with some NResponders.
These methods are very similar with `hasEventListener()` and `removeEventListener()`, but with some big advantages.


---


# has() #

This method expect 3 (three) parameter and by default all these three is null. Because you can make any combination to active a specific behavior. The parameters are:
  * Action - A string that represent the action you want to search.
  * Listener - The function itself that you want to search.
  * Target - The target itself that you want to search.

Let's start with a simple example and increase the complexity gradually:
```
NResponder.add('myAction', myListener, 1, 0, 0, myObject);
NResponder.add('anotherAction', anotherListener);

...

trace(NResponder.has('myAction'));                                 // true
trace(NResponder.has('anotherAction'));                            // true
trace(NResponder.has('myAction', myListener));                     // true
trace(NResponder.has(null, myListener));                           // true
trace(NResponder.has(null, anotherListener));                      // true
trace(NResponder.has(null, null, myObject));                       // true
trace(NResponder.has('myAction', anotherListener));                // false
trace(NResponder.has('anotherAction', myListener));                // false
trace(NResponder.has('anotherAction', anotherListener, myObject)); // false
trace(NResponder.has('myAction', null, myObject));                 // true
trace(NResponder.has('anotherAction', null, myObject));            // false
```

As you can see you can make any combination. You don't need every time have all parameters, you need at least one to check if has a NResponder with it. Analyzing the lines above, we can see:
  * NResponder.has('myAction') will check if exist at least one NResponder with the Action "myAction".
  * NResponder.has('myAction', myListener) will be more specific, and will check if has a NResponder with "myAction" as Action and "myListener" as Listener.
  * NResponder.has('anotherAction', anotherListener, myObject) will be a very specific and will search for a NResponder with exactly "myAction", "anotherListener" and "myObject", in this example, don't exist so return `false`.
  * NResponder.has(null, anotherListener) will ignore the Action and will search at least one NResponder with "anotherListener" as Listener.
  * NResponder.has(null, null, myObject) will ignore the Action and the Listener and will search at least one NResponder with "myObject" as Target.
  * NResponder.has('anotherAction', null, myObject) will search for a NResponder with "myObject" as Target with a specific Action, the "anotherAction" independent of the Listener that it has.

The most important here is remember that `null` parameter represent that you want to ignore that parameter and focus on others.

For security reasons, the `has()` with null in all three parameter will always return `false`, because you can't check or manipulate all the NResponder at same time.



---


# remove() #

The `remove()` method has a very similar behavior to `has()`, the difference is that here instead only check if a NResponder exist or not, you will exclude it. When you do it the NResponder immediately will stop to respond and go to the Garbage Colletion of Flash Player.

Obviously, if you try to remove a NResponder during a dispatch execution (inside the callBack Listener) the code will finish all the job in callBack first and after will remove the NResponder.

The following example illustrate this situation:
```
NResponder.add('myAction', myListener_1, 0, 0, 2);
NResponder.add('myAction', myListener_2), 0, 0, 1);
NResponder.add('anotherAction', anotherListener);

...

// Any of the three following alternatives will remove the same NResponder
NResponder.remove('anotherAction');
NResponder.remove('anotherAction', anotherListener);
NResponder.remove(null, anotherListener);

// Nothing will happens.
NResponder.dispatch('anotherAction');

// In reason the order, the listener "myListener_2" will be dispatched first.
NResponder.dispatch('myAction');

// This second attempt to dispatch "myAction" will result in nothing, because during the first dispatch this Action was removed.
NResponder.dispatch('myAction');

...

function myListener_1():void
{
    // This function will appear because the remove will occurs just after finish the execution of the current dispatch.
    trace('This is the "myListener_1" and was dispatched last because has the last order.');
}

function myListener_2():void
{
    trace('This is the "myListener_2" and was dispatched first.');
    
    // Now let's remove the current action in dispatch process, using the currentAction static property.
    NResponder.remove(NResponder.currentAction); 
}
```

As you can see, one of the most advantages here is you don't need to know about the listeners to remove a NResponder, and can remove multiple NResponders at same time.

Just like `has()` you can combine the parameter to get a more specific or more globally result:
```
NResponder.addNative(myObject, Event.ADDED_TO_STAGE, onStage);
NResponder.addNative(myObject, MouseEvent.CLICK, clickHandler);
NResponder.addNative(myObject, MouseEvent.MOUSE_OVER, overOutHandler);
NResponder.addNative(myObject, MouseEvent.MOUSE_OUT, overOutHandler);
NResponder.addNative(myObject, 'aCustomAction', customListener);

...

// Just this line bellow will remove all the NResponder of the "myObject" Target.
NResponder.remove(null, null, myObject);
```

This is very useful mainly when you don't have a reference to the Listener, like in some cross SWF applications.


---


If you have some doubts about this content, leave you comment, check the full documentation here [ASDoc](http://db-in.com/frameworks/nineveh/doc/) or [email me](mailto:diney@db-in.com).

Will be a pleasure to help.