# return vs side effect example

#### also known as Batman vs Joker example

There are two main ways a function can be written in JavaScript (other languages too, but my examples are in JavaScript). One way is to **return a value**, and the other way is to **have a side effect**. And those are often misunderstood or mixed up by beginners. So let's clarify that with an example. And as those types of functions are often called **pure functions** and **impure functions** or **dirty functions**, I will (non-commercially) use the Batman and Joker analogy as they are possibly the most famous pure and impure characters in the world. And Joker does have a lot of dirty tricks up his sleeve, doesn't he?

Batman always puts maximum effort in order not just to fight the crime, but also to bring the criminals to justice, alive. And result is always just as one would expect: they eventually escape from the prison or asylum, so he will be there to return them back. Yet, his actions are always predictable, and he never does anything unexpected. And so all his heroics change nothing in the world or even in Gotham. So Batman always gets the reason to return to our pages and screens.

Joker, on the other hand, is so unpredictable. Seemingly random even. He loves doing something unexpected, and he always leaves a mess behind him. Anything and everything he does, he does it for the show. And he always leaves a mark.

So, let's see the example. We'll examine two sets of simple functions that perform the same calculations but present results differently:

```javascript

// say, Batman, less known as Bruce Wayne, a billionaire,
// decides to calculate the average of the funds he spent
// on his gadgets and vehicles by quarter and by year
const january = 1000;
const february = 2000;
const march = 1200;
const april = 2600;
const may = 3000;
const june = 3100;
const july = 2700;
const august = 2500;
const september = 2300;
const october = 2900;
const november = 2200;
const december = 2100;

// Batman, being a hero, always returns the result
function bCalcQuartAvg(month1, month2, month3) {
  return (month1 + month2 + month3) / 3;
}
// always returns the result!
function bCalcYearAvg(quart1, quart2, quart3, quart4) {
  return (quart1 + quart2 + quart3 + quart4) / 4;
}

// And then he makes his calculations
const q1avg = bCalcQuartAvg(january, february, march);
const q2avg = bCalcQuartAvg(april, may, june);
const q3avg = bCalcQuartAvg(july, august, september);
const q4avg = bCalcQuartAvg(october, november, december);
const yearAvg = bCalcYearAvg(q1avg, q2avg, q3avg, q4avg);

// We can easily see the results of his calculations
console.log({ q1avg, q2avg, q3avg, q4avg, yearAvg });
// { q1avg: 1400, q2avg: 2900, q3avg: 2500, q4avg: 2400, yearAvg: 2300 }
// and none of his functions made side effects
```
And now, after we've seen how Batman analyzes his spending on crime-fighting gadgets, let's see the Joker's way of doing the same thing as he wants to keep track of the loot from his heists:

```javascript
// say, Joker, being a criminal mastermind, decides 
// to calculate the average of the money he and his 
// gang stole by quarter and by year teasing Batman
const january = 1700;
const february = 2200;
const march = 1500;
const april = 2900;
const may = 3100;
const june = 3300;
const july = 2800;
const august = 2600;
const september = 2400;
const october = 3000;
const november = 2300;
const december = 2200;

// Joker, being a chaotic show-off, wants everyone to see
function jCalcQuartAvg(m1, m2, m3) {
  console.log("A-ha-ha!", (m1 + m2 + m3) / 3);
}
// but he doesn't return anything
function jCalcYearAvg(q1, q2, q3, q4) {
  console.log("BOOM!!", (q1 + q2 + q3 + q4) / 4);
}

// And then he makes his calculations...
const q1avg = jCalcQuartAvg(january, february, march);
const q2avg = jCalcQuartAvg(april, may, june);
const q3avg = jCalcQuartAvg(july, august, september);
const q4avg = jCalcQuartAvg(october, november, december);
const yearAvg = jCalcYearAvg(q1avg, q2avg, q3avg, q4avg);

// But what we see is not what one might expect...
// A-ha-ha! 1800
// A-ha-ha! 3100
// A-ha-ha! 2600
// A-ha-ha! 2500
// BOOM!! NaN
```

Let's see what happened here. Batman's functions returned the results, allowing us to use them in further calculations. Joker's functions, on the other hand, just printed the results to the console, and didn't return anything. Sure, we can see the results, but we cannot use them in further calculations. Yes, console was changed, that's a side effect. But that's the end of it, those values we output there can't be used any more. Even though that dirty function will still return a value, it's not the result of the calculation, but merely `undefined`. And when we tried to use those results in further calculations, we got `NaN` (Not a Number) as a result. 

So if you only care about showing the results to the console or stash them somewhere else, you can use the Joker's way of impure functions with side effects. But if you want to use the results in further calculations, you should use Batman's way of functions that return the results. Of course, technically, nothing stops you from mixing those two ways, but I would advise against it. It's better if your function either returns a value or has a side effect, but not both. Unless you are experienced enough to know what you are doing and why you are doing it.

Still, Batman and Joker are just fictional characters. Do not think that you can't use the Joker's way of doing things. Quite often you will need to modify the UI, sort an array, add or remove something somewhere, open or close a modal, write to a file, update a database - and all those actions are side effects. And that's perfectly fine. No better or worse than returning a value. Normally we use both. Just avoid mixing those two ways of doing things in the same function if you can. 

So if you are writing a function, start by asking yourself: do you need to return a value, or do you need to have a side effect? And if you are getting familiar with some function you didn't write, the very first thing you should find out is: does it return a value, or does it have a side effect? 

Postscript: An experienced developer can object that I oversimplified the concept of a pure function without mentioning some other important properties required to call a function pure. And they would be right. But that's intentional, as I wanted to keep this example as simple as possible, and I hope I managed to do that.
