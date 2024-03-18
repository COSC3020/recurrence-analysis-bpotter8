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

$T(n) = 3 \cdot T(\frac {n} {3}) + n^5$

$= 3 (3 T (\frac {\frac {n} {3}} {3}) + (\frac {n} {3})^5) + n^5$

$= 9 T (\frac {n} {9}) + 3 (\frac {n} {3})^5 + n^5$

$= 9 (3 T (\frac {\frac {n} {9}} {3}) + (\frac {n} {9})^5) + 3 (\frac {n} {3})^5 + n^5$

$= 27 T (\frac {n} {27}) + 9 (\frac {n} {9})^5) + 3 (\frac {n} {3})^5 + n^5$

$= 3^i T (\frac {n} {3^i}) + \sum_{j=0}^i  3$ ^ (i-1) * (n/3^(i-1))^5 + $n^5$

$i = log_3 n$

= 3 ^ $log_{3} n$ $\cdot T (\frac {n} {3^log_3 n}) + \sum_{j=0}$ ^ $(log_3 n)$  3 ^ $(log_3 n - 1)$ * ($\frac n 3$ ^ $(log_3 n - 1)$ )^5 + $n^5$

$= n \cdot 1 + n^5$

Since $n^5$ is the most dominant, the runtime is big-O ($n^5$).
