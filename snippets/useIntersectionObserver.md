---
title: useIntersectionObserver
tags: hooks,effect,state,intermediate
---

Implements Intersection Observer in a declarative manner.

- Create a custom hook that takes a `options` and that uses the `IntersectionObserver` web API to observe intersection an html element.
- Use the `useRef()` hook to create a `ref` for the html element to observe.
- Use the `useState()` hook to create an appropriate state variable, `isVisible`, and setter.
- Create a `callbackFunction` to set the visibility state of the observed html element when the intersection change.
- Use the `useEffect()` hook to add listeners to observer, and cleanup those listeners when unmounting.

```jsx
const useIntersectionObserver = (options) => {
  const containerRef = React.useRef();
  const [isVisible, setIsVisible] = React.useState(false);

  const callbackFunction = (entries) => {
    const [entry] = entries;
    setIsVisible(entry.isIntersecting);
  };

  React.useEffect(() => {
    const observer = new IntersectionObserver(callbackFunction, options);

    if (containerRef.current) observer.observe(containerRef.current);

    return () => containerRef.current && observer.unobserve(containerRef.current);

  }, [containerRef, options]);

  return [containerRef, isVisible];
};
```

```jsx
const App = () => {
  const [containerRef, isVisible] = useIntersectionObserver();
  return <div ref={containerRef}>{isVisible? 'visible': 'not visible' }</div>;
};
ReactDOM.render(<App />, document.getElementById('root'));
```
