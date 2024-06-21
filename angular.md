# Angular

- [Angular CLI](https://angular.dev/tools/cli/){:target="_blank"}
- [Interesting Property vs. Attribute Article](https://jakearchibald.com/2024/attributes-vs-properties/){:target="_blank"}

## How To

### Install a global version of angular
``` 
sudo npm install -g @angular/cli
ng new angular-2024-app
cd angular-2024-app
npm install
npm start
```
### Generate a new component
```
ng generate component header    // Longhand
ng g c header                   // Shorthand
ng g c task --skip-tests        // Shorthand but skip generating the unit test.
```

## Components

### Signal
A signal is an angular value type object that angular monitors when it changes inorder to better push updates to the UI.

The original and still available Change Detection Mechanism is based on Zones. Zones notify angular about user events, 
expired timers etc. When angular gets the notification, it checks the zone for necessary UI updates. 

With signals, Angular knows exactly what to change for any specific value change.  

The ```computed``` function provides a way for Angular to set up a subscription to watch the signal buried in code.  
So, in this case, whenever selectedUser is set, imagePath will also be recomputed and signaled as a change.

``` 
    selectedUser = signal(initialValue);
    imagePath = computed( () => '/assets/users/' + this.selectedUser().avatar );
    
    this.selectedUser.set(updatedValue);
```
To access a signals value in the template, you must call it as a method, then access the variables. This call to the method is what
angular uses to set up appropriate listeners so the values can be updated asap. Notice the () after each signal or computed usage.
```
<img [src]="imagePath()" alt="selectedUser().name" />
<span>The User is {{ selectedUser().name }}</span>
```

### @Input and input()
@Input describes values coming in from the template page.  
Notice the avatar!, the '!' indicates there will be a value provided sometime. Needed because of the {required: true}  

There is a more modern input() method, similar to computed, returns an input from the template and wraps it into a signal.  
To avoid the '!' effect, provide a generic <string>, so TypeScript knows what will be held by this variable.

This is the parent component code:
```
@Input() avatar?: string;                   // The standard old way with a possible undefind value.
@Input() avatar: string | undefined;        // The union operator is equivilant.
@Input({required: true}) avatar!: string;   // Add {required: true} to eliminate the undefined, and ! because we didn't intialize it here
... OR ...
avatar = input<string>();                   // Generate a signal using the input()...            
avatar = input.required<string>();          // Make it required
```

// Child component coded in the parent HTML
```
<app-user [avatar]="users[2].avatar" />     // Passing a value from the parent the child component tag attribute and its .ts.
```

### @Output and output()
@Output decorates values sent from a child component back up to the parent component.
There is a more modern output() method which works exactly like the @Output, 

This is the child component:
```
@Output select = new EventEmitter<string>();
OR
select = output<string>();

onSelect(id: string) {
    this.select.emit(id);
}
```

Child component coded in the parent HTML.  
The $event variable is build in.
```
<app-user [avatar]="users[2].avatar (select)=onselectedUser($event)"/>     // Passing a value from the HTML to .ts.
```

// Parent component acting on the emitted select event (the id is emitted above):
``` 
onSelectedUser(id) {
    console.log("selected id = " + id);
}    
```

### Type vs. Interface
- [Detailed Explanation](https://stackoverflow.com/questions/37233735/interfaces-vs-types-in-typescript/52682220#52682220){:target="_blank"}
- [Another](https://medium.com/@martin_hotell/interface-vs-type-alias-in-typescript-2-7-2a8f1777af4c){:target="_blank"}
```
type User = {
    id: string,
    avatar: string,
    name: string
}
OR
interface User {
    id: string,
    avatar: string,
    name: string
}
```
### Control Flow (Pre Angular 17)
- [Control Flow](https://v16.angular.io/api/common/NgFor#description){:target="_blank"}

Structural Directives *ngFor and *ngIf and must be imported into the .ts file.
``` 
<main>
    <ul id+"users">
        <li *ngFor="let user of users" >
            <app-user [user]="user" (select)=onselectedUser($event)"/>
        </li>   
    </ul>

    @if (selectedUser) {
        <app-tasks [name]="selectedUser.name" />
    } @else {
        <p id="fallback">Select a user to see there tasks!</p>
    }
</main>
```


### Template Control Flow (New for Angular 17)
- [New Template Control Flow](https://angular.dev/guide/templates/control-flow){:target="_blank"}

The @for and @if are not directives, they are part of template feature, therefore, they do not need to be imported.
@for requires a track item.id inorder to know how to track the items and more efficiently update lists without a complete rewrite.
```
<main>
    <ul id+"users">
        @for (user of users; track user.id) {
            <li>
                <app-user [user]="user" (select)=onselectedUser($event)"/>
            </li>   
        }
    </ul>
                                                           NOTICE the v!v below, because angular doesn't know about the directive
    <app-tasks *ngIf="selectedUser; else fallback" [name]="selectedUser!.name" />
    <ng-template #fallback>
        <p id="fallback">Select a user to see there tasks!</p>
    </ng-template>
</main>
```

## @NgModule

- [Module Introduction](https://www.udemy.com/course/the-complete-guide-to-angular-2/learn/lecture/43797772#learning-tools){:target="_blank"}
This is the old way of building applications without standalone components. If you don't have to do it that way, don't. 
If you find yourself needing to integrate with existing NgModules, review this chapter for more information.

## Template Content Tricks

### <ng-content>
ng-content is the way to supply elements in the body of the control element being used in a new page.
You can only have one ng-content tag within the component template so Angular knows where to put the body.

The component looks like this:
``` 
HTML:
<div class="dashboard-item">
    <article>
        <header>
            <img [src]="image.src" [alt]="image.alt" />
            <h2>{{ title }}</h2>
        </header>
    </article>
    <ng-content/>                <=== This is where the body of the parent tag will be inserted
</div>

ts: with standared input binding
export class DashboardItemComponent {
  @Input({required: true}) image! : { src:string, alt:string };
  @Input({required: true}) title! : string;
}

```
When binding an attribute, the square brackets [src]= binds the value to the ts @Input field. 

Usage looks like this:
```
<main>
  <div id="dashboard">
    <app-dashboard-item [image]="{ src:'status.png', alt:'A signal symbol'}" title="Server Status" >
        <app-server-status/>     <=== ng-content inserted here
    </app-dashboard-item>
    <app-dashboard-item [image]="{ src:'globe.png', alt:'A globe'}" title="Traffic" >
        <app-traffic/>           <=== ng-content inserted here
    </app-dashboard-item>
    <app-dashboard-item [image]="{ src:'list.png', alt:'A list of items'}" title="Server Tickets" >
        <app-support-tickets/>   <=== ng-content inserted here
    </app-dashboard-item>
  </div>
</main>
```
Also Note: when binding attribute into the component the square brackets have a slightly different meaning:
[image]="{ src:'status.png', alt:'A signal symbol'}"   In this case, image is a dynamic or calculated value,
title="Server Status"                                  and title is a string; which is the handled more commonly.
[title]="'Server Status'"                              So, using square brackets, would need to look like this.

#### Extending built-in components for a leaner DOM
In this example, we wanted to build a re-usable button component like so...
button.component.html
``` 
<button>
    <span>
    Logout
    </span>
    <span class="icon">
    →
    </span>
</button>

Template Usage:
<li>
    <app-button>
</li>
```
DOM Output works just find, but looks like this, which has an extra layer of HTML...
``` 
<app-button>
    <button>
        <span>
        Logout
        </span>
        <span class="icon">
        →
        </span>
    </button>
</app-button>
```
To keep the built-in button components capabilities while creating a custom component:
- Remove the wrapping <button> element from your template.
- [Use a different component selector in the .ts.](https://angular.dev/guide/components/selectors){:target="_blank"}

In this case .ts uses what is called an attribute selector:
```
HTML:
<span>
    Logout
</span>
<span class="icon">
    →
</span>

Component: 
@Component({
  selector: 'app-button',
  standalone: true,
  
becomes:
@Component({
  selector: 'button[appButton]',      <== If you want to use an button[attribute] selector
  or      
  selector: '.button',                <== to use a class selector
  or    
  selector: 'button.button'           <== to use a more specific element.class selector
  
  standalone: true,

Template Usage:
<li>
    <button appButton></button>
</li>

```
Resulting in a DOM output without the extra layer of HTML...
``` 
<button appButton>
    <span>
        Logout
    </span>
    <span class="icon">
    →
    </span>
</button>
```

####  <ng-content select="" >
Note above, that all property standard propety binding can be used for dynamically populating the Text and icon.  
But, there is also another way by using special <ng-content> select attribute to leverage multiple <ng-content> elements.  
And only select a part of the content.  
Note, all non-selected content will be transformed into the default <ng-content>!
``` 
Button HTML:
<span>
    <ng-content/>
</span>
<ng-content select=".icon" />

Template Usage:
<li>
    <button appButton>
        Logout
        <span class="icon">→</span>
    </button>
</li>
```

#### ngProjectAs allows control over the projected selector...
I'm not sure of the reasoning, but keeping this note just in case.
``` 
Button HTML:
<span>
    <ng-content/>
</span>
<span class="icon">
    <ng-content select="icon" />
</span>

Template Usage:
<li>
    <button appButton>
        Logout
        <span ngProjectAs="icon">→</span>
    </button>
</li>
```
Lastly, you can provide fallback content in the <ng-content> body:
``` 
<span class="icon">
    <ng-content select="icon" >
        →                               <-- this is the fallback content
    </ng-content>
</span>
```


There is also a way to supply special content replacement using the select attribute.
```
<ng-content select="input, textarea" />
```



#### Extending Built-in Elements with Custom Components via Attribute Selector

For example, if you wanted a custom Button component, and you designed a component as follows
