### How to Run Code Only Once in React

In React development, especially in strict mode (enabled by default in Create React App and Next.js), effects and other code might run multiple times during development to help detect side effects. However, for certain operations like API calls, logging, or other side effects, you may want to ensure they execute only once per component lifecycle, even in strict mode.

The `useRef` hook can be used to create a flag that prevents code from running more than once. By initializing a ref with `false` and checking/setting it inside the effect, you can guard against multiple executions.

#### Link
https://www.youtube.com/watch?v=jmPVg5zRUlU

#### Example: Running an Effect Only Once with useRef

```typescript
import { useEffect, useRef } from 'react';

function MyComponent() {
  const hasRun = useRef(false);

  useEffect(() => {
    if (hasRun.current) return;

    hasRun.current = true;

    // Code that should run only once
    console.log('This will only log once, even in strict mode');
    
    // Example: API call
    fetch('/api/initialize')
      .then(response => response.json())
      .then(data => {
        // Handle initialization data
      });
  }, []);

  return <div>My Component</div>;
}
```

#### Example: Preventing Duplicate Subscriptions

```typescript
import { useEffect, useRef } from 'react';

function ChatComponent({ roomId }) {
  const hasSubscribed = useRef(false);

  useEffect(() => {
    if (hasSubscribed.current) return;

    hasSubscribed.current = true;

    const subscription = subscribeToChat(roomId, (message) => {
      // Handle incoming messages
    });

    return () => {
      subscription.unsubscribe();
    };
  }, [roomId]);

  return <div>Chat Room: {roomId}</div>;
}
```

#### When to Use This Pattern

- When you have side effects that should absolutely not run multiple times
- In development with React strict mode enabled
- For initialization code that sets up global state or connections
- When working with third-party libraries that don't handle multiple initializations well

#### Note

This pattern is primarily useful in development environments with strict mode. In production, effects with empty dependency arrays already run only once per mount. Use this sparingly and consider if the multiple runs in development are actually problematic for your use case.</content>
<parameter name="filePath">/Users/patti/Documents/Projects/santosh/kb-reactjs/run-code-once.md