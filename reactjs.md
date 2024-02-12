# REACT JS and NEXT JS

### JSX - Dynamic markup Java syntax extension
JSX must have a single parent element, if multiple tags are required wrap in a `<> </>` fragment
Wrap tags in single curly braces to logically show or hide.   { showThisTag && <ThisTag>  }

### Virtual DOM, Data Binding
Array forEach() map
Promises

### React-Router-Dom. Browser Router as Router, Route
`<Route path='/about' component={About} />`  
For 'A' tags, use Link  
`<a href='/'>Go Back</a>`  becomes  
`<Link to='/'>Go Back</Link>`

React is based on Functions "Components" could be classes, but functions are preferred.
With functions, we need state, React looks at useState(), useEffect(), useReducer, etc…
Functions can be passed in as props

Components pass in props in method functions
Use proptypes to set types of each props
Style {{ }} for literals and { } for variables

### useState React Hook
Only used in a function NOT in a class.
Hooks must execute in the same order "Strange" not inside if's etc.

When changing a value based on it current value, use function style
Const [ count, setCount ] = useState(4);
```
Function decrementCount() {
   setCount( prevCount => prevCount - 1);     and not     setCount( count - 1 );
}
```

**Important Note:** useState(4) gets run with every render. To avoid this pass in a function as useState( () => { return 4 } )
In this case, the method only get run the first render.

const [thisState, setThisState] = useState(default value);  return names are yours
To set state call setThisState(new value), to access see thisState.
Important: the entire state is immutable, recreate the entire state and set again.
You cannot push a new item into a state array.
For example:
```
const [tasks, setTasks] = useState( [task1, task2])
To add task3, setTasks( […tasks, task3])
To remove task2, setTasks( tasks.filter( (task) => task.id !== task2.id ) );
Change a task value 
setTasks( tasks.map( (task) => task.id === id 
    ? { …task, reminder : !task.reminder }                …task means copy all fields and change reminder
    :  task                                                                        copy the task without changing anything
```

useEffect React Hook
Only works in functions, NOT in a class.
  to do things when the pages loads, whenever a specific state object changes, or when the page is destroyed.

```
useEffect ( () => {
    console.log('render');
    return () => {
         console.log( 'cleanup');
    }
}, [ **] )
```

** Add one or more states in the array and the effect will run when that state changes. An empty array will only run the first render. 
Add a return method that runs when the component is destroyed.

useContext React Hook
Use the "Context API" of Redux to store global state or just put it in the top component. (_app.js) and pass it down as props.


# NEXT JS
Next Environment Variables:
They are for the backend primarily, not the frontend, everything in pages/api has access to the env vars and are hidden from the browser.

Settings with a NEXT_PUBLIC_ prefix are visible to the browser.
Environment variables can be read from multiple files, first setting wins
Order:
npm start:           .env.development.local > .env.development > .env.local > .env
Npm run build:       .env.production.local > .env.production > > .env
npm test.            .env.test.local > .env.test > > .env
