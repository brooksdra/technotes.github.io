# NODE NPM NVM

Use NVM (Node version manager) to install whichever version of node and the node package manager.

<!-- TOC -->
* [NODE NPM NVM](#node-npm-nvm)
  * [NVM](#nvm)
  * [NPM](#npm)
    * [Registry](#registry)
    * [package.json](#packagejson)
      * [Script](#script)
  * [NPX](#npx)
  * [Node.js](#nodejs)
    * [Scripting](#scripting)
    * [Bundlers](#bundlers)
<!-- TOC -->

## NVM

- [Npm Registry](https://www.npmjs.com/)
- [Udemy Tutorial](https://www.udemy.com/course/npm-node-package-manager-course/learn/lecture/35429292#overview)
- [Npm Packages Trending](https://npmtrends.com/)
- [Lightweight Nodejs Private Repo](https://github.com/verdaccio/verdaccio)

[Install NVM](https://github.com/nvm-sh/nvm?tab=readme-ov-file#installing-and-updating) (Node Version Manager) first.

If you get a missing all profiles file, touch ./zshrc on the mac, ./bashrc on linux to generate an empty and try again.

Restart terminal and check versions

```
nvm -v
```  
M1 - 0.37.2  
PY - 0.39.7  

Install the latest node LTS version
```nvm install node --lts```

Important: use the following to keep your global packages up-to-date while maintaining campatibility with the new Node.js release:
``` 
nvm install node --lts --reinstall-package-from=current
```

Check what is installed and being used  
```
nvm list 
->      v22.2.0
        system
default -> node (-> v22.2.0)
iojs -> N/A (default)
unstable -> N/A (default)
node -> stable (-> v22.2.0) (default)
stable -> 22.2 (-> v22.2.0) (default)
lts/* -> lts/iron (-> N/A)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.24.1 (-> N/A)
lts/erbium -> v12.22.12 (-> N/A)
lts/fermium -> v14.21.3 (-> N/A)
lts/gallium -> v16.20.2 (-> N/A)  
lts/hydrogen -> v18.20.3 (-> N/A)  
lts/iron -> v20.14.0 (-> N/A)  
```

## NPM
The NPM (node package manager) is, in fact, a node package as well.
```
npm -v
```  
M1 10.7.0  
PY 10.7.0

Start a new project in a directory (This basically just builds the initial package.json)  
```
npm init 
npm init -y   // To accept y for all of the prompts 
```  

Download all of the dependencies of an existing project based on the package.json  
```
npm install                         // This is typical development process.
npm clean-install                   // This cleans up the node_modules and builds based on both package.json and package-lock.json.
                                    // package-lock.json is required.
npm install --omit=dev              // Removes all development dependencies.
npm prune --production              // Prunes all development dependencies to prepare for production.
npm install ./other-local-project   // installs a copy of the local project into this project 
```  

Find out information about the uuid package
```
npm view uuid 
```

Install a specific dependency for a project  
```
npm install uuid          // to get the latest
npm install uuid@9.0.1    // to specify a version
npm uninstall uuid
```
NPM installs local project modules at project_root/node_modules.  
In this case, uuid is installed at project_root/node_modules/uuid.   
uuid is a JavaScript (node) application, some application like uuid, register with npm so they can be run from the command line.  
Verify this with
``` 
npm list    // list local package for the project
npm root    // show where the local packages are installed
```

NPM puts a symlink at project_root/node_modules/.bin which puts it on the npm search path for local projects.
``` 
npm run uuid  
```

Install a specific dependency globally (This is a bit more complicated...)  
```
npm install sass -g
npm uninstall ssas -g
```  

NPM installs global modules at /usr/local/lib/node_modules.   
-- or if you are using NVM /Users/daveb/.nvm/versions/node/v22.2.0/lib/node_modules
In this case, sass is installed /usr/local/lib/node_modules/sass.   
SASS is a JavaScript (node) application, some application register so with node they can be run from the command line.
Verify this with
``` 
npm list -g    // list global package for a project
npm root -g    // show where the global packages are installed
```
NPM put a symlink at /usr/local/bin/sass which is in the `PATH` that points to /usr/local/lib/node_modules/sass/sass.js  

sass.js example first line tells your system to run this using node!  
```
#!/usr/bin/env node

require('./sass.dart.js');
var library = globalThis._cliPkgExports.pop();
.
.
.
library.cli_pkg_main_0_(process.argv.slice(2));
```

List dependencies
```
npm list            // for local dependencies
npm list -g         // for global dependencies
npm list -depth-1   // for transative dependencies
```  

NPM also has development dependencies which are only used for the development cycle.  
esbuild is a lightweight bundler (see [Bundlers](#bundlers) section below), jest is a unit test environment.  
The dev dependencies are not built into a production build.   
```
npm install esbuild --save-dev
npm install jest --save-dev
```

Verify current packages with
``` 
npm outdated            // list all package that have newer versions
npm doctor              // checks for problems
npm audit               // looks for problems
```

Update packages
``` 
npm update uuid         // updates a specific module
npm update              // update all packages in node_module
npm update --save       // update all packages in node_module, package.json, and package-lock.json
```

Cleanup NPM packages
``` 
npx npkill              // analysis of the node_modules installed
npm update              // update all packages in node_module
npm update --save       // update all packages in node_module, package.json, and package-lock.json
```

### Registry
You can install Verdaccio, login and register with npm.
``` 
npm set registry http://localhost:4873
```
This updates .npmrc file.
Now publish your module to the registry with
``` 
npm publish
```

### package.json
#### Script
The scripts section of the package has script that can be run via npm.    
You can write small bash type scripts for the scripts for example:  
``` 
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index.js",
    "hello": "echo \"Running my hello script...\" && node index.js"
    "watch": "node --watch index.js"
  },
```
Use --watch to rebuild and restart after every save.

``` 
npm run hello 

> npm-practice@1.0.0 hello
> echo "Running my hello script..." && node index.js

Running my hello script...
Hello World!
```

Run npm specific scripts like "start" and "serve"
```
npm start
npm serve
```
Run your own named scripts like "drb_script"
```
npm run drb_script
```

## NPX
Node Project Execute.  
If any dependencies are not installed, they will be temporarily installed and run.
``` 
npx uuid        // if not installed, npx will install uuid and then run it.
npm exec uuid   // if not installed, npm will install uuid and then run it.
```

## Node.js
Node.js is a JavaScript server engine used to run JavaScript scripts locally without a browser.

```node -v```   
M1 - 20.11.1  
PY - 22.2.0

### Scripting
Old (pre ES 5) scripting style
``` 
const uuid = require('uuid');
const { v4 } = require('uuid'); // de-reference

console.log("Hello World!");
console.log("Your new  id is " + uuid.v4());
console.log("Your next id is " + v4());
```

New ES 5 scripting style  
To use this, add "type": "module" to the package.json  
``` 
import { v4 as uuidv4 } from 'uuid';

console.log("Hello World!");
console.log("Your new  id is " + uuidv4());
 ```

### Bundlers
esbuild prepares code developed in the project to be able to run in the browser.  
Add this to your package.json scripts:
``` 
    "build-browser": "esbuild index.js --bundle --outfile=dist/out.js",
    "build-node": "esbuild index.js --bundle --platform=node --outfile=dist/out.cjs",
    "build-all": "npm run build-browser && npm run build-node"
```
