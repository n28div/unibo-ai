# Exercise Book

- [Exercises proposed and solved by professors](exercise_book.pdf)
  - [Solution to exercise 2.4 of the file](http://turingmachinesimulator.com/shared/vbwvbqjngd)
- [Binary addition on TM](http://turingmachinesimulator.com/shared/zjisqsfwgm)

# Exercises proposed during lessons of the Accademic Year 2020/21 - WIP

## Computational Model

### Exercise 1

Prove the uncompatibility of the halting problem, namely the fact that the function <img src="https://render.githubusercontent.com/render/math?math=halt(\alpha, x)"> defined by cases:
 - equal to 1 if <img src="https://render.githubusercontent.com/render/math?math=M_\alpha(x)"> terminates
 - equal to 0 otherwise

is uncomputable.

**Solutions:**
We show that from an hypotetical machine computing _halt_, calling it _Mhalt_, we can get another TM, call _Muc_, which computes the _uc_, and we know it cannot exist (_uc_ is by definition a function not computable by any TM).

Let us construct _Muc_ out of _Mhalt_:
 - on input _α Muc_ proceeds by calling _Mhalt_ on input _(α, α)_ and:
    - in case _Mhalt_ returns 0 (meaning that _Mα(α)_ diverges), _Muc_ outputs 1
    - otherwise, i.e. in the case in which _Mhalt_ returns 1 (meaning that _Mα(α)_ converges), _Muc_ knows that it can safely call U (the universal TM) on _(α, α)_ and that U will terminate its execution on that input (because what U does with input _(α, α)_ is to simulate the execution of _Mα(α)_), returning an output _b_. Now:
      - if _b=1_ then _Muc_ returns 0
      - if _b=0_ then _Muc_ returns 1
  - _Muc_ as we have just defined it is indeed a TM computing _uc_, but since we know that _uc_ is uncomputable, there is a contradiction and _halt_ itself is uncomputable.

### Exercise 2
Show that the function _inc_: N -> N such that _inc(n) = n+1_ can be computed in linear time by giving an explicit construction of a TM.

**Solution:**
At first we have to encode natural numbers as binary strings. We have two possibility:
  - traditional encoding: (e.g. 12 = 1100)
  - reverse encoding: (e.g. 12 = 0011)

If we choose to use reverse encoding the problem is quite simple. With a single tape TM we will need to pass through the whole input string from left to right only once, meaning in linear time. The transiction function will look as follows:

(qinit, ▷) → (q0, ▷, R)  
(q0, 0) → (q1, 1, L)  
(q0, 1) → (q0, 0, R)  
(q0, □) → (q1, 1, L)  
(q1, 0) → (q1, 0, L)  
(q1, 1) → (q1, 1, L)  
(q1, ▷) → (qhalt, ▷, S)

## Turing Machines

### Exercise 1
Write a TM which computes the sum of two binary numbers _a,b >= 0_.

[**Solution**](https://turingmachinesimulator.com/shared/zjisqsfwgm)

### Exercise 2
Write a TM for palindromes, i.e. a TM that accepts a binary string _w_ iff _w_ is a palindrome.

The alphabet Γ can be defined as {▷, 0, 1, □}, while the set of states Q is {qinit, qa, q0, q0a, q1, q1a, qb, qhalt}. The transition function δ is specified as follows:

(qinit, ▷) → (qa, ▷, R)  
(qa, 0) → (q0, ▷, R)  
(qa, 1) → (q1, ▷, R)  
(qa, □) → (qhalt, □, S)  
// 0 is read  
(q0, 0/1) → (q0, 0/1, R)  
(q0, □) → (q0a, □, L)  
(q0a, 0) → (qb, □, L)   
(q0a, ▷) → (qa, ▷, R)  
// 1 is read  
(q1, 0/1) → (q1, 0/1, R)  
(q1, □) → (q1a, □, L)  
(q1a, 1) → (qb, □, L)  
(q1a, ▷) → (qa, ▷, R)  
//  
(qb, 0/1) → (qb, 0\1, L)  
(qb, ▷) → (qa, ▷, R)  

This is not exactly the same proposed by professor, but I've tested it with [JFLAP](http://www.jflap.org/) and it works. Here it is my implementation. Keep in mind that in JFLAP Touring Machines start with the head pointing at the first character of the string. Also the string is not preceded by the starting charachter ▷, but it is fully surrounded with □. So I have replaced ▷ with x and I've made some changes to manage the different starting position of the head.

![image](https://user-images.githubusercontent.com/31796254/121325059-949ee380-c911-11eb-99f5-e55f8708864f.png)


### Exercise 3

Write a TM that accept a binary string _w_ iff the number of 0s in _w_ is equal to the number of 1s in _w_.

This was proposed as a homework problem, so there is no solution showed in class, but I've tested mine with [JFLAP](http://www.jflap.org/) and it works. As usual, keep in mind that in JFLAP Touring Machines start with the head pointing at the first character of the string. Also the string is not preceded by the starting charachter ▷, but it is fully surrounded with □. So I have replaced ▷ with x and I've made some changes to manage the different starting position of the head.

**Solution:**
The alphabet Γ can be defined as {▷, 0, 1, □}, while the set of states Q is {qinit, qa, qb, q0, q1, qhalt}. The transition function δ is specified as follows:

(qinit, ▷) → (qa, □, R)  
(qa, 0) → (q0, ▷, R)  
(qa, 1) → (q1, ▷, R)  
(qa, ▷) → (qa, ▷, R)  
(qa, □) → (qhalt, □, S)  
(q0, 0) → (q0, 0, R)  
(q0, 1) → (qb, ▷, L)  
(q0, ▷) → (q0, ▷, R)  
(q1, 0) → (qb, ▷, L)  
(q1, 1) → (q1, 1, R)  
(q1, ▷) → (q1, ▷, R)  
(qb, 0/1/▷) → (qb, 0/1/▷, L)  
(qb, □) → (qa, □, R)  

![image](https://user-images.githubusercontent.com/31796254/121327435-ba2cec80-c913-11eb-9865-52f90058d014.png)
[Another solution](http://turingmachinesimulator.com/shared/zxbtwcdkil)

## Undecidability

Determine which ones of the following problems are decidable:
 1. P = {_M_ | _L(M)_ infinite}
 2. P = {_M_ | PALINDROME ⊆ _L(M)_}
 3. P = {_M_ | _M_ has exactly 5 states}
 4. P = {_M_ | _L(M)_ = Ø}
 5. P = Ø

### 1.
**Claim**: P is undecidable.

**Proof**: By Rice's Theorem:
 1. P is **non-trivial**: 
    1. P ≠ Ø: if _M_ is a TM that accepts every string, then _L(M)_ is infinite, so it belongs to P.
    2. ∃ _M_ | _M_ ∉ P: if _L(M)_ = Ø (so _M_ is a TM which rejects every input), then |_L(M)_| = 1, so _L(M)_ is not infinite, and so _M_ not belongs to P.
 2. P is **extensional**: Assume _L(M)_ = _L(N)_ and _M_ ∈ P. We have to show that also _N_ ∈ P. Since _M_ ∈ P iff |_L(M)_| = ∞, and considering that _L(M)_ = _L(N)_ ⇒ |_L(M)_| = |_L(N)_|, then |_L(N)_| = ∞ ⇒ _N_ ∈ P. QED.


### 2.
**Claim**: P is undecidable.

**Proof**: By Rice's Theorem:
 1. P is **non-trivial**: 
    1. P ≠ Ø: if _M_ is the TM acceppting every string, then  PALINDROME ⊆ _L(M)_, and so _M_ belongs to P.
    2. ∃ _M_ | _M_ ∉ P: if _L(M)_ = {01} (which can be easily decided with a TM _M_), then _L(M)_ not contains PALINDROME, so _M_ not belongs to P.
 2. P is **extensional**: Assume _L(M)_ = _L(N)_ and _M_ ∈ P. We have to show that also _N_ ∈ P. Since _M_ ∈ P iff PALINDROME ⊆ _L(M)_ , we know that PALINDROME ⊆ _L(M)_ = _L(N)_, so PALINDROME ⊆ _L(N)_, then _N_ ∈ P. QED.

### 3.
**Claim**: P is decidable.

**Proof**: Trying to apply Rice's Theorem we can easily see that P is non-trivial, but **is not extensional**.
To demonstrate that it is decidable we have to design a TM that decides P. Decided a binary encoding for a TM, our TM take in input a string _w_ and it checks that _w_ is a valid encoding. If _w_ is invalid then it is rejected. Otherwise _w_ is acceppted iff it encodes a TM with exactly 5 states.

### 4.
**Claim**: P is undecidable

**Proof**: By Rice's Theorem:
 1. P is **non-trivial**: 
    1. P ≠ Ø: if _M_ is the TM rejecting every string, then _L(M)_ = Ø, and so _M_ belongs to P.
    2. ∃ _M_ | _M_ ∉ P: if _M_ is the TM acceppting every binary string, then _L(M)_ = {0,1}* ≠ Ø, so _M_ not belongs to P.
 2. P is **extensional**: Assume _L(M)_ = _L(N)_ and _M_ ∈ P. We have to show that also _N_ ∈ P. Since _M_ ∈ P iff _L(M)_ = Ø, we know that Ø = _L(M)_ = _L(N)_, so _L(N)_ = Ø, then _N_ ∈ P. QED.

### 5.
**Claim**: P is decidable

**Proof**: Trying to apply Rice's Theorem instantly fails because **P is trivial**. Indeed P = Ø by definition.
To show that P is decidable we have to design a TM that decides P and such a TM is the TM rejecting every input string.

## Polynomial Time Computable Problems

### Exercise 1
Prove that the function _minmax_ which given a list of natural numbers {_a1_, _a2_, ..., _an_} returns both the minimun and the maximum between _a1_, _a2_, ..., _an_ in in **FP**

**Solutions:**
We can describe the solution of this problem with a pseudocode:

```
input: (a1, a2, ..., an) appropiately encoded
output: (min, max)

min = a1			# 1 instruction
max = a1			# 1 instruction
for i <- 2 to n:		# For loop executed O(n) times. it contains at most 4 instructions
	if ai < min:
		min = ai
	if ai > max:
		max = ai
return (min, max)		# 1 instruction
```

 - The total number of executed instructions is _2 + 4*O(n) + 1 = O(n)_.
 - The size of the intermediate results can be bound as follows:
 	- min and max, being elements of the input list, are of course smaller or equal to the lenght of the input
 	- i, going to 2 to n, is of course smaller or equal to the input.
 - Each intruction executed by the algorithm takes polynomial time. Indeed, we have:
 	- assignements
 	- comparison between natural numbers of polynomial lenght.
 
 Altogether, this means that the described alogrithm works in polynomial time, and this mean that the function _minmax_ belongs to **FP**.

# Problem Examples from Virtuale 20/21 - WIP

Solutions provided are not _official_ solutions by professor, but are made by me. So be careful.

## Problem 1

Construct a deterministic TM of the kind you prefer, which decides the following language:

![L=\{w\in\{0,1\}^*\mid&space;w&space;$&space;does&space;not&space;contain&space;01&space;as&space;a&space;substring$\}](https://latex.codecogs.com/svg.latex?L%3D%5C%7Bw%5Cin%5C%7B0%2C1%5C%7D%5E*%5Cmid%20w%20%24%20does%20not%20contain%2001%20as%20a%20substring%24%5C%7D)

Study the complexity of TM you have defined.

### Solution

The alphabet Γ can be defined as {▷, 0, 1, □}, while the set of states Q is {qinit, q1, q2, q3, qhalt}. The transition function δ is specified as follows:

(qinit, ▷) → (q1, ▷, S)  
(q1, ▷) → (q1, ▷, R)  
(q1, 0) → (q2, 0, R)  
(q1, 1) → (q1, 1, R)  
(q2, 0) → (q2, 0, R)  
(q1, □) → (q3, □, L)  
(q2, □) → (q3, □, L)  
(q3, 0) → (q3, 0, L)  
(q3, 1) → (q3, 1, L)  
(q3, ▷) → (qhalt, ▷, S)  

If the TM reaches the ending state qhalt, then the string is accepted, otherwise, when the TM reaches a state where δ is not defined, the string is rejected.

Note that there are no transitions for the configuration (q2, 1), which corresponds to substring 01 detected.

When the TM read □ (i.e. the input string is finished), it goes to the state q3, in which it simply goes back to the starting position (the cell with ▷) and then it passes to the state qhalt, terminating and accepting the string. 

It follows a JFLAP implementation. As usual, keep in mind that in JFLAP Touring Machines start with the head pointing at the first charachter of the string. Also the string is not preceded by the starting charachter ▷, but it is fully surrounded with □. So I've made some changes to manage the different starting position of the head.

![image](https://user-images.githubusercontent.com/31796254/121328990-17756d80-c915-11eb-87fa-c8e993c55c85.png)

## Problem 2

You are required to prove that the following function _**f**_ is in **FP**. To do that, you can give a TMs or define some pseudocode.
The function is one that, given a list _L=L1,…,Ln_, returns its inverse, namely _Ln,Ln−1,…,L1_.

### Solution

First, we define a pseudocode that compute _**f**_:

```
def f (L=[L1,L2,...,Ln]):
  Reverse = new List[n]
  for i in range(n):
    Reverse[i] = L[n-1-i]
  return Reverse
```

Now we have to prove that this algorithm works in polynomial time. To do this we have to:

1. encode the input as a binary string. Our analysis of the time complexity will be done with respect of the length _l_ of such a string;
2. prove tha the number of instructions is bounded by a polynomial function in _l_;
3. prove that each instruction can be simulated by a TM in polynomial time
4. show that all the "intermediate" data and results use a space bounded by a polynomial function in _l_.

**Step 1**: In order to encode _L = [L1, L2, Ln]_ we need at first to encode its components _Li_. We can do it with one of the standards encoding of natural numbers in _{0,1}\*_.
Since using n bits allows us to encode _2^n - 1_ numbers, the encoding of _Li_ requires _log(Li) + 1_ bits.

Now we need to encode the whole list _L_. To do that we introduce a separator character # between elements of the list and then we encode 1 as 11, 0 as 00 and # as 01. So the total encoding will have length:

![l = \sum{i=1}^{n}{(2\log{L_i}+2)} + 2(n-1)](https://latex.codecogs.com/svg.latex?l%20%3D%20%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%7B%282%5Clog%7BL_i%7D&plus;2%29%7D%20&plus;%202%28n-1%29)

**Step 2**: The only relevant instruction is ```Reverse[i] = L[n-1-i]``` which is executed _n_ times, which is polynomial. Other instructions (updating i and similar) have also a polynomial bound and can be trivially translated in a polynomial number of TM steps.

**Step 3**: Let's suppose to have a TM with two tapes. On the first we have the input (_L_), on the second one we write the output. Let's suppose that the head of the first tape it's in the first cell (the one before the input) and the head of the second tape it is in the first blank cell after the output written until this moment. To execute ```Reverse[i] = L[n-1-i]``` we need to moove the head of the input tape until the end of the string (□ read) which takes at most _l_ steps, then we have to go back until we read 01 (the binary encoding for the separator #) which takes around _l/n_ steps. Now we can copy what we read in the first tape on the second tape, replacing all the cells in the first tape with □, which takes again around _l/n_ steps. Then we have to move the first head on the first cell again: _l_ steps in the worst case.
This algorithm, which is far to be the most efficient, takes _2l + 2l/n_ steps, which is polynomial in l.

**Step 4**: We never use more than _l_ cells in each tape.

## Problem 3

We studied the problem **CLIQUE**.
You are required to classify the subset **THREECLIQUE** of **CLIQUE** consisting of all the pairs **(_G_,3)**.
To which class does **THREECLIQUE** belong? 

### Solution

**THREECLIQUE** is a way simpler problem than **CLIQUE**. In fact we can solve it with the algorithm described by this simple pseudocode:

```
def threeclique(V, E):
  for u in V:
    for v in V - {u}:
      for w in V - {u, v}:
        if (u,v), (v,w) and (u,w) belongs to E:
          return true
  return false
```

Checking if an edge belongs to the set of edges of the graph can be done by simpling comparing it with alle the m edges of the graph, which can be done in polynomial time.
This operation is inside a triple nested ```for```, so it will be done a very big number of times, but still polynomial. SO the problem belongs to the **P** class.


# Question Examples from Virtuale 20/21

Let _f, g_ be the functions defined as ![f(n)=2^nn^2](https://latex.codecogs.com/svg.latex?f%28n%29%3D2%5Enn%5E2) and ![g(n) = n2^n](https://latex.codecogs.com/svg.latex?g%28n%29%20%3D%20n2%5En).  
Select one or more.
- [x] ![f\in\Omega(g)](https://latex.codecogs.com/svg.latex?f%5Cin%5COmega%28g%29)
- [ ] ![f\in O(g)](https://latex.codecogs.com/svg.latex?f%5Cin%20O%28g%29)
- [ ] ![f\in\Theta(g)](https://latex.codecogs.com/svg.latex?f%5Cin%5CTheta%20%28g%29)

- - - 
In Turing Machines:  
Select one or more.
 - [ ] The presence of many tapes can make the class **P** different
 - [x] What can be computed in exponential time is different from what can be computed in polynomial time
 - [x] The presence of many tapes can make the class **DTIME(_n_)** different
 - [ ] The class **EXP** can be equal to **P**

- - -
The problem **3SAT** is:  
Select one or more.
 - [x] Such that **INDSET** can be reduced to it
 - [x] **NP**-hard
 - [x] In the class **EXP**
 - [ ] Computable in polynomial time

- - -
Suppose a language **_L_** is both in **NP** and in **EXP**. Then  
Select one or more.
 - [ ] **EXP** and **NP** are necessarly equal.
 - [x] **_L_** can even be **NP**-complete.
 - [x] **NP** and **EXP** are maybe different.
 - [ ] **_L_** cannot be in **P**.

- - -
The notion of PAC-learnable concept class:  
Select one or more.
 - [x] Needs to hold for every distribution D on the instance class.
 - [x] Does not make any reference to the time complexity of the learning algorithm.
 - [ ] Requires the output concept to have probability of error ε, in all cases.
 - [ ] Cannot be reached when the underlying concept class is the one conjunctions of literals.

# Problems from Exam 06/26/2020

## Problem 1

Give a TM to decide _**L**_= set of strings for which if 01 is present, then is followed by all 0s.

### Solution

The alphabet Γ can be defined as {▷, 0, 1, □}, while the set of states Q is {qinit, q1, q2, qhalt}. The transition function δ is specifies as follows:

(qinit, ▷) → (q1, ▷, S)  
(q1, ▷) → (q1, ▷, R)  
(q1, 0) → (q2, 0, R)  
(q1, 1) → (q1, 1, R)  
(q2, 0) → (q2, 0, R)  
(q2, 1) → (q3, 1, R)  
(q3, 0) → (q3, 0, R)  
(q1, □) → (q4, □, L)  
(q2, □) → (q4, □, L)  
(q3, □) → (q4, □, L)  
(q4, 0) → (q4, 0, L)  
(q4, 1) → (q4, 1, L)  
(q4, ▷) → (qhalt, ▷, S)  

If the TM reaches the ending state qhalt, then the string is accepted, otherwise, when the TM reaches a state where δ is not defined, the string is rejected.

States explanantion:
  - **qinit**: it is just the initial state. The TM immediately passes to q1.
  - **q1**: the TM read the string charachter by charachter. If it read 0, it passes to q2.
  - **q2**: as q1, but a 0 has been detected yet, so reading a 1 will mean that 01 is detected and the TM will pass to q3.
  - **q3**: 01 detected, so the TM only reads 0s, indeed there are no transitions for the configuration (q3, 1).
  - **q4**: This state is reached when the TM reads a blank charachter, meaning that the string is finished and has to be accepted. It just reset the head at the start of the tape, before passing to qhalt, which is the final state.

When the TM read □ (i.e. the input string is finished), it goes to the state q3, in which it simply goes back to the starting position (the cell with ▷) and then it passes to the state qhalt, terminating and accepting the string. 

## Problem 2

Prove that the problem is in **NP**: check if a number is the sum of powers of 3 by giving a TM or pseudocode.
(Asked to the professor, he said that 3^0 is not allowed as the problem would be trivial).

### Solution

We at first notice that a number can be expressed as a sum between power of 3 (3 to the power of 0 excluded) iff it is divisible by 3.
Since we have to show that the problem is in **NP** we can describe a non-deterministic algorithm. So our algorithm can just pick a random number non-deterministically, multiply it by 3 and check if it is equal to the input number n.
The multiplication and the comparison between two numbers can be of course executed in polynomial time.
The pseudocode is the following:
```
def f(n):
  assign non-deterministically a number greater than 0 to k
  k = k * 3
  return k == n
```

## Problem 3

PP is the set of theorems expressed in the Principia Matematica, published by Bertrand Russel in 1909-13. Do they fall in a complexity class? Motivate

### Solution
This formulation of the problem (which is indeed a reformulation by a student) is actually a bit tricky and it would require to know all the algorithm of the book to establish to which subset of **NEXP** the algorithms belong (**NEXP** is a set enough big to make us quite sure that all the algorithms in that book belong to it).

However, I've found similar exercises with the original formulations of the professor, which are more clear. The problem asks to establish which is the complexity of establishing if an algorithm (which is given in input with some binary codification) belongs to PP.

This can be achieved comparing (in linear time) it with all the algorithms of the book (which are a constants number), so of course is a **P** problem.



# Problems from the exercise book

## The computational model

### Exercise 2.1

[This Turing Machine right here.](http://turingmachinesimulator.com/shared/cacvifsuib)

### Exercise 2.2

[This Turing Machine right here.](http://turingmachinesimulator.com/shared/gomvaerezb)

### Exercise 2.4

[Two-taped solution](http://turingmachinesimulator.com/shared/zphovjeoro)

## Polynomial time computable problems

### Exercise 3.1

We are basically psudo-coding a linear search. The first thing we'll have to do is encoding the input as binary strings. This is pretty straightforward: we can introduce a separator `#` that separates the elements of the list, and finally, the query.

The list would therefore be encoded as follows:

$l_1\#l_2\# ...\#l_n\#q$

Now, we know that the saving of a given natural number requires $roundToNextInt(l_i)$ bits, and our encoding will be the following: `0=00,1=11,#=01`. This means that every *normal* bit will require twice the space, and we will have $n$ separators occupying 2 bits each. 

We can now introduce the pseudocode solving the problem:

```
def linsearch(List[Int] l, int query) {
	i = 0
	while i<|l| {
		if (l[i] == query) {
			return i
		}
	}
	return -1
}
```

Now, the analysis of the code. We know that the first instruction is $O(1)$. The `while` loop, then, is executed **at most** $|l|$ times, and contains three (the while check, the if, the return) constant instructions. The final instruction is still constant.

This means that, finally:
$$
O(1)+O(n)O(3)+O(1) = O(n)
$$
The intermediate results are clearly bounded: the list will never exceed its original size (nor get modified) and i is an int.

Since $n$ is clearly polynomial, we have proven the presence in $FP$.

A TM could simulate this code by simply having the same input we cited before, as $l_1\#...\#l_n\#q$, scrolling to the end of the TM, copying the query to another tape, then searching for the element while saving the index in a third tape (incremented at every separator).

## Between the feasible and unfeasible

### Exercise 4.1

We know that a language is in NP when:
$$
\mathcal{L} = \{x\in \{0,1\}^* | \exist y \in \{0,1\}^{p(|x|)}.(x,y)=1\}
$$
Therefore, we can introduce a TM $\mathcal{M}_a$ that verifies the language $\mathcal{L}_1$ and a TM $\mathcal{M}_b$ that verifies $\mathcal{L}_2$. Now, if we introduce a third TM that, given a triple $(x,y_1,y_2)$ emulates the first one on $(x,y_1)$ and the second one on $(x,y_2)$, ultimately returning $1$ if and only if both the emulations do so.



