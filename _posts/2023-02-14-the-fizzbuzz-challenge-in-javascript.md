---
layout: post
---


When we talk about a problem that's very common in an interview, we assume we already know how 
to code and solve it. We can discuss some of the most popular problems, like the fibonacci algorithm, plenty of sorting algorithms, etc. and that's a true thing. 

We surely don't know how many problems are but, I'll explain u (by my words) one problem very popular (and often is memed by the community) that's in the 98% of the times, it'll be a question you need to solve by hand in less than 5 min (well, that's the most accurate number tho). This problem's called: The FizzBuzz. 

This article will be relately short, but I'll explain the problem and how to solve it in JavaScript. I'll start saying that this problem is very simple, but it's a good way to test your logic and your ability to code it in the less time possible. 

I'll not use any GUI tools to explain the algorithm, since it's very easy. The thing is that there's lots of ways to solve this problem and each programmer has his own way to solve it according to his logic, so there's no "the best way" to solve it or, a unique rule to follow and if u don't follow it, u are disordering the time-space continuum and the universe will collapse. lol

Nah, just kidding (or not). Well, let's start. First of all, what is the FizzBuzz problem? This problem consists in a simple algorithm that prints the numbers from 1 to 100, but if the number is divisible by 3, it outputs "Fizz" instead of the number, if the number is divisible by 5, it outputs "Buzz" instead of the number and if the number is divisible by 3 and 5 (or 15), it outputs "FizzBuzz" instead of the number.

Seems easy, right? Well, as I said, there's lots of ways to solve this problem, but I'll code it in some ways I thought of. Check this out: 
    
```js
// By Yayo
const fizzbuzz = (n) => {
    for (let i = 1; i <= n; i++) {
        if (i % 15 == 0) console.log('FizzBuzz');
        else if (i % 3 == 0) console.log('Fizz');
        else if (i % 5 == 0) console.log('Buzz');
        else console.log(i);
    }
}

```

If you already know JavaScript, you are just noticing I did an if sentence. To reduce lines, I didn't use curly brackets (yea, Python memories lol). But you can use them:
    
```js
// By Yayo
const fizzbuzz = (n) => {
    for (let i = 1; i <= n; i++) {
        if (i % 15 == 0) {
            console.log('FizzBuzz');
        } else if (i % 3 == 0) {
            console.log('Fizz');
        } else if (i % 5 == 0) {
            console.log('Buzz');
        } else {
            console.log(i);
        }
    }
}

```

Let's see what happens if we call this function with the number 100 (well yea, it's 1 to 100). 

```
$ node some_code.js
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
16
17
Fizz
19
Buzz
Fizz
22
23
Fizz
Buzz
26
Fizz
28
29
FizzBuzz
31
32
Fizz
34
Buzz
Fizz
37
38
Fizz
Buzz
41
Fizz
43
44
FizzBuzz
46
47
Fizz
49
Buzz
Fizz
52
53
Fizz
Buzz
56
Fizz
58
59
FizzBuzz
61
62
Fizz
64
Buzz
Fizz
67
68
Fizz
Buzz
71
Fizz
73
74
FizzBuzz
76
77
Fizz
79
Buzz
Fizz
82
83
Fizz
Buzz
86
Fizz
88
89
FizzBuzz
91
92
Fizz
94
Buzz
Fizz
97
98
Fizz
Buzz
$
```

Damn well, that's a lot of outputed lines. What we can do in this case? Let's try creating an array which all the output will be stored in it and then, we'll print the list. 

```js
// By Yayo
const fizzbuzz = (n) => {
    let array = [];
    
    for (let i = 1; i <= n; i++) {
        if (i % 15 == 0) array.push('FizzBuzz');
        else if (i % 3 == 0) array.push('Fizz');
        else if (i % 5 == 0) array.push('Buzz');
        else array.push(i);
    }
    return array;
}

console.log(fizzbuzz(100));
```

Now, let's see what happens if we run this code. 

```
$ node some_code.js
[
  1,      2,      'Fizz',     4,      'Buzz', 'Fizz',
  7,      8,      'Fizz',     'Buzz', 11,     'Fizz',
  13,     14,     'FizzBuzz', 16,     17,     'Fizz',
  19,     'Buzz', 'Fizz',     22,     23,     'Fizz',
  'Buzz', 26,     'Fizz',     28,     29,     'FizzBuzz',
  31,     32,     'Fizz',     34,     'Buzz', 'Fizz',
  37,     38,     'Fizz',     'Buzz', 41,     'Fizz',
  43,     44,     'FizzBuzz', 46,     47,     'Fizz',
  49,     'Buzz', 'Fizz',     52,     53,     'Fizz',
  'Buzz', 56,     'Fizz',     58,     59,     'FizzBuzz',
  61,     62,     'Fizz',     64,     'Buzz', 'Fizz',
  67,     68,     'Fizz',     'Buzz', 71,     'Fizz',
  73,     74,     'FizzBuzz', 76,     77,     'Fizz',
  79,     'Buzz', 'Fizz',     82,     83,     'Fizz',
  'Buzz', 86,     'Fizz',     88,     89,     'FizzBuzz',
  91,     92,     'Fizz',     94,     'Buzz', 'Fizz',
  97,     98,     'Fizz',     'Buzz'
]
$
```
Much better eh? This array shows every value I push into it, as you see. Also, it's more readable for a user to check all the code's output, because if output every value in a single new line, it would be a mess, but also for a user could be boring to check every value by scrolling the terminal. 

You need to scroll it anyways lol, but it's more readable, clearner and easier to check and evaluate the outuput. You might use the switch sentence also to create conditional statements. In this case, for the fizzbuzz challenge. 

```js
// By Yayo
const fizzbuzz = (n) => {
    let array = [];
    
    for (let i = 1; i <= n; i++) {
        switch (true) { 
            case i % 15 === 0: array.push('FizzBuzz'); break;
            case i % 3 === 0: array.push('Fizz'); break;
            case i % 5 === 0: array.push('Buzz'); break;
            default: array.push(i);
        }
    }
    return array;
}
```
The output is the same as the previous code I showed you. You can try it by yourself if you want!, also to see the difference between the switch sentence and the if sentence, but also to think about the best way to solve this problem for yourself. 

Now, I'ma explain you some JS basics. To declare a function, you might use the function keyword, like this: 

```js
function some_function() {
    // Code here
}
```
Like in other languages, there's a key reserved word to declare a function, but in JS, you can also use the arrow function, like this: 

```js
const some_function = () => {
    // Code here
}
```
The arrow function is a new way to declare a function in JS, and it's more used than the function keyword. The ```const``` keyword is used to declare a constant. This constant is only read-only, so you can't change it's value. Also you can't redeclare it with another value, so because of this, the ```const``` form will only be read-only what's inside the function's code. 

If you want to declare a variable, you might use the ```let``` keyword. This variable can be changed, so you can redeclare it with another value. I used it to declared the ```array``` variable, because I wanted to change it's value (pushing new items), so I used the ```let``` keyword. 

If you wanna learn more about JS, I recommend you to check the [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript) or the JavaScript [documentation](https://devdocs.io/javascript/). Thanks for reading this, and I hope you learned something new. :)
