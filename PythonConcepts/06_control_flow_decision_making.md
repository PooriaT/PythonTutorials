---
id: 06_control_flow_decision_making
title: Decision Making
sidebar_label: Decision Making
slug: /python_Basics/06_control_flow_decision_making
---

---

In programming, with `if` statement, it is possible to provide the decision-making statement:

```
# if statement
if <condition>:
   statements

# if else statement  
if <condition>:
    statements
else:
    statements

# if elif else statement
if <condition>:
    statements
elif <condition>:
    statements
.
.
.
else:
    statements

# Nested if statement

if <condition>:
    if <condition>:
        statements
    elif <condition>:
        statements
    else:
        statements
elif <condition>:
    if <condition>:
        statements
else:
    if <condition>:
        statements
```

Example:

```
# Finding a given number is odd or even

num = 14

if num % 2 == 0:
    print(str(num) + " is even")
else:
    print(str(num) + " is odd")


(output): 14 is even
```
