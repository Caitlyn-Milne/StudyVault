Dynamic programming is a way of making an [[Algorithm]] more efficent by storing itimidary results. 

Dynamic programming works well for [[Algorithm|algorithms]] with repetitive computations because as it prevents having to repeat the same computations again.

One method for creating a dynamic programming solution is first create a [[Recursion|recursive]] solution and then use the memoise results instead of creating a recursion call if the results exsit.

If a current result requires a previous result, sometimes a bottom up approach is better. A bottom up approach first starts with the base case, and computates each result untill the desired result. Doing things this way makes your code easier to understand and reduces recursive calls, however this is not ideal is all situations.