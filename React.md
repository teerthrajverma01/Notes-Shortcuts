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
We can enter JavaSsript mode by using `{ //javascript code }` 

#### Props
Props are used to pass data from parent componet to child component   
Anything can be passed through props: values,arrays,objects,functions,components  
Nested JSX like `<Card><Avatar /></Card>` will appear in Card component’s.youc can access using `props.children` prop.
**Props are read only ie immutable**   
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
function Avatar({ person, size }){
  // use data by means of person and size are available here
}
//OR
function Avatar({ ..props }){
  
}
//OR
function Avatar(props) {
  //use data by means of props.person , props.size
}
```
#### Rendering List   
**Steps:**  
+ Move the data into an array   
+ Map the people members into a new array of JSX nodes, listItems    
+ Return listItems from your component wrapped in a `\<ul\>`
   
`Note: Each child in a list should have a unique 'key' prop.`  
```javascript
const people = [{
  id: 0,
  name: 'Creola Katherine Johnson',
  profession: 'mathematician',
}, {
  id: 1,
  name: 'Mario José Molina-Pasquel Henríquez',
  profession: 'chemist',
}, {
  id: 2,
  name: 'Mohammad Abdus Salam',
  profession: 'physicist',
}, {
  name: 'Percy Lavon Julian',
  profession: 'chemist',  
}, {
  name: 'Subrahmanyan Chandrasekhar',
  profession: 'astrophysicist',
}];

export default function List() {
  const listItems = people.map(person =>
    <li key={person.id}>{person.name : {person.profession} </li>
  );
  return <ul>{listItems}</ul>;
}
```

#### Conditional Rendering:
+ You can return a JSX expression conditionally with an if statement ie having multiple returns.  
+ You can conditionally save some JSX to a variable and then include it inside other JSX by using the curly braces.  
+ In JSX, `{cond ? <A /> : <B />}` means “if cond, render <A />, otherwise <B />”.  
+ In JSX, `{cond && <A />}` means “if cond, render <A />, otherwise nothing”.


#### Fragment
`<Fragment>`, often used via `<>...</>` syntax, lets you group elements without a wrapper node.









