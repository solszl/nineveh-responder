# Who should read this #

  * To follow at this point, you need be familiar with the "add" methods of NResponder. You can find all information about this here AddMethods.

# Introduction #

After you created a NResponder with the "add" methods or with the contructor, you can, by anywhere, either in another SWF file, dispatch that NResponder.

In a more advanced chapter you can learn some exclusive features of the dispatch method. You can, for example dispatch all the NResponder of a specific action or dispatch all NResponder of a specific target or either change the parameters to the listeners on the run-time.

For now, let's see a simple dispatch.



---


# Simple dispatch #

To use dispatch is very similar to the dispatch with native Event API. All that you need is call the `dispatch()` method and inform an action. Like this:
```
NResponder.add('someAction', myListener);

...

NRresponder.dispatch('someAction');
```

Remember that in AddMethods chapter is advisable to you store the action in a class to don't miss the spelling. Here is another good reason to do this, you probably will need your action more than one time. So you can organize your actions in one place.


---


# Dispatching with parameters #

The `dispatch()` method has three parameters, the second is about the variables that you want to pass to the listener. You can pass how many variables you want and can change these variables when you want.

Just remember that you need to inform all the variables inside an Array. Like this:
```
NResponder.add('someAction', myListener);

...

NRresponder.dispatch('someAction', [true, 0, 'aString', {andAnObject:null}]);
```

Your listener, in above example "myListener", need to expect 4(four) parameters: Boolean, Number, String and Object, respectively, in this case.

In the DispatchAdvanced you can see a simple way to change these variables "on the fly" and how to do dispatches to an entire target.


---


If you have some doubts about this content, leave you comment, check the full documentation here [ASDoc](http://db-in.com/frameworks/nineveh/doc/) or [email me](mailto:diney@db-in.com).

Will be a pleasure to help.