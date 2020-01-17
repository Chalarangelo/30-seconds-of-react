---
title: DecimalInput
tags: input,state,beginner
---

Renders a float input field.

- If you need an initial value, define it as `defaultValue`.
- By modifying the regular expression, you can limit the number of decimal places.

```jsx
function DecimalInput({
  defaultValue = "",
  placeholder = ""
}) {
  const [value, setValue] = React.useState(defaultValue);

  const handleOnChange = (event) => {
    const value = event.target.value;
    const floatRegExp = new RegExp("^[+-]?([0-9]+([.][0-9]*)?|[.][0-9]+)$")

    if (value === '' || floatRegExp.test(value)) {
      setValue(value);
    }
  }

  return (
    <input
      defaultValue={defaultValue} 
      placeholder={placeholder}
      value={value} 
      onChange={(event) => handleOnChange(event)}/>
  );
}
```

```jsx
ReactDOM.render(<DecimalInput placeholder="Input Number"/>, document.getElementById('root'));
```
