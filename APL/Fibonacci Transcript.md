Welcome to the APL quest. See APL Wiki for details. Today we're going to compute the Fibonacci sequence.

Note that we are computing the first n elements of the sequence and not the nth element, which is a more usual task. So the Fibonacci sequence is usually defined as being recursive. The way it's defined is that we start off with some seed values and then we compute the next value by summing the last two values in the sequence.

We can express this as with a stopping condition. So if we start off the sequence with zero and one for the Fibonacci sequence and that in that case we say that for the first zero elements we don't need anything at all. We can just return zero.

And for the element number one we want a one. When we summon them together, we get the zero and the one and that gives us a one and then one and one gives two and so on. So if the argument is less than or equal to one, that means it's zero one.

Then we can return the element itself. Otherwise we want the sum of the function itself applied to each one of the argument, minus one and two. So we can try this on one, two, three and so on.

But we don't want the nth element, we want all the elements up to end. So we can apply this on each of the numbers here. While this works, it is exceedingly inefficient.

Not only do we compute the same sequence over and over again for n minus one and n minus two for every element of the sequence, we're also doing this whole thing over and over again and this becomes ridiculously slow very quickly. So that's not a good way to do it, but it very clearly expresses what the sequence is about. Instead we're going to focus on computing the entire sequence at once.

And the way we're going to do that is by using what I call a fundamental Fibonacci transformation function. Let's call that delta. The fundamental function is that we are extending the current generator sequence with one more element by summing the last two elements of the current sequence.

So the current sequence concatenated to the sum of the last two elements taken from the current sequence. And so if we start by applying this, we can do it to a one because taking the last two elements will give you a zero and one and then we can apply it over and over again. So how can we actually use this and how can we define things in terms of this function? Well, now we can write a recursive function where we are looking at the element, at the argument.

If it's less than equal to one, then we know exactly what the sequence is going to be. If it's zero, it's going to be the empty numeric vector. If it's one, it's going to be a vector one.

And so we can transform a one into a vector, one and zero into zero element vector simply by letting the argument reshape itself. And then we want to extend the sequence otherwise. And what sequence are we going to extend? We're going to extend the sequence that we got for one less than the current number we are at and then we just need to extend it.

So let's call this a recursive version. This works, but it has one problem and that approaches the field of telco optimization. Telco optimization is a method where we do not need to keep track of the caller when we are recursing by not having to build up a stack because the final result value is not going to be post processed in any way.

And the problem that we have up here is that after we're recursing we're taking the result value and modifying it. Essentially we're building up a sequence on the stack which is just waiting for a value that can be extended more and more and we really should try to avoid that both for efficiency and not to run out of stack space either. So if the interpreter and this one is is tilcoll optimized, then it will detect that we're not using the result, just returning it.

And then it will not build up a new stack frame will just replace the old stack frame with a new one. And for that we want to know when to stop rather than just returning a value which is then used. And the way we know how to stop is when we've generated enough of the sequence.

Meaning when the generator sequence is long enough. So we'll feed every iteration of this function, the stop condition in the form of a length, how long we need to make it, and that's going to be a left argument. And that left argument then is given in the initial call.

So our argument is ten means we want to keep going until we've got ten. Of course we can't make a function that just takes the left argument. So we'll use as raggedy argument the seed value, the beginning sequence we're going to start with.

So if the cut off point is less than or equal to the length of the currently generated sequence, then we either done or beyond done. And so we would in principle just return the sequence. But the problem is it might have been too long and it only really happens if the argument is zero and we begin with a seed value of a one, then we need to chop it down just like we did before.

So we can do a take which just caps the sequence to the correct length. And now since we know we're not done yet, then it's safe to just extend the sequence and then we need to check again. That means we need to recurse and the limit for the sequence length is still going to be the same so we feed that along to the next iteration.

And here we can see that the last call is the recursive call with the left argument but the result isn't being used for further computation. Therefore this is tail call optimized. Then we just need to start off with the seed which is one doesn't matter, it's a scalar because we're going to do the take on it.

So it's going to become a vector anyway and we're going to extend it in all other cases. So this is the tail call optimized version. Here we go.

Another way we could see this use of the fundamental function is by applying multiple times and we can express this using the power operator. So if we use the power operator with a number on some seed then we're going to extend it probably is we're just generating a little bit too much but we can use take again to chop it down. We don't want to start with zero one either because then we get a zero at the beginning.

So we can express this just by using argument over here. So this is using the power operator with two beginning values. So we are pending to the first two.

Oops, there we go. It's a bit, it feels a bit silly to make the sequence longer than it needs to be and we only do that because we're starting off with a seed value of eleven. Problem is, if you were to start with an empty sequence and append to that then when we try to take the last two elements we'll be off an empty vector, we'll be padding with zeros and that's going to be sum together zero and we add a zero and the sequence will stay zero forever.

So how can we ensure that we always get at least one? Well, we can do that by clamping to be above one or doing a max with a one. So if we start with empty sequence and then we apply the basic transformation function on that n times we max with a one, we need to bind these together. So essentially here what's happening is the power operator is applying max over and over again, always with the constant one as left argument, but right before it applies it in the next time it preprocesses the right argument with the fundamental extension function which just then adds one more element to the sequence and that does the job.

So this is appending to the first zero elements. Same mistake. There we go.

So that's another way to do it, another way we can iterate is using reduction and there's a bit of a trick here going on. If we look at our definition of delta it's a different and it doesn't have an alpha in there. So it doesn't use a left argument, doesn't mean we can't give it a left argument.

That works perfectly fine. Therefore we can start off with the sequence and then we can apply with some random value here it doesn't actually matter. And this is a reduction.

We have a sequence 42 42 one in this case, but all these values except for the last one don't matter because only the right side is going to be used as our seat value and then we're just inserting this delta in between them. So we just need to generate a sequence that ends with a one. It doesn't matter what it is, we might as well just use all ones for that.

And then we can reduce using delta and that gives us this notice that it's enclosed because reduction has to reduce the rank from one vector to zero scanner. So it encloses that but we can just disclose that and go back. So this is a very short way of defining it using a reduction.

There is one problem however, that is if we try to run this on zero, so zero reshape one, that's empty vector and then we try to reduce over empty vector. That requires that the operand has a known identity element. We don't have that because it's a user defined function and in fact there isn't one anyway.

So we can't do that. We have to extend the sequence by one and then remove one element again. And it will be a little bit ugly to do that, but it can be done.

So instead of using omega to reshape the one, let's use one plus or one max omega. That just means that if we have zero it becomes one. All the other numbers stay the same and then finally we'll have too many elements just in that case of zero.

But we can fix that as we've done before by just taking the first N element. So in most cases it's going to be a no up, but for zero it's going to chop the one down to a zero. And now that works.

And it works still for larger numbers as well. That's it for using this fundamental fibonacci extension function. But there are other ways to compute it and one is by using a pairwise sum.

So a pairwise sum we can see how it's related to what we're doing because we want to add the last two elements in order to build up the next element. But we want to extend the sequence, not shorten it down. And a pairwise sum that's an Nwise reduced with N being two.

It always reduces the length of the argument by one because it's taking two adjacent elements and combine element to one. So we need to extend, we need to pad with additional numbers. So that means if we have a pairwise sum of zero and one, that gives us the next element.

But we need to have more elements added up. So if we add more and then we can use this again. So if we add more elements so we need to extend one element every time around the loop and pair risk reduction removes one, so we need to add two.

So if we do this hold on, this isn't working. Oh yeah, of course. The problem is that we need to have more, we need to have more ones here.

We need to make sure that the minimum value is a one. So we can use the same trick as we did before with the maximum one. So let's try that now.

We don't actually need any start values anymore. We can apply this again and we can see how the sequence is building up. So we just need this transformation here to be applied over and over again.

So we take the sequence as far as we've built it up so far, put two more zeros on the left Paris reduction, make sure that we start off generating ones and we do that n times beginning with an empty sequence. So this is a parallise sum. Another way to compute the Fibonacci sequence is by using a transformation matrix.

That matrix, it's a tiny little matrix, looks like this. And if we multiply that by itself and keep doing that, then if we look at the generated matrices along the way, we can spot the Fibonacci sequence in there. For example, in the top right corner, we're going down 112358, so on.

And so again, we have here M all over the place and we have matrix multiplications in between them. This means that we can define a vector of Ms and then we can reduce those using the matrix multiplication to get the 10th element. However, we want all the intermediary values.

Instead of using reduction, we can use a scan. And then we just need to have the top right element of each one. That gives us the Fibonacci sequence.

If you try to use it on a zero, it works fine because we have an empty vector with a reduction with a known. So we can try this plus times reduction over an empty vector of matrices. Doesn't really matter what their values are, that doesn't work.

But a scan just gives us the intermediary values beginning with the first one preserved. But when there aren't any, there's nothing that needs to be done. We don't need to curse on any value out, we don't need an identity element, which would have been the identity matrix anyway, but it would have been relative to the argument and that hasn't been defined.

But this is using matrix multiplication and we can hard code our vector in our matrix inside here, so it's standalone. Okay, another way to do it is by the only information is remember, the only information that we need to compute the next value in the sequence are the last two elements. So what it means is that when we go from the current last two elements to the next last two elements, then the last elements become the last element, becomes the first element, and the sum of the two becomes the last element.

So consider here two and three. Let's say those are our last elements. If we do a scan on those, then we preserve the first element and the second element becomes the sum of the two.

That's very close to what we wanted. We want to preserve the last element and then have the sum. And we can do this simply by reversing the two.

So now the three became the first and the sum of two and three became the last. Which means if we do this again, we get the next values. And then if we extract every time around the loop one of the elements, the first one for example, then we can build up the sequence.

We just need to store them somewhere so we can define a function where we have a result variable. We're not going to use it initially, but we're going to apply this transformation. Here the plus scan on the reverse of the current pair.

And then we want to take the first element from that and append that to the result variable. And then we want to return the new pair, which is this whole thing. So here's a trick.

Instead of taking the first element, let's leave the whole thing. And when we do the concatenation to the result variable, we preprocess the new value that is being added to the result with first. But still this whole function is the modifying function in this modified assignment.

And the assignment is here. And there's a principle that the assignment always returns whatever is on the right. So even though we are only actually using the first value, the result of this whole assignment is going to be this whole pair.

And that's the whole pair that we actually interested in. So now we can do this and we want to do it end times. And we just need a starting pair which is zero and one.

So if we do this zero times, we have R already set to an empty vector. If you do it one time, then that means we are adding them up. We're getting one, one taking the first value, that's one adding to that, then the second time around the loop, we do one, one.

Adding up is two. So we get one two, we get another one and so on. And once we've done that N times, then R has accumulated all the values that we want and we're not interested in the last pair, which would be the result from this application with the power operator.

We just want the resulting value. So that gives us our sequence using accumulation. And that's it for all the methods that we're going to look at for building up the result slowly, we can actually compute the entire result in one go.

And there are because it's possible to compute the N fibonacci number directly without building it up to it. And there are various ways of doing so. One way is by using approximations of the golden ratio.

So if we have a bunch of ones for this series and then we can reduce using addition to the reciprocal, this gives us an approximation of the golden ratio. If this value is large enough then we get a very good value for the golden ratio. But as we get there, all the intermediary values which we can get with a scan are approximations and these approximations are exactly ratios of two adjacent elements in the Fibonacci series.

So if they're fractions of the two adjacent elements, that means if you can get either the numerator or the denominator then we can get the sequence and we can do that with these common divisor with one. Although you can see here we're missing one, we want actually the other number in the pair and we can just flip the ratio upside down taking the inverse or reciprocal of that and that gives us the series directly computed. However, we're both using a scan using custom function here and we're using a number of theoretical function on the floats so the performance is not going to be great.

It is neat looking though. We can also use the sum of the binomial coefficients to compute the n three Fibonacci number. The way it works is that we start with the numbers from one to n minus one and then we can give those a name and reverse them and then we can pair them up with themselves in the normal order.

So this pairs up zero, nine, one and eight and so on and doing the binomial on that and then we've sum that and that gives us the Nth Fibonacci number in this way. Notice that we have a scalar function reduction over a scalar vector application. We can combine that to be an inner product and we want the same argument on both sides.

I goes on both sides. We only just want to preprocess the right argument to this inner product with reverse so that it can be stated like this as well. And that means we can make this into a tested function, apply it on ten to get the 10th Fibonacci number and we can therefore get all the numbers up to ten by applying on each on the ocean just like we did in the very beginning with the recursive version.

Of course this is hugely inefficient both because of the expensive functions that we are using the phenomena and also because we're recomputing over and over for every number. But it's kind of fun and short. So this is based on the coefficients and finally we can use be nice formula.

It's rather long and involved but it's not using any difficult math. And so scalar functions and that has the benefit then that we can just compute the enthusiam but directly on those sequence just by feeding it all the indices that we want. I'm going to type it up.

There's nothing really to explain other than this is a formula. You can look it up online. It can be stated in various ways because of some equivalences, but it's not really important.

And so we want that on the entire sequence, that computes the sequence directly. Okay, onto the finishing stage here, which is going to be performance comparison that's copy Cmpx from Defense Workspace. And then we need to build up all the expressions that we want to run.

We can get all the functions that we have defined like this, but there's actually a feature that maybe not so well known that quad. NL can take a list of letters that it will then filter its result with to only include functions that begin with any of those letters. And notice here that all our solutions begin with an uppercase letter, cmpex begins with a locust letter, and delta isn't a normal letter at all.

So if you give it the uppercase English alphabet that filters out in each one of them, well, we want to apply to some argument or argument and in order to get some balance in it, should it be a large number, a small number. So let's apply to all the numbers up to some limit. So we're applying it to each one up to say, 20 and we are doing that on each.

So these are all the expressions we're going to run and then Cmpex on that. And this might take a little while, so I might cut this out of the video. And there we go.

Here's our result. And we can see that using this formula to compute the values is the clear winner here. And even though there is cute, the binomial coefficients is not going to be able to compete with anything.

Thank you for watching.