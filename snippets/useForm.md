---
title: useForm
tags: hooks,effect,state,advanced
---

A hook that updates a form values state.

- Create a custom hook that takes a `initialValues`.
- Use the `React.useState()` hook to initialize the `values` state variable.
- Return the values and a function to update the form.

```jsx
const useForm = (initialValues) => {
  const [values, setValues] = useState(initialValues);

  return [
    values,
    e => {
      setValues({
        ...values,
        [e.target.name]: e.target.value,
      });
    },
  ];
};

```

```jsx
const Form = props => {
 const initialState = { email: '', password: '' };
  const [values, setValues] = useForm(initialState);

  return (
    <form>
      <input type="email" name="email" onChange={setValues} />
      <input type="password" name="password" onChange={setValues} />
    </form>
  );
};

ReactDOM.render(<Form />, document.getElementById('root'));
```
