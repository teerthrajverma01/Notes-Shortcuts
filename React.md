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
  **ASYNC PROMISES**  
  **ASYNC AWAIT**   
  **Working with components, props and jsx**
  **States, Events, and Forms Interactive Components**
 **Thinking in State Managment**
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
+ In JSX, `{cond ? <A /> : <B />}` means 'if cond, render `<A />`, otherwise `<B /\>`.  
+ In JSX, `{cond && <A />}` means 'if cond, render `\<A /\>`, otherwise nothing'.


#### Fragment  
`<Fragment>`, often used via `<>...</>` syntax, lets you group elements without a wrapper node.

___

### States, Events, and Forms Interactive Components  

#### Responding to Events:      
+ You can handle events by passing a function as a prop to an element like <button>.  
+ Event handlers must be passed, not called! `onClick={handleClick}`, not `onClick={handleClick()}`.  
+ You can define an event handler function separately or inline.  
+ Event handlers are defined inside a component, so they can access props.  
+ You can declare an event handler in a parent and pass it as a prop to a child.    
+ You can define your own event handler props with application-specific names.  
+ Events propagate upwards.  `Call e.stopPropagation()` on the first argument to prevent that.  
+ Events may have unwanted default browser behavior. Call `e.preventDefault()` to prevent that.  
+ Explicitly calling an event handler prop from a child handler is a good alternative to propagation.   

#### UseState Hook   
State is isolated and private.
**Updating Component State results into rerendering of component** 
The useState Hook provides those two things:    
+ A state variable to retain the data between renders.   
+ A state setter function to update the variable and trigger React to render the component again.
_Convention is to name this pair like const `[something, setSomething]`._
```javascript
import { useState } from 'react';//importing useState hook
// COMPONENT STARTS
const [index, setIndex] = useState(0);//hooks need to be called on top level of component
//here index is a state variable and setIndex is the setter function.
function handleClick() {
  setIndex(index + 1);//here we update state variable by using settler function on certain event
}
```

#### State as a snapshot(IMP)  
+ Setting state requests a new render.
+ React stores state outside of your component, as if on a shelf.
+ When you call useState, React gives you a snapshot of the state for that render.
+ Variables and event handlers don’t “survive” re-renders. Every render has its own event handlers.
+ Every render (and functions inside it) will always “see” the snapshot of the state that React gave to that render.
+ You can mentally substitute state in event handlers, similarly to how you think about the rendered JSX.
+ Event handlers created in the past have the state values from the render in which they were created.   
  
#### Queing a series of state update 
+ Setting state does not change the variable in the existing render, but it requests a new render.
+ React processes state updates after event handlers have finished running. This is called batching.
+ To update some state multiple times in one event, you can use `setNumber(n => n + 1)` updater function.

#### Updating object in state
+ Treat all state in React as immutable.
+ When you store objects in state, mutating them will not trigger renders and will change the state in previous render “snapshots”.
+ Instead of mutating an object, create a new version of it, and trigger a re-render by setting state to it.
+ You can use the `{...obj, something: 'newValue'}` object spread syntax to create copies of objects.
```javascript
setPerson({
  ...person, // Copy the old fields
  firstName: e.target.value // But override this one
});
```
+ Spread syntax is shallow: it only copies one level deep.
+ To update a nested object, you need to create copies all the way up from the place you’re updating.
+ To reduce repetitive copying code, use Immer.
```javascript
// Run npm install use-immer to add Immer as a dependency
// Then replace import { useState } from 'react' with import { useImmer } from 'use-immer'
```
#### Updating Arrays in State
+ You can put arrays into state, but you can’t change them.
+ Instead of mutating an array, create a new version of it, and update the state to it.
+ Types of Changes, For Detail `Refer Documentation`.
  - Adding to an Array
  - Removing from Array
  - Transforming an Array
  - Replacing items in an Array
  - Inserting into Array
  - Making other changes to Array
  - updating objects in Array 
+ You can use the `[...arr, newItem]` array spread syntax to create arrays with new items.
+ You can use filter() and map() to create new arrays with filtered or transformed items.
+ You can use Immer to keep your code concise.

#### Choosing State Structure
+ If two state variables always update together, consider merging them into one.
+ Choose your state variables carefully to avoid creating “impossible” states.
+ Structure your state in a way that reduces the chances that you’ll make a mistake updating it.
+ Avoid redundant and duplicate state so that you don’t need to keep it in sync.
+ Don’t put props into state unless you specifically want to prevent updates.
+ For UI patterns like selection, keep ID or index in state instead of the object itself.
+ If updating deeply nested state is complicated, try flattening it.

#### Sharing States between Components
+ When you want to coordinate two components, move their state to their common parent.
+ Then pass the information down through props from their common parent.
+ Finally, pass the event handlers down so that the children can change the parent’s state.
+ It’s useful to consider components as “controlled” (driven by props) or “uncontrolled” (driven by state).

#### Preserving and reseting states
+ React keeps state for as long as the same component is rendered at the same position.
+ State is not kept in JSX tags. It’s associated with the tree position in which you put that JSX.
+ Same Component at same position preserve state
+ Different Component at same postion reset state  
  
**Reseting State at same position** 
- option1:render a component with different position
- option2:reset state with a key

**Preserving state from removed component**   
_You could lift the state up and hold the pending message for each recipient in the parent component._ 
_This way, when the child components get removed, it doesn’t matter, because it’s the parent that keeps the important information._




















