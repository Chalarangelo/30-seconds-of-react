---
title: Filter
tags: components,state,effect,beginner
---

Filters some data by a value and uses a render prop to render the filtered data

- Use object destructuring to set default for `data` prop so data is an empty array when not provided
- Use the `React.useState` hook to create a state for `filteredData` and initialize to `data` prop initially
- Use the `React.useEffect` hook to listen for changes in `data`, `property` & `value` props
- On any change in props, attempt to filter the data
- Inside `React.useEffect` if the `property` prop does not exist or is an empty string save the initial `data` prop to `filteredData` so that it will return all items when no property is filtered
- If the `property` exists, filter the data using `Array.prototype.filter()` by checking if the `property` field of current item is equal to the `value`, and return all items that match.
- Finally save the filteredData to state variable `filteredData`
- Check if the `render` prop is provided, if not, returns null
- If the `render` prop is provided, pass the `filteredData` to the `render` for the parent to handle rendering

```jsx
const Filter = ({ data = [], property, value, render }) => {
  const [filteredData, setFilteredData] = React.useState(data);

  React.useEffect(() => {
    if (!property?.length) {
      setFilteredData(data);
      return;
    }
    const filtered = data.filter((item) => item[property] === value);
    setFilteredData(filtered);
  }, [data, property, value]);

  return !render ? null : <>{render(filteredData)}</>;
};
```

```jsx
const data = [
  { id: "user1", status: "active" },
  { id: "user2", status: "inactive" },
  { id: "user3", status: "active" },
];
ReactDOM.render(
  <Filter
    data={data}
    property="status"
    value="active"
    render={(data) => (
      <div>
        All active users
        {data.map((user) => (
          <>
            <div>{`User: ${user.id}`}</div>
            <div>{`Status: ${user.status}`}</div>
          </>
        ))}
      </div>
    )}
  />,
  document.getElementById("root")
);
```
