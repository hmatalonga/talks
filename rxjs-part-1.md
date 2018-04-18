<div style="display: flex; align-items: center; justify-content: center; flex-direction: column">

![](images/rx.png)

# RxJS + Vuex + Vue = Awesomeness

### Part I

###### Hackathonners, Braga - 7 April 2018

</div>

---

Managing **state** stuff is **hard**

---

Vuex makes it **simple**

<small>(not necessarily easy)</small>

---

Managing **async** stuff is **harder**

---

RxJS makes it **manageable**

---

<div style="display: flex; align-items: center; justify-content: center;">

<img src="images/profile2.jpg" style="width: auto; height: 300px; border-radius: 50%; margin-right: 50px">

<div class="display: flex; align-items: center; justify-content: center; flex-direction: column">

# Hugo Matalonga

Full Stack Developer

[http://hmatalonga.com](http://hmatalonga.com)

</div>

</div>

---
<!-- page_number: true -->

What are **async** stuff do we commonly do?

---

# Async

- User interactions (mouse, keyboard, etc)
- AJAX
- Timers/Animations
- Web Sockets
- etc

---

Sometimes you need **more control**

---

- AJAX cancellation/composing
- Debounce/throttle/buffer/etc (time manipulation)
- Drag and Drop
- Web Sockets, etc

---

Use **middleware** to manage **async**/side effects

---

Most of them use **callbacks** or **Promises**

---

# Callbacks

The most **primitive** way to handle **async** in JavaScript

---

# [Live code](http://jsbin.com/gecivit/1/edit?html,js,output)

---

# Promises

- Guaranteed future
- Immutable
- Single value
- Caching

---

Promises cannot be cancelled!

---

Why you would want to **cancel**?

---

- Changing routes/views
- Auto-complete
- User wants you to

---

Cancelling is **common** and often **overlooked**

---

What do we use?

---

**Observables**

---

# Observables

- Stream of zero, one or more values
- Over any amount of time
- Cancellable

---

Streams are a **set**, with a **dimension of time**

---

Being **standardized** for ECMAScript aka **JavaScript**

---

# RxJS

> "lodash for events" - Ben Lesh

---

# Creating Observables

```javascript
.of('hello')
.from([1, 2, 3, 4])
.interval(1000)
.ajax('http://example.com')
.webSocket('ws://echo.websocket.com')
.fromEvent(button, 'click')
```

many more...

---

# Subscribing

```javascript
myObservable.subscribe(
  value => console.log('next', value)
)
```

> Subscribing to an Observable is like calling a function, providing callbacks where the data will be delivered to.

---

# Subscribing

```javascript
myObservable.subscribe(
  value => console.log('next', value)
  err => console.error('error', err)
)
```

---

# Subscribing

```javascript
myObservable.subscribe(
  value => console.log('next', value)
  err => console.error('error', err)
  () => console.log('complete!')
)
```

> In an Observable Execution, zero to infinite Next notifications may be delivered. If either an Error or Complete notification is delivered, then nothing else can be delivered afterwards.

---

Observables can be **transformed**

*map, filter, reduce*

---

Observables can be **combined**

*concat, merge, zip*

---


Observables represent **time**

*debounce, throttle, buffer, combineLastest*

---

Observables are **lazy**

*retry, repeat*

---

Observables can **represent** just about **anything**

---

# [Live code](http://jsbin.com/gonigup/3/edit?html,js,output)

---

That's all. **Thanks**.
Question time!
