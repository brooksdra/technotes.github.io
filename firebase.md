# Firebase

Setup firebase in google at https://console.firebase.google.com/u/0/

Supabase is an open source firebase alternative: https://supabase.com/

### A few quick links to keep around
Started this tutorial to get a handle on a real world app with auth, database, and maybe analytics.
https://firebase.google.com/codelabs/firebase-web?hl=en#0
At the end, I deployed the app to Firebase Hosting with the following output:
Project Console: https://console.firebase.google.com/project/friendlychat-cff21/overview
Hosting URL: https://friendlychat-cff21.web.app

### Still a good resource for HTML, CSS and Material
https://traversymedia.com/#courses

### This might be a good tutorial for getting started with the app
https://developers.google.com/codelabs/building-a-web-app-with-angular-and-firebase#0 

Project Console: https://console.firebase.google.com/project/kanbanfire-98326/overview
Hosting URL: https://kanbanfire-98326.web.app

### Next attempt is to add authentication to the test KanbanFire application.
This is an interesting youtube video about file organization, 
See How to Connect Firebase Users to their Data - 3 Methods  will use the first layout example of user specific items
```
npm install -g @angular/cli
npm install -g @angular/material
npm install -g firebase-tools
npm list -global -json     
{
  "name": "lib",
  "dependencies": {
    "@angular/cli": {
      "version": "13.2.5"
    },
    "@angular/material": {
      "version": "13.2.4"
    },
    "corepack": {
      "version": "0.10.0"
    },
    "firebase-tools": {
      "version": "10.2.1"
    },
    "npm": {
      "version": "8.5.1"
    }
  }
}
```

### Adding project to Firebase…
daveb@Daves-M1 journal-ease-again % `ng add @angular/fire`

### Use the following to manage firestore rules 
https://firebase.google.com/codelabs/firebase-web?hl=en#11  
Update firebase-firestore.rules  
`Firebase deploy --only firestore ` 
I use this to set up a slightly different set of rules.  


### Deploy a testing site for preview with a different preview_name
`firebase hosting:channel:deploy preview_name`
