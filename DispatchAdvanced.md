# Who should read this #

  * To follow at this point, you need be familiar with the "add" methods of NResponder. You can find all information about this here AddMethods.
  * You need be familiar with the dispatch method too. You can find all information about this here DispatchBasic.

# Introduction #

Using the dispatch you can change the parameter to the listeners during run-time and do dispatches to an entire target.


---


# Change parameters #

A simple way to change the parameters during run-time is prepare you listener to expect a custom number of arguments, using the "rest".
```
NResponder.add('someAction', myListener);

...

var parameters:Array;

if(myConditional)
{
    parameters = ['justOneParameter'];
}
else
{
    parameters = ['anArgument', true, 0, 'anotherString'];
}

NResponder.dispatch('someAction', parameters);

...

function myListener(...params:Array)
{
    // Do something.
}
```


---


# Dispatch to targets #

The dispatch method has 3(three) parameters, the last one is the "toTarget". This means that you can dispatch an action, with more than one NResponder, just to a specific target. For example, you can have in your application 38 buttons at total, all they have MOUSE\_OVER, MOUSE\_OUT and MOUSE\_UP actions in NResponder. How NResponder will know to dispatch one or other? With the "toTarget" parameter.

On each dispatch, NResponder will check the target and if necessary, it will dispatch the action just to its target.

With this feature you can "force/simulate" a dispatch in a listener, for example, you can "force" the dispatch of a MOUSE\_OVER action. with a code like this:
```
NResponder.addNative(myObject1, MouseEvent.MOUSE_OVER, overOutHandler);
NResponder.addNative(myObject2, MouseEvent.MOUSE_OVER, overOutHandler);
NResponder.addNative(myObject3, MouseEvent.MOUSE_OVER, overOutHandler);

...

NResponder.dispatch(MouseEvent.MOUSE_OVER, [null], myObject1);
```

For this example, remember that when you use native Event API with NResponder, you listener need to expect a parameter (Event). Because this, this example set "[null](null.md)" (array with a null parameter).

Now, another useful feature of dispatch is that you can dispatch all NResponder of a specific target. To do this, pass `null` to the action, set the params to return if you need, and set the target. Like this:
```
NResponder.addNative(myObject, MouseEvent.MOUSE_UP, clickHandler);
NResponder.add('myCustomAction', customListener, 1, 0, 1, myObject);

...

NResponder.dispatch(null, [null], myObject);
```



---


# Beyond dispatch to targets #

At this point, maybe you already have realized another possibility with targets and dispatch to targets feature. You can use the "target" as a reference or a group to your listeners. You can do things like this:
```
// In a class A
NResponder.add('makeSearch', searchHandler, 0, 0, 1, myObject.stage);

// In a class B
NResponder.add('animateMenuOut', inOutMenu, 0, 0, 0, myObject.stage);
NResponder.add('closeAllModals', closeModals, 0, 0, 0, myObject.stage);

// In a class C
NResponder.add('stopBanner', stopBanner, 0, 0, 0, myObject.stage);

...

// In any class
NResponder.dispatch(null, null, anotherObject.stage);
```

As you noted, in this example the dispatch has the second parameter of "null" instead "[null](null.md)", it is because all the listeners of these NResponders don't expect any parameter.


---


If you have some doubts about this content, leave you comment, check the full documentation here [ASDoc](http://db-in.com/frameworks/nineveh/doc/) or [email me](mailto:diney@db-in.com).

Will be a pleasure to help.