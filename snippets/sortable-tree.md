### Sortable Tree Example


```

import React, { Component } from "react";
import SortableTree from "react-sortable-tree";

const maxDepth = 5;

const renderDepthTitle = ({ path }) => `Depth: ${path.length}`;

const treeData = [
  {
    expanded: true,
    title: "Any node can be the parent or child of any other node",
    children: [
      {
        expanded: true,
        title: "Chicken",
        children: [{ title: "Egg" }]
      }
    ]
  },
  {
    title: "Button(s) can be added to the node",
    subtitle:
      "Node info is passed when generating so you can use it in your onClick handler"
  },
];

class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      treeData
    };
  }

  render() {
    console.log("treeData", this.state.treeData);
    return (
      <div style={{ height: 500 }}>
        <SortableTree
          treeData={this.state.treeData}
          onChange={treeData => this.setState({ treeData })}
        />
      </div>
    );
  }
}

export default App;

```
