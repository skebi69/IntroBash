# Intro to BASH Shell Scripting
## John Kennedy
### skebi69@gmail.com

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
-   She Bang - Not Ricky Martin (see - I told you I was old) |
-   Variables |
-   Special variables |
-   User input |

+++
### Topics (Cont)
-   Conditional handling |
    -   if statement |
    -   if else |
    -   if elif |
    -   case |
-   Select/case text menu |

+++
### Topics (Cont)
-   Loops |
    -   for |
    -   while |
    -   until |
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
-   Start every script to set interpreter
-   #!/bin/bash

---
### Variables
-   A temporary store for small pieces of information
-   No need to declare
-   Can contain any type of data - String, integer, float, etc

---
### Special variables
-   $? - Exit code of last command
-   $0 - Script name
-   $1 - $N - Option 1 to whatever
-   $$ - PID of script

---
### User input
-   read command
-   read <options> variable
    -   Options
    -   -p - Prompt
```
read -p "Enter password:" PASSW
```
    -   -s - Suppress output
```
echo "Enter password"
read -s PASSW
```
