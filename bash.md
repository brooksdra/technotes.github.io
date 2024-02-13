# Bash

## Advanced scripts at the bottom
- [Excel Script](#excel-script-id)

### COMMAND LINE
`history | grep stringToFind`            # Lists all commands from history containing stringToFind

### HISTORY
`history`: Displays the user's command history.  
`history <number>`: Displays the last <number> of commands in the history.  
`!<number>`: Executes the command with the corresponding history <number>.  
`!!`: Executes the last command in the history.  
`history -c`: Clears the command history.  
`history -w`: Writes the current command history to the .bash_history file.  
`history -a`: Appends the current command to the history file without waiting for the shell to exit.  

### WSL bash script not working because of /bin/bash^M bad interpreter: No such file or directory
Update script to replace newlines for immediate environment…  
`sed -i -e 's/\r$//' scriptname.sh`

### Find files by name removing all errors from the output
`find / -name "docker*.txt" -print 2>/dev/null`  

### Find in file 
`grep  "string" file`  
`cat file | grep "string"`  

### SSH and SFTP
`ssh daveb@10.1.10.156 `    "then provide password"  

`sftp daveb@10.1.10.156`  "provide password" if necessary  
sftp> `pwd` - Display remote working directory  
sftp> `lpwd` - Display local working directory  
sftp> `cd path` -  Change remote working directory to 'path'  
sftp> `lcd path` - Change local working directory to 'path'      
sftp> `ls` - Display contents of remote working directory  
sftp> `lls` - Display contents of local working directory  
sftp> `get` - Download file from remote working directory to local working directory  
sftp> `put` - Upload file from local working directory to remote working directory  

### Get a file from /Users/daveb/Documents/test.txt without maintaining a persistent connection
This logs into the sftp server at ~ or in this case /Users/daveb  
`sftp daveb@01.1.10.156:./Documents/test.txt`

### Search files for
`ripgrep (must install)`

### Favorite ls setting
`ls –las sort by date –last`

### Change Mod
`Chmod 777 filename or ugo=rwx`
`Chmod u=rwx,go=rw filename`    -- to mix things up

### Run something behind the scenes (in the background)
`./disk-monitor.sh & disown`
Then, use ctrl-Z if necessary

### Count files in a directory
`ls –1 | wc -l`

### List most recent 10 files
`ls -Art | tail -n 10`

### To get more information from ps
`ps -aux`

### SSH: How to change the window title to the Host's IP
    echo -ne '\033]0;10.195.132.57\007'

### BS has a file on each device, just source it something like bs.sh blah blah blah
    _HNUM=$(hostname | tr -d '[a-z]-')
    export PS1="alpha${_HNUM}$ "
    #export PS1='alpha7$ '
    export HISTSIZE=2000
    unalias ls
    alias retitle="echo -ne '\033]0;'$(hostname):$(ifconfig ethernet0 | grep 'inet ' | awk '{print $2}')'\007'"


### Check Linux version
    uname -r  
    lsb_release –a  "this may only be for torizon"

### Debugging bash script  
Run an script with debug turned on  
`bash –x ./script.sh`  
Or, for more dynamic control add the following to your script:  
`set –x`   # To enable debugging output  
`Set +x`   # To disable debugging output  

### Problem with newline conversion
Getting the following error when running a bash script named ./run-capture.sh:  
-sh: ./run-capture.sh: /bin/bash^M: bad interpreter: No such file or directory  
Means WINSCP improperly converted LF:CR, Fix with:  
`sed -i -e 's/\r$//' run-capture.sh`

### Tail command
See the last few lines of a file  
`tail filename.ext`  
See last 30 lines  
`tail –n 30 filename.ext`  
See last 30 ongoing  
`tail –n 30 –f filename.ext  or tail –fn 30 filename.ext`  

### Hostname
`sudo hostname –v new-host-name`

### Builtins
`command –V df`  # To check if it is a program  
df is /usr/bin/df  
`command –V echo`  
Echo is a shell builtin  
Builtins take precedence  
`command echo` # will run the builtin  
Enable –n echo # enables the command over the buildin  
`command –V echo`  
Echo is /usr/bin/echo  
`help`    # provides information about builtins  

`()` Parentheses, `{}` Braces, `[]` Brackets  
`~` Tilde expansion    # Users home variable or $HOME  
`~-` Old pwd or pwd before most recent cd

### {…} Brace expansion
Can be used as array substitution to run a command for every value in the braces  
`echo /tmp/{one,two,three}/file.txt`  
/tmp/one/file.txt /tmp/two/file.txt /tmp/three/file.txt  
`echo c{i,o,a}t`  
cit cot cat  
`echo {000..100}`  
000 001 002 … all the way to … 099 100  
`echo {000..100..2}`  
000 002 004 … all the way to … 098 100  
`echo {Z..A}`  
Z Y X W … C B A  
`touch file_{01..12}{a..d}.txt`  
Generates file_01a.txt, file_01b.txt … file_12d.txt  # nesting each expansion  
`head –n1 {dir1,dir2,dir3}/lorem.txt`  
Dumps the first line of the lorem.txt file in each of the three directories  

### ${…} Parameter expansion
`echo $a` or `echo ${a}`  is the same thing  
`greeting="hello there!"`  
`echo ${greeting:6}`  # returns There!  
`echo ${greeting:6:3}`  # returns The  
`echo ${greeting/there/everybody}`  # returns Hello everybody!  
`echo ${greeting//e/_} ` # returns H_llo Th_r_!  
`echo ${greeting/e/_} ` # returns H_llo everybody!  

### $(...) Command substitution
`echo "The kernel is $(uname -r)."`   # returns The kernel is 10.2.x.blah blah blah.  
`echo "Results: $(python3 -c 'print("Hi")' | tr [a-z] [A-Z])"` # returns Results: HI  

### $((…)) Arithmetic expansion
`echo $(( 3+3 ))`  # returns 6  
Careful with spacing and remember this is only integer arithmetic, special things happen for decimals.

### Tests [ ... ] and 
This is used to test conditions 0=true, all non-zero is false  
$ help test to see all the things you can test  
To see the return value, use $?   
`[ -d ~ ]; echo $?`  # returns 0  for my home directory is a directory  
`[ -d /bin/bash ]; echo $?`  # returns 1 because this is an executable  
Use = for strings and –gt, -lt, etc. for numbers  

### Extended Test [[ ... ]] to test multiple or complex conditions
`[[ -d ~ && -a /bin/bash ]]; echo $?`  #returns 0 because both are true  
`[[ -d ~ && -a /bin/mash ]]; echo $?`  #returns 1 because there is not mash  
You can also string together tests with an && to run the next condition  
`[[ -d ~ ]] && echo ~ is a directory` # returns /home/daveb is a directory
`[[ -d /bin/bash ]] && echo /bin/bash is a directory` # returns NOTHING, the echo statement isn't run

### Use true and false to force an issue
`true && echo "success!"` # displays success and false && echo "success!" Does not

### Use +~ to run a regex
`[[ "cat" =~ c.* ]] ; echo $?`  # returns 0 - true.  
`[[ "dat" =~ c.* ]] ; echo $?`  # returns 1 - false.  

### You can also use ((…)) for testing, see while/until loop below

### Arrays (limited to one layer deep)
bash works with indexed arrays:  
`declare –a snacks=("apple" "banana" "orange")`  
`echo ${snacks[2]}`  
orange  
`snacks[5]="grapes"`      #Jagged array is okay  
`snacks+=("mango")`  
`echo ${snacks[@]}`  
apple banana orange grapes mango
`for i in {1..6}; do echo "$i: ${snacks[i]}"; done`  
0: apple  
2: banana  
…  # This includes all indexes, even the ones without values  
6: mango  

### bash works with associative arrays, think of map
    declare –A snacks
    snacks[breakfast]=banana
    snacks["lunch time"]=nuts
    Snacks[dinner]="popped corn"


### Conditional If statements:
    If [[ $a>4 ]]
    then 
        Echo "more"
    elif [[ $a<4 ]]
        Echo "less"
    else
        echo "same"
    fi

### Stylistic choice:
    If [[ $a>4 ]]; then 
        echo "greater"
    fi

### While and Until Loops
    declare -i n=0
    while ((n<10)); do
        echo "n:$n"
        ((n++))
    done
    
    declare -i m=0
    until ((m==10)); do
        echo m:$m
        ((m++))
    done
    
    for i in 1 2 3; do
        echo $i
    done
    
    for i in {1..3}; do
        echo $i
    done
    
    for (( i=1; i<=3; i++ )); do
        echo $i
    done

### indexed array
    declare -a fruits=("apple" "banana" "cherry")
    for i in ${fruits[@]}; do
        echo $i
    done

### associative array
    declare -A people
    people["name"]="dave"
    people["id"]="1234"
    # use ! to access keys and quotes to include spaces
    for i in "${!people[@]}"; do
        echo $i: "${people[$i]}"
    done
    
    # from the ls command
    for i in $(ls); do  
        echo "Found a file: $i"
    done

    # * provides a list of filenames
    for i in $(ls); do  
        echo "Found a file: $i"
    done
    
    # input arguments (all)
    echo "There are $# arguments"
    for i in "$@"; do  
        echo "Found a argument: $i"
    done
    
### Case Statement
    animal="dog"
    case $animal in
        bird)  echo "Avian";;
        dog|puppy)  echo "Canine";;
        *) echo "No match!";;
    esac


### Process options passed in
    echo "$# options supplied"
    while getopts :u:p:ab option; do    # leading : necessary, trailing colon means values expected
        case $option in
            u) user=$OPTARG
               echo "user: $user";;
            p) pw=$OPTARG
               echo "pw: $pw";;
            a) echo "a flag provided";;
            b) echo "b flag provided";;
            ?) echo "unknow arg: $OPTARG";;
        esac
    done

### Ask for input
    echo "Enter name "
    read name
    echo "Enter pw "
    read -s pw
    read -p "Enter animal " animal
    read -ep "Enter fruit " -i banana fruit     #provide a default value
    echo $name $pw $animal $fruit

### Ask for option selection, will keep asking till a valid options or quit is provided
    PS3="Select IDE: "
    while true; do
        clear
        options=("VSCode" "Eclipse" "IntelliJ" "Web Storm" "Quit")
        select opt in "${options[@]}"
        do
            case ${REPLY} in
                1)  SelectedIDE=vscode         
                    break 2 ;;
                2)  SelectedIDE=eclipse
                    break 2 ;;
                3)  SelectedIDE=idea
                    break 2 ;;
                4)  SelectedIDE=storm
                    break 2 ;;
                5)  echo "you chose to quit!"
                    exit ;;
                *) echo "you chose choice ${REPLY} which is invalid";;
            esac
        done
    done

### A script to extract Excel data from a tab delimited file with {#excel-script-id}
    #!/bin/bash
    
    # pull a list of .log files with a wmem3- name prefix and convert all newlines to a space; for the cat command
    wmem3logs=$(ls -rt wmem3-*.log | tr '\n' ' ')
    echo "input file(s): $wmem3logs"
    
    # concatenate all files into one long file
    cat $wmem3logs > wmem3-combined.txt
    echo "catted to: wmem3-combined.txt"
    
    # remove all lines with non-table data 
    grep -vE "(date|hour|minute|second)" wmem3-combined.txt > wmem3-all-clean1.txt
    echo "filtered to: wmem3-all-clean1.txt"
     
    # retain these lines (not needed, but might be interesting for troubleshooting)
    grep -E "(date|hour|minute|second)" wmem3-combined.txt > wmem3-trash.txt
    echo "trash to: wmem3-trash.txt"
     
    # remove all blank lines
    grep -ve '^[[:space:]]*$' wmem3-all-clean1.txt > wmem3-all-clean2.txt
    echo "removed blanks to: wmem3-all-clean2.txt"
     
    # Add a header; this is open ended and can produce bad results of the input headers are different.
    echo -e 'date\tkernel\tmemtotal\tmemfree\tmemavail\ttotal\tdatacont\tdatastor\tenvironm\timagingc\tkiosk\tldap\tprocessc\tuserinte\tweston' > wmem3-all.txt
    cat wmem3-all-clean2.txt >> wmem3-all.txt
    echo "ready for excel: wmem3-all.txt"

### Imaging Controller: How many tests were run or images between each hang/crash:
Each __main__ is an IC restart, and the number at the left is the number of completed tests after the restart.  
`cat $(ls -rt ImagingController.log*) | egrep -a '(Test Complete|__main__ L)' | uniq -c -s 25 -w 50`
 
     33 2023-03-28 12:44:37,291 INFO pro.......__main__ Launching the m.dt.x ImagingSubsystem application version: 0.0.33
      1 2023-03-30 16:02:44,466 INFO pro.......imaging_subsystem ^^^ Test Complete ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
     11 2023-03-30 16:22:07,971 INFO pro.......__main__ Launching the m.dt.x ImagingSubsystem application version: 0.0.33
      1 2023-04-03 16:12:58,870 INFO pro.......imaging_subsystem ^^^ Test Complete ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      1 2023-04-03 16:34:39,016 INFO pro.......__main__ Launching the m.dt.x ImagingSubsystem application version: 0.0.33
      2 2023-04-03 17:02:26,814 INFO pro.......imaging_subsystem ^^^ Test Complete ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Slightly different example __main__ is an IC restart, and the number at the left is the number of images taken after the restart.  
`cat $(ls -rt ImagingController.log* | tail -10) | egrep -a '(__main__ L|--- Snapshot ---)' | uniq -c -s 25 -w 50`

      3 2023-04-17 14:13:20,228 INFO pro.......__main__ Launching the m.dt.x ImagingSubsystem application version: 0.0.36
    103 2023-04-17 16:04:25,659 INFO pro.......imaging_subsystem --- Snapshot ---------------------------------------------------------
      8 2023-04-17 19:06:19,120 INFO pro.......__main__ Launching the m.dt.x ImagingSubsystem application version: 0.0.36
    290 2023-04-18 19:33:27,440 INFO pro.......imaging_subsystem --- Snapshot ---------------------------------------------------------
      2 2023-04-18 20:27:46,739 INFO pro.......__main__ Launching the m.dt.x ImagingSubsystem application version: 0.0.37
     50 2023-04-18 20:36:07,249 INFO pro.......imaging_subsystem --- Snapshot ---------------------------------------------------------
      1 2023-04-18 21:05:17,225 INFO pro.......__main__ Launching the m.dt.x ImagingSubsystem application version: 0.0.37
    646 2023-04-18 21:07:11,290 INFO pro.......imaging_subsystem --- Snapshot ---------------------------------------------------------
      1 2023-04-19 13:42:55,097 INFO pro.......__main__ Launching the m.dt.x ImagingSubsystem application version: 0.0.37
      7 2023-04-19 13:52:07,104 INFO pro.......imaging_subsystem --- Snapshot ---------------------------------------------------------
      2 2023-04-19 14:23:44,052 INFO pro.......__main__ Launching the m.dt.x ImagingSubsystem application version: 0.0.37

### call-many-something.sh
    #!/bin/bash
     
    echo $1
    CAPTURES=1
    if [ -n "$1" ]
    then
        let CAPTURES=$(($1))
    fi
     
    echo "Calling capture ${CAPTURES} time(s)"
    # this needs to built first
    # docker build -t capture_app .
    COUNTER=1
    while [  $COUNTER -le $CAPTURES ]; do
       echo Calling captuer: $COUNTER
       let COUNTER=COUNTER+1 
       ./capture
    Done

### curl-simple-send.sh
    #!/bin/bash
     
    AUTH_HEADER="Authorization: pro......"
    CONTENT_HEADER="Content-Type: application/json"
    PC_GET_VERSION_URL= http://localhost:8686/m.dt.x/setting/subsystem
     
    subsystem=imaging-controller
     
    echo "" | curl -s -X GET -H "$AUTH_HEADER" -H "$CONTENT_HEADER" -d'@-' $PC_GET_VERSION_URL/$subsystem
    echo ""

### curl-many-results.sh
    #!/bin/bash
    #
    #set -x
     
    AUTH_HEADER="Authorization: pro......"
    CONTENT_HEADER="Content-Type: application/json"
     
    PC_GET_VERSION_URL= http://localhost:8686/m.dt.x/setting/subsystem
    subsystem=imaging-controller
     
    DS_GET_RESULT_URL= http://localhost:8585/m.dt.x/result
    id=6410b2f3900eab5edc96991a
     
    # echo "" | curl -s -X GET -H "$AUTH_HEADER" -H "$CONTENT_HEADER" -d'@-' $PC_GET_VERSION_URL/$subsystem
     
    #curl -s -X GET -H "$AUTH_HEADER" -H "$CONTENT_HEADER" -d'@-' $DS_GET_RESULT_URL/$id 2>/dev/null
     
    result=$(echo "" | curl -s -X GET -H "$AUTH_HEADER" -H "$CONTENT_HEADER" -d'@-' $DS_GET_RESULT_URL/$id 2>/dev/null)
    echo $result
     
    newResult=$(echo $result | sed 's/"_id":"6410b2f3900eab5edc96991a",//')
    echo $newResult
     
    newWrites=1000000
     
    for i in $(seq 1 $newWrites);
    do
      curl -s -X POST -H "$AUTH_HEADER" -H "$CONTENT_HEADER" -d "$newResult" $DS_GET_RESULT_URL -o /dev/null
      res=$((i%100))
      if [ $res -eq 0 ]
      then
        echo "$i/$newWrites"
      fi
    done
     
    echo "done"



