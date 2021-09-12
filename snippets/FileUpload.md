---
title: FileUpload
tags: components,state,beginner
firstSeen: 2021-09-11T20:35:37+03:00
---

Renders a FileUpload component.

- Use the `allowMultiple` prop to handle the `multiple` attibute value by default its `false`.
- Render an `<input type="file">` and bind its `onChange` event to handle the `files`, applying the appropriate `className` to the wrapping `<label>`.

```css
.fileUploadContainer {
  margin: 20px;
  text-align: center;
}
.fileUploadLabel {
  border: 2px solid#1890ff;
  color: #1890ff;
  background-color: white;
  padding: 8px 20px;
  border-radius: 8px;
  font-size: 20px;
  font-weight: bold;
}
.fileTypeInput {
  position: absolute;
  left: 0;
  top: 0;
  opacity: 0;
}
```

```jsx
function FileUpload(props) {
  const { allowMultiple = false } = props;
  const fileInput = useRef(null);
  const handleFileChange = (event) => {
    console.log(event.target.files);
    alert("Selected file " + JSON.stringify(fileInput.current.files[0]?.name));
  };
  return (
    <div className="fileUploadContainer">
      <label className="fileUploadLabel">
        Upload a file
        <input
          className="fileTypeInput"
          type="file"
          ref={fileInput}
          onChange={handleFileChange}
          multiple={allowMultiple}
        />
      </label>
    </div>
  );
}
```

```jsx
ReactDOM.render(<FileUpload />, document.getElementById("root"));
```
