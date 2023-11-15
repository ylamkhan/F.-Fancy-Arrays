It is difficult to directly calculate the number of arrays that satisfy both conditions. So let's calculate the opposite value — the number of arrays, where only the second condition is holds, and the first is necessarily violated.

Using the fact that the array can contain integers from two sets [0,x) and [x+k,∞).
We can notice that the array can consist of elements from only one set, but not both (because the difference between elements from different sets is at least k+1 which violates the second condition). So the answer to the problem is f(0,M −f(0,x−1)−f(x+k,M) , where f(l,r) is the number of arrays of length n that satisfy the second condition and elements in range from l to r , and M is some big constant (let it be equal to 10100).

Let's take a closer look at the function f(l,r).
We can represent the required array a as integer a1 and an array of n−1 differences Δi=ai+1−a1 .
There are (2k+1)n−1
differences arrays in total, because of the second condition. Let cnt(l,r,Δ) be the number of valid a1 for the given array Δ
(a1 is valid if it's produces array a , where all elements from l to r).
Using such a representation we can see that f(l,r)=∑Δcnt(l,r,Δ).
Moreover, let mn be the minimum value in Δ and mx
be the maximum value in Δ , then cnt(l,r,Δ) is equal to max(0,(r−l)−(mx−mn)).
It is difficult to calculate the values of f(0,M) and f(x+k,M) independently, because we can't iterate over all arrays Δ.
Luckily, our goal is to calculate their difference. Since the value of M is big enough, we can say that cnt of any Δ is positive. So we can represent f(0,M)−f(x+k,M) as ∑Δcnt(0,M,Δ)−∑Δcnt(x+k,M,Δ) or ∑Δ(M−0)−(mx−mn)−∑Δ(M−(x+k))−(mx−mn))
Since the Δ arrays are the same in both cases, we can combine the sums ∑Δ((M−0)−(mx−mn))−((M−(x+k))−(mx−mn))
Let's expand the brackets, and we get the final value f(0,M)−f(x+k,M)=∑Δx+k We can see that each Δ array adds x+k
to the difference between two values. So this part of the answer is equal to the (x+k)(2k+1)n−1.

It remains us to calculate the value of f(0,x−1).
We can do it using simple dynamic programming dpi,j — the number of arrays of length i if the last element is j.
The transition from (i,y) to (i+1,z) can be made if |y−z|≤k .
And the answer is equal to the sum of dpn,j for each j∈[0,x) Such dynamic programming works in O(nx), but n
is too big for this solution. However, thanks to fairly simple transitions, we can represent it as matrix multiplication. Using fast matrix exponentiation, we can calculate it in O(x3log(n)).
The total answer is (x+k)(2k+1)n−1−f(0,x−1).
