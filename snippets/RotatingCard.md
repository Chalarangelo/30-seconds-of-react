---
title: RotatingCard
tags: components,dumb
---

Renders a two side card which gives a rotation effect upon hover and switches sides.

- Define some appropriate CSS styles and an animation for the rotating effect.
- Create two `<div>` elements inside the card for both the sides of the card.
- Use the `:hover` event to `rotate` and `transform` the card sides.

```css
  .card {
    perspective: 150rem;
    -moz-perspective: 150rem;
    position: relative;
    height: 40rem;
    max-width: 400px;
    margin: 2rem
  }
  .card__side {
    height: 35rem;
    border-radius: 15px;
    transition: all 0.8s ease;
    backface-visibility: hidden;
    position: absolute;
    top: 0;
    left: 0;
    width: 80%; 
    padding:2rem;
    color: white
  }
  .card__side--back {
      transform: rotateY(-180deg);
      background-color: #4158D0;
      background-image: linear-gradient(43deg, #4158D0 0%,#C850C0 46%, #FFCC70 100%);
  }
  .card__side--front {
      background-color: #0093E9;
      background-image: linear-gradient(160deg, #0093E9 0%, #80D0C7 100%);
  }
  .card:hover .card__side--front {
    transform: rotateY(180deg); 
  }
  .card:hover .card__side--back {
    transform: rotateY(0deg); 
  }

```

```jsx
const RotatingCard = ()=>{
  return(
    <div className="card">
      <div className="card__side card__side--front">
          <div className="card__side--front--mask">
              Front Side
          </div>        
      </div>
      <div className="card__side card__side--back">
          <div className="card__side--back--mask">
              Back Side
          </div>           
      </div>
    </div>
  )  
};
```

```jsx
ReactDOM.render(<RotatingCard />,
document.getElementById("root"));
```
