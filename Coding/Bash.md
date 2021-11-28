## TABLE OF CONTENTS
1) [BATCH](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Bash.md#batch)
2) [BASICS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Bash.md#basics)
3) [OPTIONS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Bash.md#options)
4) [SCRIPT EXAMPLES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Bash.md#script-examples)

<br />

## BATCH
- `@echo off`
   - `echo off`:  no print out of command, but result only 
   - `@`:  no output "echo off"
- `rem`: comment 
- `pause`: script stop ("Press any button...")

<br />

## BASICS

#### Variables
- `readonly VARIABLE=value`: set variable read-only
- `unset VARIABLE`: remove assigned value from variable
- Conversion: "shell variable" -> "environment variable"
   - **Temporary Solution**
   - `VARIABLE=value`
   - `echo $VARIABLE` #control purpose
   - `export VARIABLE` 
   - **Permanent Solution**
   - `nano ~/.bashrc`
   - `export VARIABLE=value` Enter this line inside of bashrc

#### Arrays
- `array_name[index]= "value_0 ... value_n"`: Shell Writing Style !
- `array_name[index]=(value_0...value_n)`: Bash Writing Style !
- `${array_name[index]}`: Accessing Array Values with { } !
- `${array_name[*]}`: Accessing All Array Values
    - Example: `month=("Jan" "Feb" "Mar" "Apr" "May")`
    - `echo ${month[3]}`: Apr
- OR functionality:
    - `command1 || command2`
    - `-o`
- AND functionality:
   - `command1 && command2`
   - `-a`

#### Quotes & Execution
- Single Quote `' '`: All special characters between these quotes lose their special meaning
- Double Quote `" "`: Most special characters between these quotes lose their special meaning      
- Back Quote `` ``: Anything in between would be treated as command and would be executed
- `$()` --> shell execution tag
- `command > /dev/null`: Execute command w/o output to terminal
- Create subshell with `( )`
   - Exp: `(cd /tmp; pwd)` --> subshell does not affect current shell

#### Special Characters (During Script Execution)
Command | Meaning
`echo $0` | The filename of the current script
`echo $#` | The number of arguments supplied to a script
`echo $$` | The process number of the current shell
`echo $?` | The exit status of the last command executed
`echo $!` | The process number of the last background command
`echo $*` | All the arguments are double quoted
`echo $@` | All the arguments are individually double quoted

#### Special Characters (Without Script Execution)
Command | Meaning
`echo $SHELL` | Check Current Shell
`ps -p $$` | Check Current Shell process ID
`grep "^$USER" /etc/passwd` | Check Current User of Shell

#### Brackets
- **Curly Bracket {}**:
   - `echo f{oo,ee,a}d` --> food feed fad
   - `mv error.log{,.OLD}` --> error.log.OLD
   - `for num in {000..2}; do echo "$num"; done` --> 000; 001; 002
   - `echo {00..8..2}` --> 00 02 04 06 08
   - `echo {D..T..4}` --> D H L P T
- **Curly Brace ( )**:
   - `echo $((14 * 2))` --> 28 
   - `echo $((a++))` --> a + 1
   - `((variable = 28))`

#### Operators
```
a=10
b=20
echo "Sub : `expr $a - $b`"  // -10
echo "Sum : `expr $a + $b`"  // 30
echo "Mul : `expr $a \* $b`" // 0,5
echo "Div : `expr $b / $a`"  // 2
echo "Mod : `expr $b % $a`"  // 0
echo "Equ :"[ $a == $b ]   // False
echo "Une :"[ $a != $b ]   // True
```

#### If-Statement
```
# Basic
if [ condition ]    // pay attention to the spaces around the condition !
then  
  command
fi

# Extended
if [ condition ]
then
  command
elif [ condition ]
  command
else
  command
fi
```

### Loops
```
for/while/until [ condition ]
do
    command
done
```

### Functions 
```
function_name () { 
   list of commands
   return
}
```

<br />

## OPTIONS

- `bash -p`: If supplied at invocation, the effective user id (EUID) is not reset to RUID
- `bash -xv [script]`: debugging

<br />

## SCRIPT EXAMPLES

#### Clickbait (Windows)(Batch)
```
# Open the browser continuously
# Attention, may lead to DoS !
#save as "clickme.txt.bat"

echo off
:LoopStart
start
start www.google.com
goto :LoopStart
```

#### Get Credentials 
```
#! /bin/bash

# -p = prompt
# -s = silent
read -p 'Username: ' uservar     
read -sp 'Password: ' passvar    
echo Thank you $uservar we now have your login details
```

#### Get MD5 of Name
```
#! /bin/bash

myname=$(whoami)
mytarget=$(echo $myname | md5sum | cut -d ' ' -f 1)
# output for user "root" --> 74cc1c60799e0a786ac7094b532f01b1
```

#### Hand over parameter(s) to netcat with while loop
```
i=1
while [ $i -le 1000 ]
do
echo "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ, $i" | nc localhost 30002 >> /tmp/file.txt &
((i=i+1))
# Alternative: let "i += 1" 
done
```

#### Backup Automisation
```
#! /bin/bash

# Wait until all services woke up 
sleep 240

#Get date 
date = $(date +%d.%m.%Y)

#Update process
apt-get update
apt-get upgrade
echo "software update performed on $date" >> /var/log/updates.log

#Updates during normal operation
while true
do
time=$(date +%H.%M)
date=$(date +%d.%m.%Y)

#Set time 
if ["$time" == 18:00];
then
apt-get update
apt-get upgrade
echo "software update performed on $date" >> /var/log/updates.log
fi
sleep 60
done
```

#### Check Remote Server Status
```
#!/bin/bash

remote="backup"
user="bob"
 
echo "Local system name: $HOSTNAME"
echo "Local date and time: $(date)"
 
echo
echo "*** Running commands on remote host named $remote ***"
echo
ssh -T $user@$remote <<'EOL'
# -T = Disable pseudo-terminal allocation 
# -t = Force pseudo-terminal allocation. This can be used to execute arbitrary screen-based programs on remote machine
	now="$(date)"
	name="$HOSTNAME"
	up="$(uptime)"
	echo "Server name is $name"
	echo "Server date and time is $now"
	echo "Server uptime: $up"
	echo "Bye"
EOL
```

#### Check Available Hosts
```
#! /bin/bash

echo
# Enter Network Address 
read -p "Enter Network Address: " network

#Use fping as scan tool; write error messages to text file 
echo
echo "Available Hosts: "
for i in `fping -r 0 -aA -g $network/24 2>/tmp/error.txt`
# -r = --retry=N | -aA = --alive --addr | -g = --generate target list from supplied IP netmask
do 
#Show IP address 
if [ $i = "192.168.56.1" ]
then
    echo "$i (Standard-Gateway)"
else
    echo $i
fi
done
echo
```
