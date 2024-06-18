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
expired timers etc. When angular gets the nofication, it checks the zone for necessary UI updates. With signals, Angular
knows exactly what to change for any specific value change.  

The ```computed``` function provides a way for Angular to set up a subscription to watch the signal even in code.  
So, in this case, whenever selectedUser is set, imagePath will be recomputed.

``` 
    selectedUser = signal(initialValue);
    imagePath = computed( () => '/assets/users/' + this.selectedUser().avatar );
    
    this.selectedUser.set(updatedValue);
```
To access a signals value, you must call it as a method, then access the variables. This call to the method is what
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

OR
avatar = input<string>();                   // generate a signal using the input()...            
avatar = input.required<string>();          // Make it required
```

// Child component coded in the parent HTML
```
<app-user [avatar]="users[2].avatar"/>     // Passing a value from the parent the child component tag attribute and its .ts.
```

### @Output and output()
@Output decorates values sent from a child component back up to the parent component.
There is a more modern output() method which works exactly like the @Output, 

This is the child component:
```
@Output select = new EventEmitter<string>();
OR
select = output<string>();

onSelectUser(id: string) {
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
