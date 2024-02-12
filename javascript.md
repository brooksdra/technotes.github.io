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
