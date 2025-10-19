
### I'm Ditching Try/Catch for Good!

The try/catch block is a staple of JavaScript, but it leaves a lot to be desired (especially when working with TypeScript). None of the errors are typed, it adds an extra level of block scoping which can make certain code difficult to write, and it catches all errors (not just the ones you want). That is why in this video I will show you 3 alternatives to try/catch that I much prefer.

```typescript
export async function catchError<T, E extends new (message?: string) => Error>(
  promise: Promise<T>,
  errorsToCatch?: E[],
): Promise<[undefined, T] | [InstanceType<E>]> {
  return promise
    .then((data) => {
      return [undefined, data] as [undefined, T];
    })
    .catch((error) => {
      if (errorsToCatch == undefined) {
        return [error];
      }

      if (errorsToCatch.some((e) => error instanceof e)) {
        return [error];
      }

      throw error;
    });
}
```

<p align="center">
  <a href="https://www.youtube.com/watch?v=AdmGHwvgaVs" target="_blank">
    <img src="https://img.youtube.com/vi/AdmGHwvgaVs/0.jpg" alt="Watch the video" width="600" />
  </a>
</p>

https://www.youtube.com/watch?v=AdmGHwvgaVs