# Who should read this #

  * To follow at this point, you need be familiar with Usage Modes of NResponder. You can find all information about this here UsageModes.

# Introduction #

NResponder engine can work with it's own API of events or use the native Adobe® Flash® Event API. This means that you can use the NResponder to a custom event, like "doSearch" for example, or use it to a MouseEvent.MOUSE\_DOWN ("mouseDown") in a button.

Using NResponder to a native events you gain a lot of performance, because not the entire process of Native API of Flash is used and you can use all the benefits and features of NResponder, of course.

These two way can be accessed by `add()` and `addNative()` methods, respectively. Or using the parameter "isNative" in the constructor.

In both ways, you can completely replace the use of addEventListener and removeEventListener in your application.


---


# Where and when to use? #

Are you a little confuse about use `add()` or `addNative()`?

Is very simple. You just need to remember: "`addNative()` is only to use when my call back function needs to expect an Event class or a class that inherits from Event!".

To any other cases, just use the `add()` method.

Other thing to remember is that `addNative()` method need a target that implement the `addEventLister()` and `removeEventListener()` methods. For example, almost all object classes in Flash Framework inherits from EventListener and has these two methods.

The [SWFAddress](http://www.asual.com/swfaddress/), for example, is a static class that doesn't inherit from EventListener, but it has implementations of `addEventLister()` and `removeEventListener()` methods. Because of it you can use NResponder to events of [SWFAddress](http://www.asual.com/swfaddress/) class. Like this:
```
NResponder.addNative(SWFAddress, SWFAddressEvent.INIT, init, 1);
NResponder.addNative(SWFAddress, SWFAddressEvent.CHANGE, change);
```

Remember the rule of `addNative()`, the call back function, in this case, "`init()`" and "`change()`" will need to expect an "`SWFAddressEvent`" (inherited from Event).

Another third part classes, like [Away3D](http://away3d.com/), [PaperVision3D](http://blog.papervision3d.org/), [FLAR Manager](http://words.transmote.com/wp/flarmanager/), [TweenMax](http://www.greensock.com/v11/) and others, will happen a similar behavior in their event classes, because they use the native Event API of Flash.


---


# add() #

Use this to all custom events of your application. If you are using the Nineveh Framework, use this method to all events/notifications of the Nineveh Framework.

The usage if very simple:
```
NResponder.add('someAction', myListener);
```

In a complex application, is advisable to use a class with static constants to store your actions. In this way, you will not risk to miss the spelling of the actions in different classes.
```
// Class AppActions.as
package com.actions
{
    public class AppActions
    {
        /**
         * A constant to indicate the action of a Search in an Application, for example.
         */
        public static const SEARCH:String = 'doSearch';
        
        /**
         * A constant to indicate the action to call a page, for example.
         */
        public static const GO_PAGE:String = 'gotoPage';
    }
}

// Class ViewController.as
package com.controls
{
    import com.actions.AppActions;
	
    import appkit.responders.NResponder;
    
    public class ViewController
    {
        public function ViewController():void
        {
            NResponder.add(AppActions.GO_PAGE, pageHandler);
            NResponder.add(AppActions.SEARCH, searchHandler);
        }
    }
}

```


---


# addNative() #

Using NResponder to work with native Event API you have a gain of performance and memory to your application, because NResponder use just a little part of native Event API of Flash. The first gain is that you have less parameters to specify:
```
// Instead this
myObject.addEventListener(MouseEvent.MOUSE_UP, clickHandler, false, 0, true);

// Use this
NResponder.addNative(myObject, MouseEvent.MOUSE_UP, clickHandler);
```

The `addNative()` method is more like a shortcut to the constructor. In the NResponder constructor has a parameter called "`isNative`" (the last parameter) that indicate if the new NResponder will work or not with native Event API of Flash.
So when you call the static method `addNative()` it automatically set the "`isNative`" parameter to `true`.

To work with native Event API, NResponder need a target that implements the `addEventListener()` and `removeEventListener()`. So, to simplify the things, the `addNative()` method requires this target as the first parameter.
```
import flash.events.MouseEvent;
...

var myButton:MovieClip;

NResponder.addNative(myButton, MouseEvent.MOUSE_OVER, overOutHandler);
NResponder.addNative(myButton, MouseEvent.MOUSE_OUT, overOutHandler);
NResponder.addNative(myButton, MouseEvent.MOUSE_UP, clickHandler);
```

Remember that to use NResponder with native Event API you need to prepare the listener to expect one parameter of Event.
```
function overOutHandler(event:MouseEvent):void
{
    trace('Returned by NResponder with native Event API:',event);
}
```

At this point, using NResponder to work with native Event API, can seems very similar to EventDispatcher methods, but in the next chapters you will see how graceful and helpful can be NResponder in native Event API too.


---


If you have some doubts about this content, leave you comment, check the full documentation here [ASDoc](http://db-in.com/frameworks/nineveh/doc/) or [email me](mailto:diney@db-in.com).

Will be a pleasure to help.