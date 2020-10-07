---
title: useLocalStorageRead
tags: hooks,beginner
---

A hook that reads the values from the local storage.

- The hook receives the `key` to `localStorage`, the `defaultValue` to return when the key of the `localStorage` not exist, and a boolean to define the return type.
- The `defaultValue` can be a function or any other type and `withJsonParse` will apply the `JSON.parse` or not.

```jsx
const useLocalStorageRead = (key, defaultValue, withJsonParse = false) => {
  const data = localStorage.getItem(key);
  if (!data && defaultValue)
    return typeof defaultValue === "function" ? defaultValue() : defaultValue;

  return withJsonParse ? JSON.parse(data) : data;
};
```

```jsx
const key = "myKey";

const SimpleComponent = () => {
  const value = useLocalStorageRead(key, () => "defaultValue");

  return <p>{value}</p>;
};

ReactDOM.render(<SimpleComponent />, document.getElementById("root"));
```
