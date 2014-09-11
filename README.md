Learning RxJava for Android by example
==============

I've read and watched a lot on Rx. Most examples either use the J8 lambda notations/Scala/Groovy or some other awesome language that us Android developers are constantly envious of.

Unfortunately i could never find real-world simple examples in Android, that could show me how to use RxJava in Android. This repo is a solution to that problem. Below are a list of examples with a little more details on the approach:

## Examples:

### 1. Concurrency using schedulers

A common requirement is to offload lengthy heavy I/O intensive operations to a background thread (non-UI thread), and feed the results back to the UI/main thread, on completion. This is a demo of how long running operations can be offloaded to a background thread. After the operation is done, we resume back on the main thread. All using RxJava! Think of this is as a replacement for AsyncTasks.

The long operation is simulated by a blocking Thread.sleep call. But since it's in a background thread, our UI is never interrupted.

To really see this example shine. Hit the button multiple times and see how the button click (which is a ui operation) is never blocked because the long operation only runs in the background.

### 1. Retrofit and RxJava (zip, flatmap) (wip)

Working examples of github from JakeWharton's Retrofit preso at Netflix
https://www.youtube.com/watch?v=aEuNBk1b5OE#t=2480
https://speakerdeck.com/jakewharton/2014-1

### 1. simpler operations: map/collect (wip)

We have a list of three twitter handles. We wish to get the 3 latest tweets from each of these people, and print them out on our screen.

### 1. First retrieve from cached data, then make a network call if you can't find your data (concat) (wip)

[Courtesy: gist](https://gist.github.com/adelnizamutdinov/7483969)

### 1. Make two parallel network calls, then combine the result into a single data point (zip) (wip)

[Courtesy: gist](https://gist.github.com/adelnizamutdinov/7483969)
http://www.programmableweb.com/category/all/apis?order=field_popularity


### 1. Accumulate calls (buffer)

This is a demo of how events can be accumulated using the "buffer" operation.

A button is provided and we accumulate the number of clicks on that button, over a span of time and then spit out the final results.

If you hit the button once. you'll get message saying the button was hit once. If you hit it 5 times continuosly within a span of 2 seconds, then you get a single log, saying you hit that button 5 times (vs 5 individual logs saying "Button hit once").

Two implementations:

2a. Using a traditional observable - but encompassing the OnClick within the observable
2b. Using PublishSubject and sending single clicks to the Observable, which in-turn then sends it to the Observer

### 1. Instant/Auto searching (subject + debounce)

This is a demo of how events can be swallowed in a way that only the last one is respected. A typical example of this is instant search result boxes. As you type the word "Bruce Lee", you don't want to execute searches for B, Br, Bru, Bruce, Bruce , Bruce L ... etc. But rather intelligently wait for a couple of moments, make sure the user has finished typing the whole word, and then shoot out a single call for "Bruce Lee".

As you type in the input box, it will not shoot out log messages at every single input character change, but rather only pick the lastly emitted event (i.e. input) and log that.

This is the debounce/throttleWithTimeout method in RxJava.

### 1. Orchestrating Observables  (flatmap + zip) (wip)

If actions A and B depend on action X running; and action C depends on action Y running. What if you want to combine the result of all those calls and have a single output?

                     ____________ A  ________________
       (flatmap)    /                                |   (zip all 3)
    X  ------------/_____________ B  ________________| ----------- > Ouput
                                                     |
    Y  -------------------------  C  ________________|



### 1. Pagination (zip) (wip)

a. Simple pagination
b. Optimized pagination



### 1. Replacing your event Bus (wip)

http://stackoverflow.com/questions/19266834/rxjava-and-random-sporadic-events-on-android