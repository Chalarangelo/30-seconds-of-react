---
title: Carousel
tags: components,children,state,effect,intermediate
---

Renders a carousel component.

- Use the `React.useState()` hook to create the `active` state variable and give it a value of `0` (index of the first item).
- Use an object, `style`, to hold the styles for the individual components.
- Use the `React.useEffect()` hook to update the value of `active` to the index of the next item, using `setTimeout`.
- Destructure `props`, compute if visibility style should be set to `visible` or not for each carousel item while mapping over and applying the combined style to the carousel item component accordingly.
- Render the carousel items using `React.cloneElement()` and pass down rest `props` along with the computed styles.

```jsx
const Carousel = ({ carouselItems, mouseControl = false , ...rest }) => {
  const [active, setActive] = React.useState(0);
  const [control, setControl] = React.useState(false);
  let scrollInterval = null;
  const style = {
    carousel: {
      position: 'relative'
    },
    carouselItem: {
      position: 'absolute',
      visibility: 'hidden'
    },
    visible: {
      visibility: 'visible'
    }
  };
  React.useEffect(() => {
    if(!control){
      scrollInterval = setTimeout(() => {
        setActive((active + 1) % carouselItems.length);
      }, 2000);
    } else {
      clearTimeout(scrollInterval)
    }
    return () => clearTimeout(scrollInterval);
  });

  return (
    <div
      style={style.carousel}
      onMouseEnter={e => mouseControl && setControl(true)}
      onMouseLeave={e => mouseControl && setControl(false)}
      >
      {carouselItems.map((item, index) => {
        const activeStyle = active === index ? style.visible : {};
        return React.cloneElement(item, {
          ...rest,
          style: {
            ...style.carouselItem,
            ...activeStyle
          }
        });
      })}
    </div>
  );
};
```

```jsx
ReactDOM.render(
  <Carousel
    carouselItems={[
      <div>carousel item 1</div>,
      <div>carousel item 2</div>,
      <div>carousel item 3</div>
    ]}
  />,
  document.getElementById('root')
);
```
