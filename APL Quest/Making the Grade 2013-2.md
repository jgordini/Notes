## [Making the Grade](https://problems.tryapl.org/psets/2013.html?goto=P2_Making_The_Grade)

**Problem:** Write a dfn which returns the percent (from 0 to 100) of passing (65 or higher) grades in a vector of grades.

**Video:** https://youtu.be/pxo2BtoMxP4
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/2.apl

**Example Solutions:**
2 Scaler functions and a reduction over a vectorized operation. 
```APL
F ← {100×(+/⍵≥65)÷≢⍵}
J ← 100×+.≥∘65÷≢ ⍝ Tacit
```

**Explanation:**
```APL
F ← {100×(+/⍵≥65)÷≢⍵}
```

1.  `(+/⍵≥65)` use [greater than or equal to](https://aplwiki.com/wiki/Greater_than_or_Equal_to) as a [Comparison Function](https://aplwiki.com/wiki/Comparison_function) returning a boolean vector of 1 if true and 0 if false. 
2. Then [sum](https://aplwiki.com/wiki/Reduce) the result - `+/`. 
3. `÷≢⍵`  [Tally](https://aplwiki.com/wiki/Tally) the length of your argument and divde that by the result in step 1. 
4. Multiply this by 100 to get your percentage of passing grades. 

**Performance:**
```APL
F ← {100×(+/⍵≥65)÷≢⍵} ⍝ n:≥ n-1:+ 1:÷ 1:×
G ← {100×+/(⍵≥65)÷≢⍵} ⍝ n:≥ n-1:+ n:÷ 1:×
H ← {+/100×(⍵≥65)÷≢⍵} ⍝ n:≥ n-1:+ n:÷ n:×
```
Note that it does not matter where we do the sum mathmatically. However there are siginificant performance penalties for summing after the division.

```APL
s←?1e6⍴100
'cmpx'⎕cy'dfns'
cmpx'F s' 'G s' 'H s'
⍝ F s → 6.6E¯5 | 0%
⍝ G s → 2.4E¯3 | +3451%
⍝ H s → 2.8E¯3 | +4126% 
```
We can evalute the performance of each function by importing the [CMPX](http://dfns.dyalog.com/n_cmpx.htm) function from the [DFNS](http://dfns.dyalog.com/n_contents.htm) library. 
1.  We [Roll](https://aplwiki.com/wiki/Roll)1 million `1e6` random numbers between 1 and 100
2.  We [copy](http://help.dyalog.com/latest/Content/Language/System%20Functions/cy.htm) `⎕cy` CMPX from the DFNS library into our workspace
3.  We use cmpx to evalute the performance of each function. With the first function as our baseline. 
```APL
F ← {100×(+/⍵≥65)÷≢⍵}
I ← {100×(⍵+.≥65)÷≢⍵}
J ← 100×+.≥∘65÷≢ ⍝ Tacit
K ← 100×+.≤÷≢⍤⊢
```

We are dealing with a scaler (65) and a vector (Scores). We should notice this pattern. We have a sum over a comparison of vectors. When we have that, we should think, [Inner Product](https://aplwiki.com/wiki/Inner_Product). 

1.  `+.≥`  Replace reduce in `+/` with inner product
2. (J) 65 is a [Bound](https://aplwiki.com/wiki/Bind) constant to the inner product allowing us to remove the parenthesis.
3. J is parsed as `{100×((⍵(+.≥)65)÷(≢⍵))}`

**Generalization:** Adding the cutoff point as an additional argument
1. K is parsed as `{100×((⍺(+.≤)⍵)÷(≢⍵))}` 
2. We are reversing the `≥` so that the Cuttoff Point (65) can be taken as the left argument. Represented by `⍺` in step 1. 
3. `≢⍤⊢` We use Atop so that we can apply [Tally](https://aplwiki.com/wiki/Tally) monadically. (Dyadic Tally is [Not Match](https://aplwiki.com/wiki/Not_Match)) We could also use Jot `≢∘⊢` in this case and achieve the same result. 


**Comment:** 
```APL
0,⍳64 ⍝ Raveld with zero becuase ⎕IO←1
```

**Glyphs Used:**
[Roll](https://aplwiki.com/wiki/Roll)
[Reshape](https://aplwiki.com/wiki/Reshape)
[Tally](https://aplwiki.com/wiki/Tally)
[Greater than or Equal to](https://aplwiki.com/wiki/Greater_than_or_Equal_to)
[Scan](https://aplwiki.com/wiki/Scan) - Plus Scan
[Quad](https://aplwiki.com/wiki/Quad_name)
[Bind](https://aplwiki.com/wiki/Bind)
[Atop](https://aplwiki.com/wiki/Atop_(operator))
[Identity](https://aplwiki.com/wiki/Identity)
[Diamond](https://aplwiki.com/wiki/Statement_Separator)
[Ravel](https://aplwiki.com/wiki/Ravel)
[Iota](https://aplwiki.com/wiki/Index_Generator)
[Without](https://aplwiki.com/wiki/Without) aka not
[Over](https://aplwiki.com/wiki/Over)
[Indices](https://aplwiki.com/wiki/Indices) aka Where

**Concepts Used:**
[Comparison Function](https://aplwiki.com/wiki/Comparison_function)
[Dfn](https://aplwiki.com/wiki/Dfn)
[Dfns Workspace](https://aplwiki.com/wiki/Dfns_workspace)
[Scientific Notation](https://mastering.dyalog.com/Data-and-Variables.html#data-and-variables-representation-of-numbers)
[CMPX](http://dfns.dyalog.com/n_cmpx.htm)
[Scalar Function](https://aplwiki.com/wiki/Scalar_function)
[Reduction](https://aplwiki.com/wiki/Reduce)
[Inner Product](https://aplwiki.com/wiki/Inner_Product)
[Dot Product](https://en.wikipedia.org/wiki/Dot_product)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Function Atop Tack](https://mastering.dyalog.com/Tacit-Programming.html?highlight=atop#function-atop-tack)
[Default Left Arguments](https://aplwiki.com/wiki/Dfn#Default_left_arguments)
[Fork](https://aplwiki.com/wiki/Train#2-trains) - 2 Train
[Boolean Mask](https://aplwiki.com/wiki/Boolean)
[Code Reuse](https://en.wikipedia.org/wiki/Code_reuse)
[Scalar Extension](https://aplwiki.com/wiki/Scalar_extension)
[Conformability](https://aplwiki.com/wiki/Conformability)



welcome to this second episode of the apl quest check out apl wiki for details today's quest is called making the grade it's the second problem from the 2013 apl problem solving competitions phase 1. here we are to write a function which takes a list of numbers representing the points that people scored on some type of test if they scored 65 or higher then they've passed in the test and we are to compute the percentage of people who passed let's start off by generating some test data so here are 10 scores between 1 and 100 and those that's succeeded in the test had scores 69 and 72. so we know how many scores there are in total and we can compare all these scores with 65 so if the test scores are greater than or equal to 65 then they have succeeded and this gives us a boolean vector indicating the ones and zeros the ones that have succeeded then we can sum the boolean vector to find out how many have succeeded and then we can divide that by the total number so this gives us a fraction and we can multiply that by 100 to get a percentage putting all this together we have the function f and and we take 100 multiplied by the sum of the scores that are larger than 65 divided by the total tally of scores that's the argument here not the variable t and we can try this on t and that gives us the correct thing now there's something here that's worth noting and we are doing a bunch of different operations on our data and while mathematically equivalent it is important which order we do this in in order to have the maximal performance so here are some variations of things that we could do in f we started off by the comparison and then we summed however we could also start off a bit differently so let's say that we start off by doing the comparison and then we divide by the total count then we sum and then we multiply by the 100. so this is mathematically equivalent but we'll see in a moment and it makes a big difference what we could also do is we could start off in the same way by computing the numbers greater than or equal to 65 we could divide by the total number of numbers then we could multiply by 100 and then sum again mathematically equivalent but this makes a difference in performance let's generate a bunch of test data so um here's some test data we're going to do random numbers between 1 and 100 but this time we're going to do a million of them i'm not going to print these out let's get in the com pair execution time utility from the defense workspace and then we're going to run f on these test scores and g on the test scores and h on the test scores and we'll see in a moment that there is a quite significant difference in the performance here so what is it that's actually going on in f we are doing if we call the number of uh of scores n we're doing n comparisons first and then we are doing n minus one additions we're doing one division and one multiplication so we can write this we're doing n comparisons right like this and then we are doing an n minus 1 summations and then we're doing one division and one multiplication in g we again start off the same way we're doing n comparisons and then but then we're dividing every comparison with the tally so that means we're doing n divisions and we're doing the summation after that so that's n minus 1 summations and finally we're doing one multiplication and in h here we are doing starting off the same way with an n comparisons then we're doing the n divisions and then we're doing n multiplications as well and finally we're doing n minus 1 at additions so while these are mathematically equivalent we can see that there's going to be a big difference in the performance and indeed an f is the one where we're doing the least amount of work so looking at f again we can come up with some variations and in the live chat event that happened last friday and there were a bunch of variations and they were all over this same theme and trying out various ways of expressing this so here we're doing dealing with a scalar the cutoff point 65 and a vector these are all the scores we should notice this pattern we have a sum over a comparison of vectors so it's two scalar functions a reduction over a vectorized operation and we have that and we're doing apl we should think inner product so we can take these and combine them like that and we can call this i so this is going to be the same we give the same result as before the test result here now why am i doing this this is because this allows us to move on to a tested solution that's really really neat notice that a tested solution expresses everything in terms of function application on the argument rather than explicitly stating the name of the argument so the argument here is omega and the function that's being applied to omega is the tally here the function that's being applied to omega is the inner product with 65 as a bound constant right argument to the inner product and that we can express as a tested function really neatly so we get rid of our braces the application of tally on the argument becomes just tally the application of the inner product with a bound right argument we use the bind operator to bind that right argument to the inner product and that allows us to get rid of all the noise right there it's going to have about the same performance but for those that like test programming this is very nice but we can also spot a thing here we bound the argument which is the cutoff point what if we want to generalize our our function such that we can take the cutoff point as an additional argument in apl it's common to have the main data as the right argument and various parameters as a left argument if any so we really want to move the 65 or whichever number we use as the cutoff over to the left side of course we can easily do this by flipping the direction of the comparison then the 65 can go on the left so the same but it's a tested function the problem is that we want the tally of only the right argument if we left it the way it is now it would be the mismatch whether or not they're different and of course they are different and we'll be dividing by zero which is not what we want so what we can do is that we add a little construct here and a top right so this applies tally magnetically on the result of choosing the right argument another way that we could generalize this is by saying the default cutoff point is 65 so we can go up and say instead of using 65 as a constant in here we supply it as a left argument but if no left argument is given then we use 65. so now we can say that the cutoff point is 65 we get the same result if instead we make the cutoff point 50 oops i made a mistake here oh yeah of course not t 50 and apply the function l um then it's 40 of the scores that are that pass and we have here 69 60 63 and 72 i'd like to show some some interesting different approaches to this problem since everything we did now was using the same empathic method basic method these are not efficient but nevertheless they're kind of eye-opening in completely different ways you can attack the problem the first one makes an assumption that all our scores are integers between 0 and 100 so we can generate our scores that would not pass and then we could remove all those scores that wouldn't pass leaving only those that do pass and now between this set difference um the the ratio and of the length of the set difference and the original is then the ratio of winners so we can take the winners and the original and do a ratio of length so this is the over operator we're applying tally on both arguments and then we're dividing them and that gives us our ratio and we can multiply by 100 so we can put this into a function here's our argument and a different approach to this is in using the interval index function so if we have our test scores here then we can put some interval cutoffs so let's say we put a cutoff of 20 and a cutoff of 65 and this gives us the indices of the intervals that these numbers fall in so 4 is below 20 so that's index 0. it's before the first one and 69 is is after 65 so this is one in the middle and then to the right of the last one is number two and 22 is right there in between however we only want one color so we can make a vector that has but one element and this gives us they're still indices but they also happen to be boolean because either something falls before the first cutoff or in the interval that's formed to the right of that cutoff inclusive so now we could sum this up and divide by uh the total number of uh of scores but let's do it a little bit differently instead we can use iota algebra again but this time magnetically and that's where this computes the indices of those that fulfill the requirement of being above 65 and now we can use the same method as we did above where we take this result and divide with uh over the tallies of the original and then we add the last thing so this is using where and the interval index so we can say it's 100 times this and of course for both s and t we could modify them to take an optional or required left argument so here are all the definitions that we did today compare them don't forget to check out what the performance looks like on the kind of data that you're running with thank you so much for watching 


