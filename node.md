# NODE  (NPM & NVM)

[Install NVM](https://github.com/nvm-sh/nvm?tab=readme-ov-file#installing-and-updating) (Node Version Manager) first.

If you get a missing all profiles file, touch ./zshrc on the mac, ./bashrc on linux to generate an empty and try again.

Restart terminal and check versions

```nvm -v```  
M1 - 0.37.2  
PY - 0.39.7  

```node -v```   
M1 - 20.11.1  
PY - 22.2.0  

```npm -v```  
M1 10.2.4  
PY 10.7.0  

Install the latest node  
```nvm install node```

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

Start a new project in a directory (This basically just builds the initial package.json)  
```npm init```  

Download all of the dependencies of an existing project based on the package.json  
```npm install```  

Install specific dependency for a project  
```npm install express```   

NPM installs local project modules at project_root/node_modules.  

Install a specific dependency globally  (This is a bit more complicated...)  
```npm install sass -g```  

NPM installs global modules at /usr/local/lib/node_modules.   
In this case, sass is installed /usr/local/lib/node_modules/sass.   
SASS is a JavaScript (node) application, so npm put a symlink at /usr/local/bin/sass which is in the `PATH` that points to /usr/local/lib/node_modules/sass/sass.js  

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

Update dependencies  
```npm update```  
