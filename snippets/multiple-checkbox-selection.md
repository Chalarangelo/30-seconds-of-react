### Multiple Checkbox Selection

 The following code shows you how to collect ID of elements you have
 selected in a list so that you can submit it to a server or process
 in your app.


```

import React from "react";

class App extends React.Component {
  state = {
    info: {
      facilities: [2]
    },
    facilities: [{ id: 1, active: false }, { id: 2, active: true }]
  };

  toggle = id => {
    let activeFacilities = [];
    let facilities = this.state.facilities.map(item => {
      if (item.id === id) {
        /**
         * we will use !item.active here, because we're about to flip the
         * value to the current opposite
         */
        if (!item.active) activeFacilities.push(item.id);
        return { ...item, active: !item.active };
      }
      if (item.active) activeFacilities.push(item.id);
      return item;
    });
    this.setState({
      facilities: facilities,
      info: {
        facilities: activeFacilities
      }
    });
  };

  render() {
    return (
      <div>
        {this.state.facilities.map(facility => (
          <div key={facility.id}>
            {facility.id} -
            <input
              type="checkbox"
              checked={facility.active}
              onChange={e => this.toggle(facility.id)}
            />
            <span onClick={() => this.toggle(facility.id)}>toggle</span>
          </div>
        ))}
        <p>To submit: {this.state.info.facilities.join(", ")}</p>
      </div>
    );
  }
}

export default App;

```
