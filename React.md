### `REACT is a LIBRARY`  (view only )   
React is declarative, component-based, state-driven javascript library for building user interfaces   
Components are building blocks of userinterface    
Declarative means telling react what component should look like based on current state by means of jsx syntax   
React is Abstraction away from DOM  instead, it is UI as reflection of current states    

Two options to create react project:    
+ `CREATE-REACT-APP` -> starter-kit, preconfigured ,slow and outdated, not used for real-world project    
+ `VITE` -> modern build tools with template , need to setup eslint and ..., used for modern app, extreme fast   

```
Topics:
  ASYNC PROMISES   
  ASYNC AWAIT   
  Working with components, props and jsx
```

```javascript 
//INDEX.JS->(starter file)
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import './index.css';

const root =ReactDOM.createRoot(document.getElementById("root"));
root.render(<React.StrictMode><App/></React.StrictMode>);
```



### Working with components, props and jsx

#### COMPONENTS
React applications are entirely made of components   
component made of -> data, logic, appearance  
components can be reusable   
Component tree -> how components are nested inside each other and their relation with each other  

```javascript
//writing a component function
const Comp1=()=>{
//logic+state 
  return (JSX);
}

 //calling a component
<Comp1/>   
```
Each component can return exactly one jsx element   

#### JSX
JSX is all about component's appearance  
Each JSX element is converted into `React.createElement`  

### Props
Props are used to pass data from parent componet to child component   
Anything can be passed through props: values,arrays,objects,functions,components
**Steps**: 
+ Pass props to the child component 
```javascript
export default function Profile() {
  return (
    <Avatar
      person={{ name: 'Lin Lanying', imageId: '1bX5QH6' }}
      size={100}
    />
  );
}
```
+ Read props inside the child component
```javascript
function Avatar({ person, size }) {
  // use data by means of person and size are available here
}
//OR
function Avatar(props) {
  //use data by means of props.person , props.size
}
```
