---
layout: post
tags: [C, C++]
author: Luis De León
---


Programming is like a cooking recipe. There's a set of instructions in which, you need to follow to solve an specific problem, or to perform a task. And each task in this case, will conform the whole cooking recipe. 

Wanna make a pizza? You need some ingredients (Which from now, I'm gonna call 'em as objects to be in reference): Cheese, Tomato sauce, Pizza dough, etc. You need to assemble all ingredients and then bake it. But I'll ask u something: Don't u ever took how much time did u last making all that pizza? 

In programming, it works similar, but at the time we are coding, we can figure out why our code is taking so much long time to execute, compile, etc. Or the opposite way: Why our code is running so fast, even before noticing how many code lines we wrote?

That's a hard truth when we are talking about algorithms. I know that debugging a +10000 line code program is really difficult, frustating and also takes a lot of time in terms of releasing a project or adding new updates to that project. To avoid that (or maybe, to invest better our time doing more effectively code) we need to think how we can solve an specific problem in less time possible according to the number of statements that conforms a task, not the time that statement needs to be done.  

To measure it, we as programmers use something we call Time Complexity. And yea, the less tasks needed to be done, better. To understand it, I'll explain very simple how each complexity works with it's respective snipet code. It should be noted that I'll put C code. 

Check this out (resuming all complexities and what the O means):
- 0(1): Constant (Very Good)
- O(Log(N)): Logaritmic (Very Good)
- O(N): Linear (Good)
- O(Nlog(N)): Linearithmic (Good)
- O(N^2): Quadratic (Not good)

These are the most common ones according to the Big O Notation syntax. Notice the last word I put in each time complexity. To summarize it, simplifies the time of an algorithm with that complexity should take. But yea, I'll explain each one with an example. 

* * *

### O(1)

Refers an algorithm that doesn't need to loop or to iterate an object, which means to be constant. A constant object is an inmutable object (can't be modified), so if are outputing something or doing a conditional statement, remember that those objects once outputed can't be modified unless u modify ur code. 

Check this simply code:

```c
// By Yayo
#include <stdio.h>

int main(int argc, char* argv[]) {
    int number = 4;
    
    if (number < 5) {
        printf("This number is lower than 5\n");
    } else {
        printf("This number is higher than 5\n");
    }

    return 0;
}
```
When I run this, it should showed me something like this: 

```
$ gcc some_code.c -o main && ./main
This number is lower than 5
$
```

Very simple. It's just a conditional statement outputing something, but to put u in reference, there's no a loop conditional inside a block of code we need to execute, so it takes less than 14 nanoseconds to output a string object. If u don't understand what are the main function's args, check this [doc](https://linuxhint.com/argc-argv-cpp/), it's the same for C and C++. 


### O(Log(N))

This time complexity is often confused with the O(1) runtime complexity, but it's not as close as you think, because in this complexity, a programmer is are aware of how much times he needs to iterate an object. This means that it's not necessary to iterate the whole object as a linear algorithm (more about this below), but it's better than that:

Imagine you have an array of 10 elements and you wanna find one of these elements but u don't know in which index it is. What we can do? 

First you need to understand that this array was sorted previously, so you don't have to sort it at the time you are looking for that element. And.. also, also u wanna find this element in the less time posible, 'cause you don't wanna wait for the next day at the time u read 34 books, played CSGO 3 hrs and u ate 4 times per hr lmao. 

Ya being serious, you don't need to iterate the whole array, so for this, I'ma explain y'all what is the Binary Search algorithm, which is a perfect example to explain this complexity. 

The main idea for this algorithm is to guess this item by dividing the given array into 3 parts. Why 3 parts? Imagine that a user chose 2 incorrect items, one is lower and the other one is higher from the number you chose at the beginning. By default, we can trash the array's part that's lower and the part that's higher. So for example, my item is 45, the incorrect items are 25 and 47, and the array's range is between 0 and 50, we need to trash the range 0-25 and 47-50. Therefore, the left range is between 26 and 46. At this time we can iterate the whole array asking this question to the program whether the item chosen is the range given or not and dividing it if it's necessary. 

I'ma code this recursively because at the time we are calling the function in each statement, we are trimming the array. In the worst case, we'll trimmer the whole array until we find the item. 

```c
// By Yayo
#include <stdio.h>

int binary_search(int array[], int len, int piv, int search) {
    if (piv == -1 || piv == len + 1) {
        printf("\nNumber out of range\n");
        return 1;
    } else {
        if (search >= array[piv]) {
            return binary_search(array, len, piv - 1, search);
        }
    }
    return binary_search(array, len, piv + 1, search);
}

```

There's no main function to call the ```binary_search(int array[], int len, int piv, int search)``` method because I wanna emphasize in the algorithm snippet code. I called the method each time we trimmer the array, as I mentioned before. That's why, I add and substract the pivot just one element in each call. If the item is not located in the array, the program ends. 

Also, as I said, I used recursion but we can also iterate the whole array using loops. You can code it by yourself, but this code could represent how the program iterates and divides the array to find the item. But I'ma use maths instead. 

Let's say we divide an 10 element array into 2 parts, by choosing a pivot (Literally what I explained before). We divide it and then, we choose the item array[6], which is the item 30 and we wanna locate where it is. 

Given the array {3, 4, 10, 23, 25, 29, 30, 56, 77, 90}, check this: 

```
 0  1  2   3   4   5   6   7   8   9
{3, 4, 10, 23, 25, 29, 30, 56, 77, 90} 
               ^^
Item chosed: 25 == 30? False   ->  10 * (1 / 2) = 5 

 5   6   7   8   9
{29, 30, 56, 77, 90}
             ^^
Item chosed: 77 == 30? False  ->  5 * (1 / 2) = 2.5 

 5   6   7
{29, 30, 56}
     ^^
Item chosed: 30 == 30? True  ->  2.5 * (1 / 2) = 1.25 

 6
{30} = [6]
```

This is the "GUI" explanation of the code. Notice the end value doesn't end in 1. Why?
