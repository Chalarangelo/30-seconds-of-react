---
title: useAnimation
tags: hooks,state,reducer,intermediate
---

A hook that handles animation.

- Create a custom hook that receives a `loading` and `time` parameters.
- Use the `React.useEffect()` hook to change the `render` state and `showAnimation` state.

```jsx
const useAnimation = (loading, time) => {
  const [render, setRender] = useState(loading);
  const [showAnimation, setShowAnimation] = useState('false');

  useEffect(() => {
    let timeoutAnimation;

    if (loading) {
      setRender(true);
      setShowAnimation(true);
    } else if (render) {
      setShowAnimation(false);

      timeoutAnimation = setTimeout(() => {
        setRender(false);
      }, time);
    }

    return () => {
      clearTimeout(timeoutAnimation);
    };
  }, [loading, render, time]);

  return { render, showAnimation };
};
```

```jsx
const AnimatedDiv = ({ loading, timeToShow }) => {
  const { render, showAnimation } = useAnimation(loading, timeToShow);

  return (
    <>
      {render && (
        <div
            style={`opacity: ${
              showAnimation ? '1' : '0'
            }; transition: opacity ${timeToShow}ms ease-in-out;`}
          >
            Animated div
          </div>
      )}
    </>
  );
};

ReactDOM.render(<AnimatedDiv />, document.getElementById('root'));
```
