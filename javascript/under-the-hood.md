# Under The Hood

## Runtime Concepts

**Stack**: Function calls form a stack of frames. Each frame contains the arguments and variables of a function (like a private workspace for the scope). 

**Heap**: 
> Objects are allocated in a heap which is just a name to denote a large mostly unstructured region of memory.

**Queue**:
> A JavaScript runtime contains a message queue, which is a list of messages to be processed. A function is associated with each message. When the stack has enough capacity, a message is taken out of the queue and processed. The processing consists of calling the associated function (and thus creating an initial stack frame). The message processing ends when the stack becomes empty again.

## Event loop

Javascript runtime contains a message queue. A function is associated with each message. 

> When the stack has enough capacity, a message is taken out of the queue and processed. The processing consists of calling the associated function (and thus creating an initial stack frame). The message processing ends when the stack becomes empty again.

Usually implemented like:
```javascript
while (queue.waitForMessage()) {
	queue.processNextMessage();
}
```
*The queue waits synchronously for a message to arrive if there is none currently*

### Run to completion
Each message is processed completely to completion. 
> Whenever a function runs, it cannot be pre-empted and will run entirely before any other code runs (and can modify data the function manipulates).

Downside: Could block user interaction if a message takes too long to run. Browsers now support a "script taking a long time to run" message.

### Adding messages (Events and setTimeout)
- messages added when event occurs on an event listener
- if there isnt a listener the event is lost
- calling `setTimeout` will add a message to the queue after the time passed, the callback will be called after a *minimum* time specified in the second argument. Not a guarenteed time
- the time after a message is processed is dependent on the remaining messages in the queue

**Note**
> A web worker or a cross-origin iframe has its own stack, heap, and message queue. Two distinct runtimes can only communicate through sending messages via the `postMessage` method. This method adds a message to the other runtime if the latter listens to message events.

*Sources*: [Event Loop](https://developer.mozilla.org/en/docs/Web/JavaScript/EventLoop)
