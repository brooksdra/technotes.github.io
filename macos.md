# MacOS

Setting up a development box.

## Profile Info
.zprofile : z-shell configuration sourced when logging into account (bash see .bash_profile). Sets environment variables, aliases, etc.   
.zshrc    : new terminal window configuration (bash see .bashrc). Sets shell specific aliases, and custom prompts.    
  
- Use shift + command + . to toggle hidden files.  
- 

## Development Tools to Install

## git 
Just comes for free!

### SVN (Subversion)
- [Homebrew Site](https://formulae.brew.sh/formula/subversion)
- [Subversion Site](https://subversion.apache.org/)
- [SVN Tech Notes](svn.md)
``` 
brew install subversion

```

### NVM, Node.js, NPM  
- [Node.js Tech Notes](node.md)
``` 
nvm install 18.12   // to align with the current projects.
nvm list            // to see what else is installed
```

### SKDMan (Java, maven)         
- [SDKMan Installation](https://sdkman.io/install)
``` 
curl -s "https://get.sdkman.io" | bash

sdk install java 16-open        // Align with current project (I know, I know)
sdk install java 17-open        // If I want to bring current project up to the LTS
sdk install java 21-open        // If I want to get up to the most recent LTS

sdk install maven 3.9.6         // Align with current projects
```
Install setting.xml at ~/.m2/settings.xml
```
mvn package -U                  // Makes sure to import all packages and required libraries
```
Setup a virtual /Pro...Suite at ~/Development/Pro...SuiteSynthetic and add /etc/synthetic.conf as:
``` 
Pro...Suite{1 tab, not spaces}/User/daveb/Development/Pro...SuiteSynthetic
```
Reboot

### Jetbrains
- [Toolbox](https://www.jetbrains.com/toolbox-app/) To install and manage the other jetbrain tools.  
- [IntelliJ Idea](https://www.jetbrains.com/idea/)  
Make sure the appropriate Java and Maven are already installed and active.     
Check out the projects into a folder, open that via Idea, and let it analyse the project. 
Verify the

- [WebStorm](https://www.jetbrains.com/webstorm/)  


- [PyCharm](https://www.jetbrains.com/pycharm/)  

### Docker
- [Docker](https://www.docker.com)
- [DockerHub](https://hub.docker.com)
Run through the tutorial to make sure everything is working...  
Build test-suite-interface
Build test-suite-service

#### Mongodb

#### Mariadb

## Usage
