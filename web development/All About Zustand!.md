# Zustand: A Simple and Flexible State Management Library for React

![Article header image](https://miro.medium.com/v2/resize:fit:640/format:webp/1*XuyDEBPesOwMlT2XRNtCMg.png)

Zustand is a state management library for React that provides a simple and flexible way to manage application states. It is built on top of the React Context API and utilizes the power of modern JavaScript features such as proxies and generators.

Zustand makes it easy to create and update complex state structures, handle asynchronous actions, and share states between components. It is designed to be easy to use and lightweight, with a minimal API that can be learned quickly.

## Example Usage

Here is an example of how to use Zustand in a simple React application:

First, we need to install the Zustand package from npm:

`npm install zustand`

Then, let’s create a store using the `create` function provided by Zustand:

```tsx
import create from "zustand";

const useCounterStore = create((set) => ({
    count: 0,
    increment: () => set((state) => ({ count: state.count + 1 })),
    decrement: () => set((state) => ({ count: state.count - 1 })),
}));
```

This creates a store that holds a count value and two functions `increment` and `decrement` that can be used to update the count value.

Now, let's create two components that use the `useCounterStore` hook to access the state and update it:

```tsx
import React from "react";
import { useCounterStore } from "./useCounterStore";

function CounterDisplay() {
    const count = useCounterStore((state) => state.count);

    return <div>{count}</div>;
}

function CounterButtons() {
    const increment = useCounterStore((state) => state.increment);
    const decrement = useCounterStore((state) => state.decrement);

    return (
        <div>
            <button onClick={increment}>+</button>
            <button onClick={decrement}>-</button>
        </div>
    );
}
```

The `CounterDisplay` component uses the `useCounterStore` hook to get the current `count` value from the store and display it.

The `CounterButtons` component uses the `useCounterStore` hook to get the `increment` and `decrement` functions from the store and use them as click handlers for two buttons.

Finally, we can use these components in our main `App` component:

```tsx
import React from "react";
import { CounterDisplay, CounterButtons } from "./components";

function App() {
    return (
        <div>
            <CounterDisplay />
            <CounterButtons />
        </div>
    );
}

export default App;
```

## Selectors

Selectors allow you to derive values from your state in a way that is composable and efficient. You can define a selector function that takes the current state and returns a derived value, and then use the `useSelector` hook to access that value.

Here is an example of how to use a selector with Zustand:

```tsx
import create from "zustand";

const useCounterStore = create((set) => ({
    count: 0,
    increment: () => set((state) => ({ count: state.count + 1 })),
    decrement: () => set((state) => ({ count: state.count - 1 })),
    doubleCount: (state) => state.count * 2,
}));

function CounterDisplay() {
    const count = useCounterStore((state) => state.count);
    const doubleCount = useCounterStore((state) => state.doubleCount);

    return (
        <div>
            <div>Count: {count}</div>
            <div>Double Count: {doubleCount}</div>
        </div>
    );
}
```

In this example, we've added a `doubleCount` function to our store that returns the current `count` multiplied by 2. We then use the `useSelector` hook to access both the `count` and `doubleCount` values in the `CounterDisplay` component.

# Middleware

Middleware allows you to intercept and modify state updates before they are applied. This can be useful for logging, performance monitoring, or other custom behavior.

Here is an example of how to use middleware with Zustand:

```javascript
import create from "zustand";

const useCounterStore = create(
    (set) => ({
        count: 0,
        increment: () => set((state) => ({ count: state.count + 1 })),
        decrement: () => set((state) => ({ count: state.count - 1 })),
    }),
    (get) => (next) => (args) => {
        console.log("State before update:", get());
        next(args);
        console.log("State after update:", get());
    }
);
```

In this example, we’ve added a middleware function that logs the current state before and after each update. The `get` function can be used to access the current state, and the `next` function is used to apply the update.

## Immer Integration

Zustand also has built-in support for [Immer](https://immerjs.github.io/immer/docs/introduction), a library that simplifies the process of working with immutable data structures. With Immer, you can write code that looks like it’s mutating data, but actually creates new copies of the data that are updated immutably.

Here is an example of how to use Immer with Zustand:

```javascript
import create from "zustand";
import { produce } from "immer";

const useTodoStore = create((set) => ({
    todos: [],
    addTodo: (text) => {
        set(
            produce((state) => {
                state.todos.push({ text, done: false });
            })
        );
    },
    toggleTodo: (index) => {
        set(
            produce((state) => {
                state.todos[index].done = !state.todos[index].done;
            })
        );
    },
}));
```

In this example, we use the `produce` function from Immer inside our store's update functions to create a new copy of the state with the desired changes. This allows us to write code that looks like it’s mutating data, but actually creates new copies of the data that are updated immutably.

Here is an example of how to use Immer with Zustand:

```javascript
import create from "zustand";
import produce from "immer";

const useCounterStore = create((set) => ({
    count: 0,
    increment: () =>
        set(
            produce((draft) => {
                draft.count += 1;
            })
        ),
    decrement: () =>
        set(
            produce((draft) => {
                draft.count -= 1;
            })
        ),
}));
```

In this example, we’ve used the `produce` function from Immer to create new copies of the state that are updated immutably. The `set` function provided by Zustand then applies these updates to the actual state.

## Conclusion

Zustand is a powerful and flexible state management library for React that provides a simple and intuitive API. It can help you manage your state more efficiently, and provides features like selectors, middleware, and Immer integration to make your life easier.

If you’re interested in learning more about Zustand, be sure to check out the [official documentation](https://github.com/pmndrs/zustand) 😉

## Show Your Support!

> Are you enjoying the content I’m putting out? If so, I would love for you to show your support by following, applauding, and commenting on my post!
> By following my account, you’ll be the first to know when I publish new content, and you’ll never miss a beat. Liking my posts lets me know that you appreciate the content I’m creating and commenting allows us to engage in a conversation and share our thoughts on the topic at hand.
> Your feedback means the world to me, and it also helps me improve my content to better meet your needs and interests. So, don’t be shy! Let me know what you think, and together, let’s build a community that inspires and uplifts one another.
> Thank you for your continued support! 🎉✨
