---
title: DatePicker
tags: input,beginner
---

Renders an `<input type="date">` (date picker) element that uses a callback function to pass its value to the parent component.

- Render an `<input>` element with the appropriate attributes and use the `callback` function in the `onChange` event to pass the value of the date picker to the parent.
- Use the `selected` prop to specify an initial date to the date picker.
- Omit the `minDate` and the `maxDate` prop to define a minimum and maximum dates for the date picker.


```jsx
function DatePicker({ callback, selected, minDate, maxDate }) {
  return (
    <input
      type="date"
      value={selected}
      min={minDate}
      max={maxDate}
      onChange={({ target: { value } }) => callback(value)}
    />
  );
}
```

```jsx
ReactDOM.render(
  <DatePicker callback={val => console.log(val)} />,
  document.getElementById('root')
);
```
