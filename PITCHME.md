## Intro to BASH Shell Scripting
### John Kennedy
#### skebi69@gmail.com
Presentation: https://gitpitch.com/skebi69/IntroBash
Source: https://github.com/skebi69/IntroBash

---
### Disclaimer
-   As in most of Linux, there is more than one way to do things. My way may not always be the best. |
-   Some of my techniques and methods may be older/outdated. I am old. |
-   There are going to be somethings that I miss out on (arrays) either on purpose or by accident. |

+++
### Notes
-   I would like to have built a usable script but did not have time so: |
-   Hopefully my examples will be easily modified to fit your needs |

---
### Topics
-   Why script? |
-   She-Bang - Not Ricky Martin (see - I told you I was old) |
-   Variables |
-   Special variables |
-   User input |

+++
### Topics (Cont)
-   Conditional handling |
-   Select/case text menu |
-   Loops |
-   Functions |

---
### Why Script?
-   Run series of commands |
-   Build a long, complicated command |
-   Run commands that depend on specific conditions/results |
-   Run repetitive commands |
-   A lazy sysadmin is a good sysadmin - Let your scripts do the work for you |

---
### She bang (#!)
-   Start every script to set interpreter |
-   #!/bin/bash |

---
### Variables
-   A temporary store for small pieces of information |
-   No need to declare |
-   Can contain any type of data - String, integer, float, etc |
-   Good practice to surround with curly braces "{}" |
-   Like file names, try and avoid spaces in variables where possible |

+++
### Other types of variables
-   Special variables |
-   Arrays (not covered today) |

+++
### Special variables
-   $? - Exit code of last command |
-   $0 - Script name |
-   $1 - $N - Option 1 to whatever |
-   $$ - PID of script |
-   $IFS - Internal field separator - Normally set to whitespace |

---
### User input
#### Syntax
```bash
read variable
``` 

```bash
read <options> variable
``` 

#### Options 

  -p - Prompt 

```
read -p "Enter a number: " NUM
echo ${NUM}
```

  -s - Supress output

```
echo "Enter password "
read -s PASSW
echo "${PASSW}"
```

Note:
The read command can be used to stop a script at certain points for debugging. I usually use the variable "dummyvar" so I know at a glance what the read is for.

+++
### A read example
```bash
echo "Enter your new password: "
read -s PASSWD1
echo "Enter your password again: "
read -s PASSWD2
if [[ ${PASSWD1} == ${PASSWD2} ]]
then
  PASSWD=$PASSWD
  echo "Your password has been saved"
else
  echo "The two passwords do not match, start over..."
fi
```
@[1-2](Ask for password but supress output from user)
@[3-4](Ask user to repeat and supress)
@[5-6](if statement to make sure passwords match)
@[7-8](What to do if they match)
@[9-10](What to do if they don't match)
@[11](Close if statement)

---
### Conditional Handling
*  if statement |

*  if else |

*  if elif |

*  case |

+++
### if statement
*  Uses a test with a binary output to determine path to take
-  Test operators - http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html
-  Arithmetic operators - -eq, -ne, -lt, -le, -gt or -ge
```bash
if [[ test condition ]]
then
  Do lots of stuff
fi
```
@[1-2](The if statement and condition it is looking for)
@[3](If the condition is true, run this command)
@[4](Close out the if statement)

+++
### Example of use
```bash
grep Hello *
ANSW=$?
if [[ ${ANSW} -lt 1 ]]
then
  echo "The command worked"
fi
```

@[1](The command you are testing output from)
@[2](Special variables can be very volitile so I usually create a "disposable" variable to hold them)
@[3-4](The if statement and condition it is looking for)
@[5](If the condition is true, run this command)
@[6](Close out the if statement)
+++
### if else statement
*  Uses a test with a binary output to determine path to take
*  Provides what to do if the condition is false
-  Syntax
```bash
if [[ test condition ]]
then
  Do lots of stuff
else
  Do different stuff
fi
```
@[1-2](The if statement and condition it is looking for)
@[3](If the condition is true, run this command)
@[4-5](If the statement is false, do this stuff)
@[6](Close out the if statement)

+++
### Example of use
```bash
grep Hello *
ANSW=$?
if [[ ${ANSW} -lt 1 ]]
then
  echo "The command worked"
else
  echo "I can't find Hello anywhere"
fi
```

@[1-2](The command you are testing output from and "disposable" variable)
@[3-4](The if statement and condition it is looking for)
@[5](If the condition is true, run this command)
@[6-7](If the condition is NOT true, run this command)
@[8](Close out the if statement)

+++
### if elif statement
*  Uses a test with a binary output to determine path to take
*  Uses further tests to provide different paths
-  Syntax
```bash
if [[ test condition ]]
then
  Do lots of stuff
elif [[ Second test condition ]]
  Do different stuff
else
  Do different stuff
fi
```
@[1-2](The if statement and condition it is looking for)
@[3](If the condition is true, run this command)
@[4-5](If the first statement is false and this is true, do this stuff)
@[6-7](If the first and second statements are false, do this stuff)
@[8](Close out the if statement)

+++
### Example of use
```bash
ANSW=6
if [[ ${ANSW} -lt 1 ]]
then
  echo "The answer is less than 1"
elif [[ ${ANSW} -lt 5 ]]
  echo "The answer is less than 5"
else
  echo "The answer is less than 10" 
fi
```

@[1](Setting a variable)
@[2-4](The if statement and condition it is looking for, and what to do if true)
@[5-6](The second statement and what to do if true)
@[7-8](If the first two conditions are NOT true, run this command)
@[9](Close out the if statement)

+++
### case statement
*  Gives several different paths depending on the results of a single condition
```bash
case <expression> in
  case1)
    break
    ;;
  case2)
    break
    ;;
  *)
    break
    ;;
esac
```
@[1](expression is usually a variable that has been previously set)
@[2-4](The first clause. "break" is needed to prevent endless case loop. ";;" terminates the clause)
@[5-7](The second clause. "break" is needed to prevent endless case loop. ";;" terminates the clause)
@[8-10](The "catch all" clause. This happens if none of the other clauses match)
@[11](Close your case statement)

Note:
Can replace (and better than) nested if statements

+++
### Example of use
```bash
disk=`df -h | grep -v snap | awk '{print $5}' | grep % | grep -v Use | sort -n | tail -1 | cut -d "%" -f1 -`
case ${disk} in
[1-6]*)
  echo="No disk issues here, move along"
  break
  ;;
[7-8]*)
  echo="There is a partition with ${disk}% space. Check it out..."
  break
  ;;
9[0-8])
  echo="Seriously...  One partition is ${disk}% full."
  break
  ;;
99)
  echo="Wake up and do something...There's a partition at ${disk}%!"
  break
  ;;
*)
  echo="W. T. F.!!!!"
  break
  ;;
esac
```

@[1](Get a number)
@[2](Case statement)
@[3-6](Stanza 1)
@[7-10](Stanza 2)
@[11-14](Stanza 3)
@[15-18](Stanza 4)
@[19-22](Stanza 5 - Catch all)
@[23](Close case)

+++
### select case to create menus
*   Allows menus in your script

```bash
select <variable> in <list>
do
  case $<variable in
    case1)
      break
      ;;
    case2)
      break
      ;;
    *)
      break
      ;;
  esac
done
```

@[1-2](select statement with variable and list)
@[3](The case statement using the select variable)
@[4-6](The first clause. The result of menu number 1)
@[7-9](The second clause. The result of menu number 2)
@[10-12](The "catch all" clause. This happens if the user picks a non choice)
@[13](Close your case statement)
@[14](Close your select statement)

---
### Loops
- for loop |
- while loop |
- until loop |

+++
### for
- Iterates through a list
- Syntax
```bash
for i in <list>
do
  All the things
done
```

@[1-2](for statement. i = variable. <list> can be any list you can think of)
@[3](What to do with each item in the list)
@[4](Close loop)

+++
### for loop example
```
for i in {1..5}
do
  echo ${i}
done
```

@[1-2](for statement. i = variable. List is the number range 1 to 5)
@[3](echo ${i} which is number 1 to 5)
@[4](Close loop)


+++
### while

+++
### until

---
### Functions
