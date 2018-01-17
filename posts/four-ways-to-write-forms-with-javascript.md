# Four Ways to Write Forms with Javascript

## FormData

```html
<form id="example" name="example">
  <fieldset>
    <label for="username">Enter name:</label>
    <input type="text" id="username" name="username">
  </fieldset>
  <fieldset>
    <label for="email">Enter email address:</label>
    <input type="email" id="email" name="email">
  </fieldset>
  <fieldset>
    <label for="image">Upload profile image:</label>
    <input type="file" id="image" name="image" multiple="false">
  </fieldset>
  <input type="submit" value="Submit!">
</form>
```

```js
var exampleForm = document.getElementById('example');
var formData = new FormData(exampleForm);

fetch('/example', {
  method: 'POST',
  body: formData,
});
```

Read more about [FormData Objects](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects)

## React

At Domain we use React

### With Uncontrolled Components

```js
class ExampleForm extends React.Component {
  constructor(props) {
    super(props);

    this.setRef = this.setRef.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  
  setRef(ref) {
    this[ref.name] = ref;
  }
  
  handleSubmit(event) {
    event.preventDefault();
    
    var formData = new FormData();
    formData.append('username', this.username.value);
    formData.append('email', this.email.value);
    formData.append('image', this.image.files[0]);
    
    fetch('/example', {
      method: 'POST',
      body: formData,
    });
  }
  
  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <fieldset>
          <label for="username">Enter name:</label>
          <input type="text" id="username" name="username" ref={this.setRef} />
        </fieldset>
        <fieldset>
          <label for="email">Enter email address:</label>
          <input type="email" id="email" name="email" ref={this.setRef} />
        </fieldset>
        <fieldset>
          <label for="image">Upload profile image:</label>
          <input type="file" id="image" name="image" multiple={false} ref={this.setRef} />
        </fieldset>
        <input type="submit" value="Submit!" />
      </form>
    );
  }
}
```

Read more about [Uncontrolled Components](https://facebook.github.io/react/docs/uncontrolled-components.html)

### With Controlled Components

```js
class ExampleForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      username: '',
      email: '',
    }
    this.handleChange = this.handleChange.bind(this);
    this.handleFile = this.handleFile.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  
  handleFile(input) {
    return (event) => {
      this.setState({
        [input]: event.target.files[0],
      });
    };
  }
  
  handleChange(input) {
    return (event) => {
      this.setState({
        [input]: event.target.value,
      });
    };
  }
  
  handleSubmit(event) {
    event.preventDefault();
    
    var formData = new FormData();
    formData.append('username', this.state.username);
    formData.append('email', this.state.email);
    formData.append('image', this.state.image);
    
    fetch('/example', {
      method: 'POST',
      body: formData,
    });
  }
  
  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <fieldset>
          <label for="username">Enter name:</label>
          <input type="text" id="username" name="username" onChange={this.handleChange('username')} />
        </fieldset>
        <fieldset>
          <label for="email">Enter email address:</label>
          <input type="email" id="email" name="email" onChange={this.handleChange('email')} />
        </fieldset>
        <fieldset>
          <label for="image">Upload profile image:</label>
          <input type="file" id="image" name="image" multiple={false} onChange={this.handleFile('image')} />
        </fieldset>
        <input type="submit" value="Submit!" />
      </form>
    );
  }
}
```

Read more about [Controlled Components](https://facebook.github.io/react/docs/forms.html)

## React with `react-reformed`

