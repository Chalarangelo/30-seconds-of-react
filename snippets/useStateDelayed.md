---
title: useStateDelayed
tags: hooks,state,effect,intermediate
---

A hook that delays loading initial state until some condition is met.

- Create a custom hook that takes `initialState` and `condition`
- Add 2 `React.useState()` hooks to keep the *state* and information if condition have already been set to true
- Define a `updateState` function that will update the state and mark it as initalized. This way when you update state `initialState` won't be loaded again.
- Use the `React.useEffect()` hook to watch for changes of `condition` and update state with `initialState` when it changes to `true`.
- Return an array of `state` and `updateState` function

```jsx
function useStateDelayed(initialState, condition) {
  const [state, setState] = React.useState(null);
  const [loaded, setLoaded] = useState(false);

  React.useEffect(() => {
    if (!loaded && condition) {
      updateState(initialState);
    }
  }, [condition, loaded]);

  function updateState(change) {
    setState(change);
    setLoaded(true);
  }

  return [state, updateState]
}
```

```jsx
const EXAMPLE_BRANCHES_LIST = ['main','stage','dev'];

const [branches, setBranches] = useState([]);
const [selectedBranch, setSelectedBranch] = useStateDelayed(() => {
  // find default branch
  const commonBranch = branches.find(branch => branch === 'master' || branch === 'main');
  if (commonBranch) return commonBranch;
  return branches[0];
}, !!branches.length);

useEffect(() => {
  const handle = setTimeout(() => {
    setBranches(EXAMPLE_BRANCHES_LIST)
  }, 1000);

  return () => {
    handle && clearTimeout(handle);
  }
}, []);

return (
    <div>
      <p>Selected branch: {selectedBranch}</p>
      <select onChange={e => setSelectedBranch(e.target.value)}>
        {branches.map(branch => <option key={branch} value={branch}>{branch}</option>)}
      </select>
    </div>
  )
```
