# JavaScript

### … Operator 

Means all items in the object, all items in an array, all properties of an object

tasks = [task1, task2, task3];

### Add a new task without pushing:
tasks = […tasks, task4]                                …tasks means all items of the array, then add task4

### Update a single value of a single array item:
tasks = tasks.map( (task) => task.id === id 
    ? { …task, reminder : !task.reminder }        …task means copy all fields and change reminder
    :  task  

### Working with JavaScript and CSS

- [JavaScript Basics](https://academind.com/learn/javascript){:target="_blank"}
- [JavaScript CSS Styles](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style){:target="_blank"}
- [ELEMENT.classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList){:target="_blank"}

JavaScript can be used to update actual element styles, but it is better to create classes to add/remove from the elements.

Element Examples
```
button.style.backgroundImage = 'image.png';    
button.style['background-image'] = 'image.png';
button.classList.add('className');
button.classList.remove('className');
```
