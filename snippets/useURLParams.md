---
title: useURLParams
tags: hooks,navigation,URL,advanced
---

A hook that returns current URL params and allows changing them

- Create a custom hook that doesn't take any parameters
- Initalize a new `URL` instance with value from `window.location.href`
- Use `React.useMemo` hook that will store URL params object and update it when `window.location.search` changes
- Reduce `url.searchParams.entries()` into an object with key, value pairs
- Create `setParam` function that accepts `key` and `value`, updates `url.searchParams` object and redirect to stringified `URLSearchParams`.

```jsx
function useURLParams() {
  const url = new URL(window.location.href);

  const params = useMemo(
    () =>
      [...url.searchParams.entries()].reduce(
        (prev, [key, value]) => ({ ...prev, [key]: value }),
        {}
      ),
    [window.location.search]
  );

  function setParam(key, value) {
    url.searchParams.set(key, value);
    window.location.search = url.searchParams.toString();
  }

  return {
    params,
    setParam
  };
}
```

```jsx
const { params, setParam } = useURLParams();

return (
  <div>
    <pre>{JSON.stringify(params)}</pre>
    <button onClick={randomizeParam}>Change to random param</button>
  </div>
);

function randomizeParam() {
  setParam("test_param", Math.ceil(Math.random() * 100));
}
```
