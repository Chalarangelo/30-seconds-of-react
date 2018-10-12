### TypeScript React Compoent

To get started with React and Typescript you need to import the React module, for Typescript you have to import the whole React Library.

```tsx
import * as React from "react";
```

Next you define your Interface for the Props. Typescript requires that you define the types as well.

```tsx
interface IProps {
    greeting: string;
}
```

After you defined your interfaces you pass them as Type Arguments into the React.Component function call. The first Parameter is for the Props and the second for the State.
As soon as you passed in the Props you are able to display them.

```tsx
class TypescriptComponent extends React.Component<IProps, {}> {
  public render(): JSX.Element {
    return <div>{this.porps.greeting}</div>;
  }
}
```

Here you are looking for a html element with the id "demoTypescript" and rendering the React Component inplace of it.

```tsx
const htmlNode: HtmlElement = document.getElementById("demoTypescript");
if (htmlNode) {
    ReactDOM.render(<TypescriptComponent greeting="Hello 30 Seconds of Code" />, htmlNode);
}
```

<!-- tags: 0,1 -->

<!-- expertise: (0,1,2) -->
<!-- Expertise levels:
  0: beginner
  1: intermediate
  2: advanced
  3: expert
-->
