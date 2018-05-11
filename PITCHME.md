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
read -p "Enter password: " PASSW
```

  -s - Suppress output

```
echo "Enter password "
read -s PASSW
```

Note:
The read command can be used to stop a script at certain points for debugging. I usually use the variable "dummyvar" so I know at a glance what the read is for.
---
### Conditional Handling
*  if statement |

*  if else |

*  if elif |

*  case |

+++
### if statement
*  Uses a test with a binary output to determine path to take
-  Syntax
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
if [[ $i{ANSW} -lt 1 ]]
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
if [[ $i{ANSW} -lt 1 ]]
then
  echo "The command worked"
else
  echo "I can't find Hello anywhere"
fi
```

@[1](The command you are testing output from)
@[2](Special variables can be very volitile so I usually create a "disposable" variable to hold them)
@[3-4](The if statement and condition it is looking for)
@[5](If the condition is true, run this command)
@[6-7](If the condition is NOT true, run this command)
@[8](Close out the if statement)

+++
### if elif statement

+++
### case statement

---
### select case to create menus


---
### Loops
for

while

until

---
### Functions
