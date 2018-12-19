### Progress Bar

#### What is this component?
This is a Progress Bar component that shows the progression of an operation to the end-user.

#### How does this component work?
This component assumes that the percentage is a non-decimal percentage (0-100), and uses that value to set the width of an internal div based on that prop.

```css
/* Progress.css */

/* Animation for stripes */
@keyframes stripes-animation {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}

/* Progress Bar styles */
.progress {
    background: red;
    height: 100%;
    border-radius: inherit;
    transition: width .2s ease-in;
    background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
    background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
    background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
    animation: stripes-animation 2s linear infinite;
}

/* Container styles */
.container {
    position: relative;
    height: 10px;
    width: 400px;
    background: gray;
}
```

```jsx
import "path/to/Progress.css";

const Progress = ({percentage}) => (
    <div className="container">
        <div style={{width: `${percentage}%`}} className="progress"></div>
    </div>
);
```

```jsx
ReactDOM.render(<Progress percentage={20}/>, mountNode);
```

<!-- OPTIONAL -->
#### Notes:
* This component assumes the percentage being entered is between 0 - 100. It is upto the parent component computing these percentage to pass them in that range. This component is just to display the percentage.
* This component relies heavily on CSS. You can always change the look and animation of this component by changing the CSS File.

<!-- tags: (separate each by a comma) -->

<!-- expertise: (0,1,2,3) -->
<!-- Expertise levels (pick only one, no parentheses):
  0: beginner
  1: intermediate
  2: advanced
  3: expert
-->