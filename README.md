# Recurrence Analysis -- Mystery Function

"I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice." 

Used prior work from: https://github.com/COSC3020/recurrence-analysis-Powerfuljackell-1
Watched this youtube video: https://www.youtube.com/watch?v=1K9ebQJosvo

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

$$ T(n) =
   \begin{cases}
       1 & n \leq 1\\
       3T(\frac{n}{3}) + n^5 & n > 1
   \end{cases}
$$

$T(n) = 3T(\frac{n}{3}) + n^5 $

$= 3 \cdot 3T( \frac{n}{3 \cdot 3} ) + 3( \frac{n}{3} )^5 + n^5$

$= 3 \cdot  3 \cdot 3T( \frac{n}{3 \cdot 3 \cdot 3} ) + 3 \cdot 3( \frac{n}{3 \cdot 3})^5 + 3( \frac{n}{3} )^5 + n^5$

$= 3 \cdot  3 \cdot 3T( \frac{n}{3 \cdot 3 \cdot 3} ) + 3 \cdot 3( \frac{n^5}{(3 \cdot 3)^5}) + 3( \frac{n^5}{(3)^5} ) + n^5$

$= 3 \cdot  3 \cdot 3T( \frac{n}{3 \cdot 3 \cdot 3} ) + \frac{3 \cdot 3n^5}{(3 \cdot 3)^5} + \frac{3n^5}{(3)^5} + n^5$

$= 3 \cdot  3 \cdot 3T( \frac{n}{3 \cdot 3 \cdot 3} ) + (\frac{3 \cdot 3}{(3 \cdot 3)^5} + \frac{3}{(3)^5} + 1) * n^5$

...

$= 3^i \cdot T( \frac{n}{3^i} ) + (\sum_{k=0}^{i-1} (\frac{3^k}{3^{5k}})) * n^5$

Test by plugging in 1 for i = $3T(\frac{n}{3}) + n^5$

for $i = logn$

$nT(1) + n^5 \cdot ( \frac{3^{log(n)-1}}{3^{5(log(n)-1)}} + 1)$ 
