### useSyncExternalStore: The Most Underrated React Hook You've Never Used

`useSyncExternalStore` is a React hook designed for subscribing to external data sources in a way that ensures compatibility with React's concurrent features, such as Suspense and concurrent rendering. It helps prevent tearing (inconsistent UI states) when the external store updates during a render. This hook is particularly useful for integrating with browser APIs, third-party libraries, or any mutable data that exists outside of React's state management.

#### Example: Subscribing to Window Dimensions

```typescript
import { useSyncExternalStore } from 'react';

function getWindowDimensions() {
  return {
    width: window.innerWidth,
    height: window.innerHeight,
  };
}

function subscribe(callback: () => void) {
  window.addEventListener('resize', callback);
  return () => window.removeEventListener('resize', callback);
}

function WindowDimensions() {
  const dimensions = useSyncExternalStore(subscribe, getWindowDimensions);

  return (
    <div>
      <p>Width: {dimensions.width}</p>
      <p>Height: {dimensions.height}</p>
    </div>
  );
}
```

<p align="center">
  <a href="https://www.youtube.com/watch?v=WBPUz1u2rZ8" target="_blank">
    <img src="https://img.youtube.com/vi/WBPUz1u2rZ8/0.jpg" alt="Watch the video" width="600" />
  </a>
</p>

https://www.youtube.com/watch?v=WBPUz1u2rZ8