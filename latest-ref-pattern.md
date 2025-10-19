### The Latest Ref Pattern in React

React's `useRef` hook is a powerful tool for persisting values across renders without causing re-renders. This pattern is particularly useful for scenarios where you need to store a reference to a callback or a value that changes over time but doesn't need to trigger a re-render.

In this example, we demonstrate how to use the `useRef` hook to store a reference to a callback function and ensure it is always up-to-date without re-running effects unnecessarily.

#### Example: Using `useRef` to Store a Callback

```typescript
import { useEffect, useRef } from 'react';

type PageProps = {
  onChange: () => void;
};

function Page({ onChange }: PageProps) {
  const onChangeRef = useRef(onChange);

  useEffect(() => {
    onChangeRef.current = onChange;
  });

  useEffect(() => {
    onChangeRef.current();
  }, []);

  return null;
}
```

<p align="center">
  <a href="https://www.youtube.com/watch?v=Zu0jjIpQTg4" target="_blank">
    <img src="https://img.youtube.com/vi/Zu0jjIpQTg4/0.jpg" alt="Watch the video" width="600" />
  </a>
</p>

https://www.youtube.com/watch?v=Zu0jjIpQTg4