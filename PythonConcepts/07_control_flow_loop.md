---
id: 07_control_flow_loop
title: Loop
sidebar_label: Loop
slug: /python_Basics/07_control_flow_loop
---

---

In programming, there are various control structures which allows to execute statements sequentially. In Python, there are two keywords, which help you to make a loop structure, `for` and `while`.

### While Loop

```
# Up until the condition is True, the statements are executed.

while <condition>:
    statements

# There is a while-else expression in which when the condition is False, the statements inside the else are executed.

while <condition>:
    statements
else:
    statements
```

Examples:

```
num = 1

while num < 10:
    print(num)
    num += 1


(output): 1
2
3
4
5
6
7
8
9
```
```
num = 1

while num < 10:
    print(num)
    num += 1
else:
    print("That's the end!!")



(output): 1
2
3
4
5
6
7
8
9
That's the end!!
```

### For Loop

```
for iterative_var in seq:
    statements
```

Example:

```
# Creating a list of number from 0 to 9
list_1 = list(range(10))

for i in list_1:
   print(i)


(output):0
1
2
3
4
5
6
7
8
9
```

### Nested Loop

It is possible to use a loop inside another loop to execute more complex task.

### Loop control statements

There are some ways to change the execution in sequence of loop statements:

- `break`
- `continue`
- `pass`

#### break

We can use `break` to exit from loop whenever a desired condition is met.

```
# Creating a list of number from 0 to 9
list_1 = list(range(10))

for i in list_1:
   # Whenever i equals to 5, the loop is stopped
   if i == 5:
       break
   print(i)

(output):0
1
2
3
4
```

#### continue

The `continue` statement is used to skip one of the sequence of loop statement and continuing the its rest.

```
# Creating a list of number from 0 to 9
list_1 = list(range(10))

for i in list_1:
   # number 5 is not printed
   if i == 5:
       continue
   print(i)


(output):0
1
2
3
4
6
7
8
9
```

#### pass

The `pass` statement can be considered as a null statement. It is useful to use `pass` in our code where it will finally implemented, but the code has not been written yet.

```
# Creating a list of number from 0 to 9
list_1 = list(range(10))

for i in list_1:
   # Nothing happen
   if i == 5:
       pass
   print(i)


(output):0
1
2
3
4
5
6
7
8
9
```
