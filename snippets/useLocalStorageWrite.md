---
title: useLocalStorageWrite
tags: hooks,state,effect,beginner
---

A hook that writes in the local storage when some state changed.

- The hook receives the `key` to `localStorage`, the `data` to write, and a function to handle with the error.
- The `React.useEffect` is used to observe the `data` and write the new values ​​in `localStorage`.
- If the `data` exceeded the limit of the `localStorage` or happen any error, the `onError` will be called.

```jsx
const useLocalStorageWrite = (key, data, onError = () => {}) => {
  React.useEffect(() => {
    if (!key) return;
    try {
      localStorage.setItem(key, JSON.stringify(data));
    } catch (e) {
      onError(e);
    }
  }, [key, data, onError]);
};
```

```jsx
const key = "myKey";

const SimpleComponent = () => {
  const [name, setName] = React.useState("");

  useLocalStorageWrite(key, name);

  return (
    <React.Fragment>
      <p>{localStorage.getItem(key) || ""}</p>
      <input
        type="text"
        onChange={(e) => {
          const name = e.target.value;
          setName(name);
        }}
      />
    </React.Fragment>
  );
};

ReactDOM.render(<SimpleComponent />, document.getElementById("root"));
```
