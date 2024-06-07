# PyCharm
Also see IntelliJ notes for more global editor details

## Shelf Info
The Shelf is workspace specific
Use Settings > Version Control > Shelf to set the directory.

I prefer a centralized place /Pro...Suite/charm-resources/shelf

## Virtual Environment 
There is a problem starting a new Python workspace with the same name as a previously deleted workspace.  For me, it is caused by checking out the project into a similarly named subdirectory.

The problem has to do with PyCharm caching the original project's virtual environment and thus not triggering a new project setup.

If you like to delete your entire project, clone a fresh copy from SVN, and start new you must do the following:

Make sure PyCharm is not opened to that new project.

Delete the workspace

Open PyCharm’s internal configuration file:

C:\Users\{your user id}\AppData\Roaming\JetBrains\PyCharm2023.3\options\jdk.table.xml

Notice each jdk tag contains a workspace:
```
   <jdk version="2">
      <name value="Python 3.9 (charm-medtox-ic-qa)" />
      <type value="Python SDK" />
      <version value="Python 3.9.9" />
      <homePath value="C:\Users\daveb\charm-medtox-ic-qa\Scripts\python.exe" />
      <roots>
        <classPath>
          <root type="composite">
            <root url=file://$USER_HOME$/AppData/Local/Programs/Python/Python39/DLLs type="simple" />
            <root url=file://$USER_HOME$/AppData/Local/Programs/Python/Python39/Lib type="simple" />
            <root url="file://$USER_HOME$/AppData/Local/Programs/Python/Python3
            . . .
            <root url=file://$APPLICATION_HOME_DIR$/plugins/python/helpers/typeshed/stubs/flake8-typing-imports type="simple" />
            <root url=file://$APPLICATION_HOME_DIR$/plugins/python/helpers/typeshed/stubs/tree-sitter-languages type="simple" />
          </root>
        </classPath>
        <sourcePath>
          <root type="composite" />
        </sourcePath>
      </roots>
      <additional ASSOCIATED_PROJECT_PATH="C:/Pro...Suite/charm-medtox-ic-qa" SDK_UUID="5eb19f9d-4972-44f8-952c-826af29facb9">
        <setting name="FLAVOR_ID" value="VirtualEnvSdkFlavor" />
        <setting name="FLAVOR_DATA" value="{}" />
      </additional>
    </jdk>
```

Find the workspace you are trying to rebuild and completely, and carefully remove the specific <jdk>…</jdk> and save.

Now open PyCharm on the newly cloned workspace and wait for the prompts and for all of the project indexing to finish.

I’ve slightly modified the Windows startup script and added these notes to it.

### IMPORTANT NOTE: 
PyCharm, actually all of the JetBrain’s Ide’s, store the SVN Shelved changes locally within the project workspace.

If you want to preserve this and have access from multiple workspaces you can move it using: Settings > Version Control > Shelf

Scratch files and database configuration files are already centrally located.
