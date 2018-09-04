# React - TDD

##### React
A javascript library for building user interfaces

## Create react app

```
npm install -g create-react-app
create-react-app "project-name"
npm start       // run app
npm test        // run tests
```

## First component

```typescript jsx
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
//import registerServiceWorker from './registerServiceWorker';

ReactDOM.render(<App />, document.getElementById('root'));
//registerServiceWorker();
```

- React  
Helps to create components
- ReactDOM  
Handles the interaction between components and web browser


### To create a React Component

```typescript jsx
class App extends Component {
  render() {
    return (
      <div className="App">
        ...
      </div>
    );
  }
}
```
JSX code.  
All components should have a render method.  
What is inside render is then compiled to javascript.  
Then javascript is used to generate HTML to ultimate render  
Code inside jsx allows to use js inside between "{}".  

##### First create the test
```typescript jsx
import React from 'react';
import ReactDOM from 'react-dom';
import Header from './Header';

it('renders without crashing', () => {
  const div = document.createElement('div');
  ReactDOM.render(<Header />, div);
  ReactDOM.unmountComponentAtNode(div);
});
```
after run the tests and fail 
### Create Header component
```typescript jsx
import React, { Component } from 'react';
import './App.css';
class App extends Component {
  render() {
    return (
      <div className='Header'> 
        this is the header1
      </div>
    );
  }
}
export default App;
```
and tests should pass now.


##### Container 
- Hold other components.
- Handle any logic in the application
- Changes t the application state

##### Component
- Also known as a stateful component or smart component

##### Stateless component
- Exists solely to produce a piece of the user interface
- Also known as dumb component  

### Refactoring 

Separate Containers from Components
Create __tests__ by default looked for Jest