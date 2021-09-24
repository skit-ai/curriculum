# What is debugging?
Debugging is an action of removing issues or potential errors that can cause your code to crash or have unexpected behavior. So this post is about ways to debug code.

Programming allows you to think about thinking, and while debugging you learn learning. Here are some of the ways you
can debug your code.

1. Adding print statements or logger to your code Whenever writing code the best practice is to put enough print
   statements/loggers in the code so that if there are issues in they could be caught while the development process and
   get fixed. Here is an example of a piece of code with print statements

```
def my_fact(numb) -> int:
    if numb is 1:
        return numb 
    else:
        return numb * my_fact(numb - 1)

if __name__ == '__main__':
    num = input("Enter the number you want to calculate factorial for: ")
    if isinstance(num, str):
        try:
            num = int(num)
        except ValueError as e:
            print("Unable to convert to integer, Exception: {}".format(e))
    else:
        print("Please input an Integer")
    if isinstance(num, int):
        factorial = my_fact(num)
        print("Factorial is: {}".format(factorial))
```

Another way to debug is adding loggers, one awesome library in python is Loguru, here is the same code snippet with
loguru.

```
from loguru import logger
 
def my_fact(numb) -> int:
    if numb is 1:
        return numb
    else:
        return numb * my_fact(numb - 1)
 
if __name__ == '__main__':
    num = input("Enter the number you want to calculate factorial for: ")
    if isinstance(num, str):
        try:
            num = int(num)
        except ValueError as e:
            logger.error("Unable to convert to integer, Exception: {}".format(e))
    else:
        logger.info("Please input an Integer")
 
    if isinstance(num, int):
        factorial = my_fact(num)
        logger.debug("Factorial is: {}".format(factorial))

```
<img src="https://dimplemathewblog.files.wordpress.com/2021/08/img_0016.jpg?w=1024"/>
The advantage to adding a logger is that you would know where the code is breaking and also most of the logger libraries
have different levels of logging:

- info 
- error
- debug

2. Python PDB module The pdb module in python helps debug the source code.

    For python 2.7 and above there is a package called pdb which you can use for debugging your code. To use this you need
    to add import pdb; pdb.set_trace() to the code where you need to examine the variables and their value. This is just
    like adding a breakpoint to your code. A breakpoint is used for suspending the program execution, post that you can
    examine the code line by line. Following is the implementation of adding breakpoint:

```
...
 
   if isinstance(num, int):
       import pdb; pdb.set_trace()
       factorial = my_fact(num)
```

Next, you need to run your code:
```
python factorial.py       
Enter the number you want to calculate factorial for: 5
> /Users/dimplemathew/PycharmProjects/pythonProject2/factorial.py(23)<module>()
-> factorial = my_fact(num)
(Pdb) 
```

You will see something similar to  ☝️   in your terminal. It shows the path of the file along with the line number where
the breakpoint is added.
```angular2html

(Pdb) p num
5
```

Next to know the value of the variables you can use ‘p <variable_name’> to get the value. If you are using python 3 and
above you need not import pdb instead just add a breakpoint() where every you want in your source code. Below is the
implementation:
```angular2html
...
 
if isinstance(num, int):
    breakpoint()
    factorial = my_fact(num)
```

For further read, here is the link to the [documentation](https://docs.python.org/3/library/pdb.html)
