### Why Signals Are Better Than React Hooks

Hooks in React are tricky to use correctly and even harder to use in a performant way. This has left many applications with poor code quality and bad performance, but that doesn’t have to be the case anymore. Signals is a technique that has been around for decades, but only recently has made its way to React and it makes creating performant clean code in React much easier. In this video I explain exactly how signals work and why they are so great.

This video explores the Preact Signals library, demonstrating its advantages over React Hooks. It uses a to-do list app to illustrate how signals simplify code and improve performance. The tutorial covers both basic and advanced signal usage in React.

#### Link
https://preactjs.com/blog/introducing-signals/

#### Example: Using Preact Signals in a To-Do List App

```typescript
import { signal } from '@preact/signals-react';
import { useState } from 'react';

const todoList = signal<string[]>([]);

function TodoApp() {
  const [newTodo, setNewTodo] = useState('');

  const addTodo = () => {
    todoList.value = [...todoList.value, newTodo];
    setNewTodo('');
  };

  return (
    <div>
      <input
        type="text"
        value={newTodo}
        onInput={(e) => setNewTodo(e.currentTarget.value)}
      />
      <button onClick={addTodo}>Add Todo</button>
      <ul>
        {todoList.value.map((todo, index) => (
          <li key={index}>{todo}</li>
        ))}
      </ul>
    </div>
  );
}
```
<p align="center">
  <a href="https://www.youtube.com/watch?v=SO8lBVWF2Y8" target="_blank">
    <img src="https://img.youtube.com/vi/SO8lBVWF2Y8/0.jpg" alt="Watch the video" width="600" />
  </a>
</p>

https://www.youtube.com/watch?v=SO8lBVWF2Y8