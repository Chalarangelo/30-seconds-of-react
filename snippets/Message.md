### Message

Renders a simple Message component.

This is a single instance component,you can import it and add it to your root element,then you can call it by `Message` class.This class contains 4 exposed methods: `success`、`info`、`warning` and `error`.Every method can show a message box related to it.

See live demo on [stackblitz.com](https://stackblitz.com/edit/message)

```css
@keyframes bounceIn {
  from {
    opacity: 0;
    transform: translate(-50%, 50px);
  }
  to {
    opacity: 1;
    transform: translate(-50%, 0);
  }
}
```

```jsx
const svgs = [
  <svg className="icon" viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg" width="16" height="16">
    <defs />
    <path d="M512 64.303538c-247.255337 0-447.696462 200.441125-447.696462 447.696462s200.441125 447.696462 447.696462 447.696462 447.696462-200.441125 447.696462-447.696462S759.255337 64.303538 512 64.303538zM512 804.948005c-35.32146 0-63.956637-28.635177-63.956637-63.956637 0-35.323507 28.635177-63.956637 63.956637-63.956637s63.956637 28.633131 63.956637 63.956637C575.956637 776.312828 547.32146 804.948005 512 804.948005zM575.956637 512c0 35.32146-28.635177 63.956637-63.956637 63.956637s-63.956637-28.635177-63.956637-63.956637l0-223.848231c0-35.323507 28.635177-63.956637 63.956637-63.956637s63.956637 28.633131 63.956637 63.956637L575.956637 512z"
    fill="#FAAD14" />
  </svg>,
  <svg className="icon" viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg" width="16" height="16">
      <defs />
      <path d="M512 1024a512 512 0 1 1 512-512 512 512 0 0 1-512 512z m258.304-674.816a50.112 50.112 0 0 0-71.104 1.664L469.376 592.896 317.12 449.984a50.112 50.112 0 0 0-71.104 2.432 50.752 50.752 0 0 0 2.432 71.488l188.672 177.088a50.112 50.112 0 0 0 70.4-2.048l264.128-278.144a50.752 50.752 0 0 0-1.344-71.616z"
      fill="#52C41A" />
  </svg>,
  <svg className="icon" viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg" width="16" height="16">
      <defs />
      <path d="M512 512m-448 0a448 448 0 1 0 896 0 448 448 0 1 0-896 0Z" fill="#2196F3"
      />
      <path d="M469.333333 469.333333h85.333334v234.666667h-85.333334z" fill="#FFF"
      />
      <path d="M512 352m-53.333333 0a53.333333 53.333333 0 1 0 106.666666 0 53.333333 53.333333 0 1 0-106.666666 0Z"
      fill="#FFF" />
  </svg>,
  <svg className='icon' viewBox='0 0 1024 1024' xmlns='http://www.w3.org/2000/svg' width='16' height='16'>
    <defs />
    <path d='M511.631 510.91m-445.605 0a445.605 445.605 0 1 0 891.21 0 445.605 445.605 0 1 0-891.21 0Z'
    fill='#EF6160' />
    <path d='M661.493 376.267a9.97 9.97 0 0 0-2.929-7.071c-3.906-3.905-10.236-3.905-14.143 0L510.188 503.429 381.042 369.33c-3.831-3.98-10.163-4.098-14.139-0.266a9.965 9.965 0 0 0-3.063 7.209 9.966 9.966 0 0 0 2.797 6.93l129.406 134.37-129.274 129.276c-1.952 1.953-2.929 4.512-2.929 7.071s0.977 5.118 2.929 7.071c1.953 1.952 4.512 2.929 7.071 2.929s5.119-0.977 7.071-2.929L509.92 531.982l124.225 128.99a9.972 9.972 0 0 0 7.204 3.063 9.97 9.97 0 0 0 6.936-2.797 9.973 9.973 0 0 0 3.063-7.21 9.97 9.97 0 0 0-2.797-6.93l-124.487-129.26 134.5-134.5a9.968 9.968 0 0 0 2.929-7.071z'
    fill='#FFF' />
  </svg>
]

class Message extends React.Component {
  constructor() {
    super();
    this.state = {
      text: '',
      visible: false,
      timer: null,
      ico: ''
    };
    this.changeStyle = this.changeStyle.bind(this);
    Message.warning = this.warning.bind(this);
    Message.success = this.success.bind(this);
    Message.info = this.info.bind(this);
    Message.error = this.error.bind(this);
  }
  render() {
    return this.state.visible ? <div style={commonStyle}>
      { svgs[this.state.ico] }
      <span>
        { this.state.text }
      </span>
    </div> :null
  }
  warning(text) {
    this.changeStyle(text, 0);
  }
  success(text) {
    this.changeStyle(text, 1);
  }
  info(text) {
    this.changeStyle(text, 2);
  }
  error(text) {
    this.changeStyle(text, 3);
  }
  changeStyle(text, ico) {
    this.setState({
      text,
      visible: false,
      ico
    }, () => {
      window.clearTimeout(this.state.timer);
      let timer = window.setTimeout(() => {
        this.setState({
          visible: false
        });
      }, 2000);
      this.setState({
        timer,
        visible: true
      });
    });
  }
}
```

```jsx
// add to render function
<Message/>

Message.warning('warning!');
Message.success('success!');
Message.error('error!');
Message.info('info!');
```

<!-- tags: class, animation, single instance, event loop -->

<!-- expertise: 1 -->
