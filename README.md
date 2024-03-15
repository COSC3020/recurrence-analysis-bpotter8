[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

Answer:

As the mystery function is run, it recursively calls itself 3 times. As it calls itself, it divides the n by 3. This is equivilent to $3 \cdot T(\frac {n} {3})$.

In the mystery function, there is 3 nested for-loops. 

The first for-loop runs from 0 to n*n. This is equal to $n^2$.

The second for-loop runs from 0 to n. This is just equal to $n$.

The third for-loop runs from 0 to n*n again. This is also equal to $n^2$.

If we multiply, $n^2 \cdot n \cdot n^2 = n^5$.

So, the recurrence relation is equal to $T(n) = 3 \cdot T(\frac {n} {3}) + n^5$.

If we use the master theorem,

a = 3, b = 3, and d = 5.

Since $d > log_{3} 3$, T(n) = big-O $(n^5)$.

The runtime is big-O $(n^5)$.

The base case is when $n \leq 1$.

To solve this without the master theorem, we go through the function step by step.

First, we have $n^5$

Then, we have $3 \cdot (\frac {n} {3}) ^ 5$

Then, we have $3^2 \cdot (\frac {n} {3^2}) ^ 5$ 

Finally, we have $3^x \cdot (\frac {n} {3^x}) ^ 5$ 

So, $n^5 + 3 \cdot (\frac {n} {3}) ^ 5 + 3^2 \cdot (\frac {n} {3^2}) ^ 5 + ... + 3^x \cdot (\frac {n} {3^x}) ^ 5$

The function will not grow faster than $n^5$.

So, the runtime is big-O $(n^5)$.






