# React Native: Unhandled Promise Rejection in useEffect with fetch

This repository demonstrates a common error in React Native applications involving asynchronous operations within the `useEffect` hook and how to properly handle them to prevent unexpected behavior and potential memory leaks.

## Bug Description

The original code performs a `fetch` call within the `useEffect` hook.  If the component unmounts before the `fetch` promise resolves, the promise may remain pending and cause issues.  The solution involves using `AbortController` to cleanly interrupt the fetch operation when the component is unmounted.

## Bug Solution

The solution uses `AbortController` to create an AbortSignal.  This signal is passed to the `fetch` call, and the `useEffect`'s cleanup function calls `controller.abort()` to signal the fetch to stop when the component is unmounted.  This prevents the unhandled promise rejection and avoids potential memory leaks.  Error handling is improved to filter out `AbortError` exceptions.