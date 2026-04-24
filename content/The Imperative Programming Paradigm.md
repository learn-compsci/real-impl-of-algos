---
title: The Imperative Programming Paradigm
tags:
  - notes
  - methods
---
# Paradigms and the Imperative Paradigm

Remember, programming is really a question of bending a computer to your will, getting it to realise your vision, your ideas. So really, it's you translating your idea into something a computer can understand. Given the many years now that we've been programming, we've come up with many different ways to do this (i.e. different programming languages, and now even things like vibe coding exist). Each programming language does usually try to support at least one **programming paradigm** and often multiple ones. So what's a programming paradigm?

A programming paradigm is, well, really just a way to structure your point of view, your thoughts, your expression. There are many that exist, and while we won't go into them (since this is an introductory course), we'll cover the imperative programming paradigm. You might feel like you're missing out considering all the other fancier ones you might have heard, like the **object-oriented paradigm** or the **functional paradigm** or the **declarative paradigm**. But there really still is a place for the imperative paradigm! Defining _methods_ in object-oriented programming languages is often still done imperatively. A lot of efficient code is still easier to accomplish when sticking to an imperative approach than any other.

## The Imperative Paradigm and Saying How You Want Things
The imperative programming paradigm is really straightforward to get right. So it won't take long. It's pretty much specifying the exact, precise, list of steps in which to get something done.


### The Downsides
There are a few downsides to the imperative paradigm that we should warn you about. 

### Forgetting the kind of steps you need to make
The most frustrating bit for people is that they often tend to slip up by forgetting about the state of the program as write their lines. For example, take the following snippet of code:

```C
int main(){
	int a = 6;
	int b = 7;
	
	// I want to swap the values of a and b
	b = a;
	a = b;
	
	// By now, they should have swapped values
	printf("%d %d", a, b);
}
```

You might have expected to see values `7 6` in the output, but instead you'd be rudely greeted by `6 6` instead. But where did we go wrong? Didn't we specify that `b` should be `a` and vice versa?

Following the code that we just wrote step by step, take notice that right after the `b = a` line, and just before the next one, `b` has been set to value `6`. So the next line `a = b` sets `a` to `6`.

This sort of pitfall is very common in imperative style programming where programmers write what they want to happen, instead of how they want it to happen.

If we were to think imperatively in this case, what we actually want is to first store the value of `b` temporarily, so if we did `b = a`, we can safely overwrite what's being stored at `b`. **Then in the next step**, we can set the value of `a` to whatever the **old value** of `b` was. Like so:

```C
```C
int main(){
	int a = 6;
	int b = 7;

	int temp = b; // remember the value of b
	b = a; // set b to the value of a
	a = temp; // set a to the old value of b
	
	// By now, they have swapped values
	printf("%d %d", a, b);
}
```

Notice the difference here, we're thinking imperatively by breaking them down into the correct steps to get our goal done. We **wanted** to swap `a` and `b` but had to specify **how** to get it done by laying out the steps in sequence.

### Tracking state
Along similar lines to the previous point, often in larger and larger programs, you'll find it harder and harder to track your state. Tracing through lines and lines of code can invite room for error, and it does get exhausting. Many programmers sometimes do this with pieces of paper just to try to remember what every variable looks like at any point in time. This sort of mental load when programming is undesirable but still does happen sometimes. With an imperative style language, there are ways to mitigate this, but being able to trace code is definitely still a very important skill to have.
### Managing larger codebases
This happens much later, when we talk about managing larger and larger pieces of code. Imperative-only programming languages tend to lack features to help programmers manage codebases on an industrial scale. And typically massive programs written in C require programmers to stick to their own conventions and habits without having a compiler come and enforce the rules. So it really just becomes a question of how much a C programmer is willing to hold themselves accountable for their own conventions and structure. But that's more of a topic in the far future.

## The Upsides

### Speed
On the other hand, people often praise languages like C and C++ for being fast. There are reasons for that. To a programmer who knows that they're doing, specifying **how** you want something means you can now write and implement algorithms. Over time, you'll realise there are many ways to solve a problem, but some ways are indeed faster or more efficient than others. Being able to specify how you want to solve a problem is indeed the best way to go. (There are other reasons why C/C++ is fast, but this definitely helps).

### Imperative is usually intuitive
For the most part, people tend to think imperatively. Think back to navigating yourself to school for example...

1. I'll take the train to Kent Ridge MRT station
2. Then I'll take the 95 bus to the central library stop
3. Then I'll walk across the road to the engineering department

These are laid out steps. The difficulty for programmers usually isn't thinking imperatively, but thinking at the right level of detail and laying out the correct sequence of steps that faithfully reproduce the idea.

# The Takeaway
It doesn't take much get decent at imperative programming, but being able to trace program code is crucial. It isn't hard, but it is admittedly tedious. There isn't really much else to it. For example, given the following snippet of code:

```C
int accum = 0;
int sign = -1;
for(int i = 0; i < 5; ++i){
	accum += sign * i;
	sign = (accum % 2) - 1;
}

printf("%d", accum);
```

We'd probably very quickly surmise that up until the `for` loop, `accum = 0` and `sign = -1`. But the parts after that might get tedious and annoying. The most reliable way to do this, would be to lay out and remember the values of all the variables as they evolve. Something like a table usually helps.


| `accum` | `sign` | `i` |
| :-----: | :----: | :-: |
|    0    |   -1   |  0  |
|         |        |     |

For example, if we had to track the variables as they changed, we might first start with this.
Then, note, that if we had to update the values, we **faithfully follow the program and update them one at a time**. Initially,  `i < 5` is evaluated, and since it's true, the loop body does execute. So we look at the line `accum += sign * i`, which happens to be `accum = 0 + -1 * 0 = 0`.

| `accum` | `sign` | `i` |
| :-----: | :----: | :-: |
|    0    |   -1   |  0  |
|    0    |        |     |

Next, the line `sign = (accum % 2) - 1` is evaluated, and based on our values, we know this means `sign = (0 % 2) - 1 = -1`.

| `accum` | `sign` | `i` |
| :-----: | :----: | :-: |
|    0    |   -1   |  0  |
|    0    |        |     |
|         |   -1   |     |

Lastly, `i` is incremented, giving us:

| `accum` | `sign` | `i` |
| :-----: | :----: | :-: |
|    0    |   -1   |  0  |
|    0    |        |     |
|         |   -1   |     |
|         |        |  1  |

Now we move into the **second** iteration of the loop, where `i = 1`. Once again, `i < 5` is evaluated, and since it's true, the loop body does execute. So we look at the line `accum += sign * i`, which happens to be `accum = 0 + -1 * 1 = -1`.

| `accum` | `sign` | `i` |
| :-----: | :----: | :-: |
|    0    |   -1   |  0  |
|    0    |        |     |
|         |   -1   |     |
|         |        |  1  |
|   -1    |        |     |

Next, the line `sign = (accum % 2) - 1` is evaluated, and based on our values, we know this means `sign = (-1 % 2) - 1 = -2`.

| `accum` | `sign` | `i` |
| :-----: | :----: | :-: |
|    0    |   -1   |  0  |
|    0    |        |     |
|         |   -1   |     |
|         |        |  1  |
|   -1    |        |     |
|         |   -2   |     |

Lastly, `i` is incremented, giving us:

| `accum` | `sign` | `i` |
| :-----: | :----: | :-: |
|    0    |   -1   |  0  |
|    0    |        |     |
|         |   -1   |     |
|         |        |  1  |
|   -1    |        |     |
|         |   -2   |     |
|         |        |  2  |

This would be how to trace the behaviour of a program, step by step.

# Translating Ideas Imperatively
As mentioned, thinking imperatively probably isn't too hard. What's a little harder is thinking at the correct level of specificity. Typically, beginners don't get specific enough. The snippet about swapping is one such common example. But let's see another one. Let's say we had some initial bank balance and today we're writing a program that computes our bank balance at the **end** of every day.

```C
int main(){
	int intial_balance = 5000;
	int daily_change[4] = { 20, -30, 50, -10 };
	int daily_balance[4]; // uninitialised set of values
	
	for(int day = 0; day < 4; ++day){
		// ???
	}
}
```

So we want to iterate through our array of transaction values, and apply the daily change for the respective day and store it into the `daily_balance` array.

So perhaps something like the following code:

```C
int main(){
	int intial_balance = 5000;
	int daily_change[4] = { 20, -30, 50, -10 };
	int daily_balance[4]; // uninitialised set of values
	
	for(int day = 0; day < 4; ++day){
		daily_balance[day] = intial_balance;
		initial_balance += daily_change[day]; 
	}
}
```

Except, if we did this, we'd end up with `daily_balance[4]` being `{5000, 5020, 4090, 5040}`. Which is the balance at the **beginning** of the day, not the end. Where did we go wrong?

The lines within the function body were misplaced!

```C
int main(){
	int intial_balance = 5000;
	int daily_change[4] = { 20, -30, 50, -10 };
	int daily_balance[4]; // uninitialised set of values
	
	for(int day = 0; day < 4; ++day){
		initial_balance += daily_change[day]; 
		daily_balance[day] = intial_balance;
	}
}
```

Notice that all it takes is a small and innocent swap in lines (pun not intended) that really changes program behaviour. Programs are fragile like that.

## Thinking Imperatively
So how do we prevent such issues from happening? The best way is still via a lot of practice, but generally knowing what kind of "basic steps" your programming language allows you to use, and making sure you can produce the sequence of steps faithfully. Sometimes you might want to play out what the code does after you've written it, that's where tracing comes in handy!
