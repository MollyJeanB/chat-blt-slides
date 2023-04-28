---
# try also 'default' to start simple
theme: dracula
class: 'text-center'
# https://sli.dev/custom/highlighters.html
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## ChatBLT slides via Slidev

  Learn more at [Sli.dev](https://sli.dev)
# page transition
transition: slide-left
---

# ChatBLT
### 🥓🥬🍅
The Amazing AI Chat program that isn't listening to you and only wants to talk about sandwiches.



<!--
quick demo of ChatGPT vs. ChatBlT
-->

---

# Why ChatBLT? 

### 🥓🥬🍅

Playing around with ChatGPT got me thinking about the realities of human communication, both text-based an IRL. People often misunderstand each other, don't listen well, etc. So I had the idea to create a "chatbot" that's basically a tech bro mainsplaining something to you at a party and not listening to your side of the conversation at all.

Then I wanted to come up with a cleverish name that sounded kind of like ChatGPT, ideally some acronym that also ended with a T. I landed on ChatBLT, which I decided stood for Bad Listener Tom. But also Bacon Lettuce Tomato. Originally I thought the AI would drone on about all kinds of things like crypto and keto and Joe Rogan, but then, with some nudging from Jaime :), I decided he should stick to sandwiches

<!--
Here is another comment.
-->

---
layout: default
---

# Planning Goals

### 🥓🥬🍅

## To Dos
* Rough dupe of ChatGPT intro page
* Form that consists of a single text input and button, and can be submitted via the return key
* comment list component that displays the users input, followed by the "AI response" (randomized string from an array)
* text animation on each new response
* ability to reset state and start new conversation via a button (non-critical stretch goal)

## Stack
* React + TypeScript + CSS Modules via my Next.js boilerplate
---
layout: default
---

# Some Fun I Had Along the Way

* Fun with SVGs

```ts {all|2|1-6|9|all}
interface User {
  id: number
  firstName: string
  lastName: string
  role: string
}

function updateUser(id: number, update: User) {
  const user = getUser(id)
  const newUser = { ...user, ...update }
  saveUser(id, newUser)
}
```
---
layout: default
---

# Some Fun I Had Along the Way

* Fun with SVGs

```ts {all|2|1-6|9|all}
interface User {
  id: number
  firstName: string
  lastName: string
  role: string
}

function updateUser(id: number, update: User) {
  const user = getUser(id)
  const newUser = { ...user, ...update }
  saveUser(id, newUser)
}
```

