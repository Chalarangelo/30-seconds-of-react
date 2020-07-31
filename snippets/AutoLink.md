---
title: AutoLink
tags: components,string,fragment,regexp,advanced
---

Renders a string as plaintext, with URLs converted to appropriate `<a>` elements.

- Use `String.prototype.split()` and `String.prototype.match()` with a regular expression to find URLs in a string.
- Return a `<React.Fragment>` with matched URLs rendered as `<a>` elements, dealing with missing protocol prefixes if necessary, and the rest of the string rendered as plaintext.

```jsx
function AutoLink({ text }) {
  const delimiter = /(^|[\s\n]|<[A-Za-z]*\/?>)((?:https?|ftp):\/\/[\-A-Z0-9+@#\/%?=()~_|!:,.;]*[\-A-Z0-9+@#\/%=~()_|])/gi;

  return (
    <React.Fragment>
      {text.split(delimiter).map(word => {
        let match = word.match(delimiter);
        if (match) {
          let url = match[0];
          return <a href={url.startsWith('http') ? url : `http://${url}`}>{url}</a>;
        }
        return word;
      })}
    </React.Fragment>
  );
}
```

```jsx
ReactDOM.render(
  <AutoLink text="foo bar baz http://example.org bar" />,
  document.getElementById('root')
);
```
