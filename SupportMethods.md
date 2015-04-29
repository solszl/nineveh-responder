# Who should read this #

  * To follow at this point, you need be familiar with the "add" methods of NResponder. You can find all information about this here AddMethods.
  * You need be familiar with the dispatch method too. You can find all information about this here DispatchBasic.
  * You should know the `has()` and `remove()` methods. You can find all information about this here HasAndRemove.

# Introduction #

NResponder has 4 (four) static supports:
  1. `currentAction`
  1. `currentTarget`
  1. `currentNResponder`
  1. `stopPropagate()`

And 2 (two) instanciated supports:
  1. `paused`
  1. `perform()`


---


# currentAction | currentTarget | currentNResponder #

Also know as "currents", these three methods have a very similar behavior. They are read-only properties and just works during a dispatch. This means you try to call one of these outside a listener of NResponder, you will have `null` as response.

The function of "currents" is give to you a shortcut to access some importants characteristics of a dispatch. If you are using the "static mode" (see UsageModes for information about modes) or don't have access to the instance of NResponder, you can use these properties to retrieve what you need.

The name of property very direct and say what it return:
  * `currentAction`: Return the Action of the current dispatching.
  * `currentTarget`: Return the Target associated with the current dispatching.
  * `currentNResponder`: Return the NResponder instance that produced the current dispatching.

The following example will show how "currents" can respond different in different places of your application.
```
NResponder.add('actionOne', listenerOne);
NResponder.add('actionTwo', listenerTwo);
NResponder.addNative(myButton, MouseEvent.CLICK, clickHandler);

trace(NResponder.currentAction); // Will output "null"
trace(NResponder.currentTarget); // Will output "null"

...

// Start dispatching "listenerOne".
NResponder.dispatch('listenerOne');

...

function listenerOne():void
{
    trace(NResponder.currentAction); // Will output "actionOne"
    trace(NResponder.currentTarget); // Will output "null"
    
    // Before finish this dispatch, let's dispatch another NResponder, doing a multiple dispatch.
    NResponder.dispatch('actionTwo');
}

function listenerTwo():void
{
    trace(NResponder.currentAction); // Will output "actionTwo"
    trace(NResponder.currentTarget); // Will output "null"
}

function clickHandler(event:MouseEvent):void
{
    trace(NResponder.currentAction); // Will output "click"
    trace(NResponder.currentTarget); // Will output "[myButton object]"
    
    // Any click on "myButton" will dispatch the Action "listenerOne" too.
    NResponder.dispatch('listenerOne');
}
```



---


# stopPropagate() #

This method is very simple and similar to native `stopImediatePropagation()`. This method immediately stop the dispatching process of a specific Action.

For example, suppose that you have a photos gallery and you need to make a ZOOM on entire gallery if the user MOUSE\_WHEEL on background (stage), but if the user make a MOUSE\_WHEEL over a specific photo, just it will ZOOM:
```
NResponder.addNative(eachPhotoInstance, MouseEvent.MOUSE_WHEEL, zoomPhoto);

// Set the NResponder to stage after.
// Or if you need to the NResponder to stage first, set it order to 1, for example.
NResponder.addNative(this.stage, MouseEvent.MOUSE_WHEEL, zoomGallery);

...

function zoomPhoto(event:MouseEvent):void
{
    // Do something.
    ...
    NResponder.stopPropagate();
}

function zoomGallery(event:MouseEvent):void
{
    // This method just will be called if the user make a MOUSE_WHEEL on stage AND outside a photo.
    // Just do something.
}
```


---


# paused #

You can change this property any time you want. When `paused` is TRUE, the NResponder will not perform the listener and any attribute like `replies` or `delay` will not be counted down. When paused, the NResponder completely ignores any dispatch.

For example:
```
var myResponder:NResponder = NResponder.add('anAction', aListener, 0, 0, 0, aTarget);
myResponder.pause = true;

// Both following dispatches will result in nothing, because the NResponder is paused.
NResponder.dispatch('anAction');
NResponder.dispatch(null, null, aTarget);

...

function aListener():void
{
    // This listener will not be dispatched until "myResponder" is unpaused.
}
```


---


# perform() #

With this method you can perform the listener of a NResponder without use the common behavior, this means that properties like `replies` or `delay` will not be counted down.

If you want, you can respect the delay time, but is not necessary.

For example:
```
var myResponder = NResponder.add('anAction', aListener, 2, 4);

// After the following dispatch, NResponder will down its replies to 1 and need to wai 4 seconds until next dispatch.
NResponder.dispatch('anAction', ['stringParameter']);

// The following three dispatch will be performed without count down the number of replies and without wait the previously delay of 4 seconds.
myResponder.perform(['stringParameter']);
myResponder.perform(['stringParameter']);

// The perform() method return a Boolean indicating if it has successful or not.
trace(myResponder.perform(['stringParameter'])); // Output "true"

// Now the following dispatch will respect the delay time, using TRUE in the second parameter.
// This method will return FALSE, because it cannot conclude the perform.
trace(myResponder.perform(['stringParameter'], true)); // Output "false"

...

function aListener(newString:String):void
{
    trace('Performing the aListener, with', newString, 'parameter');
}
```


---


If you have some doubts about this content, leave you comment, check the full documentation here [ASDoc](http://db-in.com/frameworks/nineveh/doc/) or [email me](mailto:diney@db-in.com).

Will be a pleasure to help.