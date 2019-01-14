### Tab

Renders a tab component.

Use the `onClick` function in the `<ul>` element, to obtain the `<li>` element that was pressed and also information of each one.
The `onClick` event executes a function called `handleTabChange` and it receives an `e` parameter by default, which contains data of the pressed element and an array of all child elements `<ul>`.
To iterate the children of `<ul>` we use `Array.from()` and thus compare the dataset of each child `<li>` and remove the attribute `className`, except the selected.

```css
  .tabs {
    list-style: none;
    padding-left: 0;
    display: flex;
  }

  .tabs > li {
    cursor: pointer;
    padding: 8px 16px;
  }

  .tabs > li.focus {
    border-bottom: 2px solid #007BEF;
  }

  .tabs > li:hover {
    border-bottom: 2px solid #007BEF;
  }
```

```jsx
class Tabs extends React.Component {
  handleTabChange = e => {
    const {
      currentTarget,
      target: {
        dataset: { tab }
      }
    } = e;

    Array.from(currentTarget.children).forEach(item => {
      if (tab === item.dataset.tab) {
        return (item.className = 'focus');
      }

      item.className = '';
    });
  };

  render() {
    return (
      <ul onClick={this.handleTabChange} className="tabs">
        <li data-tab="0" className="focus">
          Tab One
        </li>
        <li data-tab="1">Tab Two</li>
        <li data-tab="2">Tab Three</li>
      </ul>
    );
  }
}
```

```jsx
ReactDOM.render(<Tabs />, document.getElementById('root'));
```