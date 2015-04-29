# Who should read this #

  * If you don't have any idea of what is NResponder, this is the way. Follow reading with an idea in you mind: "NResponder engine came to replace the native Event API of Flash (EventListeners, IEventListener, Events, etc...)".


---


# Introduction #

NResponder engine can be used in two ways: a static mode, more directly, and a instantiated mode, where you have more control on NResponder object. Is advisable use the static mode in general cases and let the instantiated mode just to cases where you needs additional control on NResponder or need to change attributes "on the fly".


---


# Static Mode #

This mode is very simple, just import the NResponder class and can the "adds" methods, like this:
```
import appkit.responders.NResponder
...
NResponder.add('someIdentify', callBackListener);

// or this

NResponder.addNative(someObject, Event.ADDED_TO_STAGE, callBackListener);
```

One important thing to remember is that even the static mode return to you an instance of NResponder. But if you don't store it instance in a variable you can't retrieve that instance after.


---


# Instantiated Mode #

To use the instantiated mode you can store the instance returned by static mode in a variable. Like this:
```
var nrInstance:NResponder;

nrInstance = NResponder.add('someIdentify', callBackListener);

// or

nrInstance = NResponder.addNative(someObject, Event.ADDED_TO_STAGE, callBackListener);
```

Or if you prefer a more object oriented declaration, you can use the constructor like this:
```
var nrInstance:NResponder = new NResponder.add('someIdentify', callBackListener);
```

But remember that `add()` and `addNative()` is shortcuts to the default constructor method and if you prefer use the constructor you will need to pass all the parameters in line code. Like this:
```
var nrInstance:NResponder = new NResponder.add('someIdentify', callBackListener, 0, 0, 0, someObject, true);
```

This is necessary because the target of NResponder and the switch of native events is the last two parameters in the constructor.

Now, the advantage of the instantiated mode is you can change some parameters during the runtime, like this:
```
var nrInstance:NResponder = NResponder.add('someIdentify', callBackListener);

nrInstance.order = 3;
if (!nrInstance.paused) nrInstance.paused = true;
```



---


If you have some doubts about this content, leave you comment, check the full documentation here [ASDoc](http://db-in.com/frameworks/nineveh/doc/) or [email me](mailto:diney@db-in.com).

Will be a pleasure to help.