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

Creating a test...  

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
After run the tests they will fail.    

Then create the component...  
```typescript jsx
import React, { Component } from 'react';
class Header extends Component {
  render() {
    return (
      <div className='Header'>
        this is the header
      </div>
    );
  }
}
export default Header;
```
and tests should pass now.

## React components

##### Container 
- Hold other components.
- Handle any logic in the application
- Changes t the application state

##### Component
- Also known as a stateful component or smart component

##### Stateless component
- Exists solely to produce a piece of the user interface
- Also known as dumb component  



**Separate Containers from Components   
Create __tests__ by default looked for Jest**

## Software testing

##### Unit testing 
- Testing of a single isolated piece of code or group of pieces.  
- unit testing tests whether component produces an expected output when given input.
##### Integration testing
- Groups of components are testing together along with hardware
##### Performance testing
- Looks at the speed of testing
##### Usability testing
- Tests the product from the perspective of the customer
- How easy it is to use and how pleasing it is
##### Acceptance testing
- Tests whether a product meets the requirements of the customer
##### Regresion testing
- Tests wheter a modification is working correctly
- Wheter anything broke as a result of a modification

### Testing framework
Software used to automate the running of tests.  
- Jasmine
- Mocha
- Jest
- QUnit

### Testing concepts

#### Suite
Set of tests for a particular unit
#### Spec
Single test within a suite of tests
#### Assertion
Boolean expression that will be true unless there is a bug in the program   
Many of them produce a spec  
#### Matcher
Method that produce true or false values
They are used inside assertions
#### Test runner
Used to run automated tests

**Software testing requires at least 2 different things**
1. Test automation functionality
2. Test assertion functionality

Frameworks that got both: Jasmine and Jest.  

Mocha allows you to use any assertion library, such as...  
Chai, Should(js), Assert.js

## TDD cycle
1. Test
2. Code 
3. Refactor  

**Repeat**

Think about your application components 


1. Think
1. Create simple test in order to fail
2. Create some code to make the test pass
3. See if there ways to improve the either one.  
**Do not write new tests or add functionality, no matter how**  
If you find out something new, add this to a to-do list, for another iteration of the TDD cycle.  

 