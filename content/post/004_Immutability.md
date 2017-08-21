+++
date = "2017-04-12T20:07:58+01:00"
draft = false
image = "tattoos.jpg"
summary = "An interesting bug I ran into during the Starling Bank hackathon"
title = "Immutability"

+++

I ran into an interesting bug while taking part in the [Starling Bank](https://www.starlingbank.com/) hackathon last weekend - it was a fantastic experience being one of the first to work with an Open Banking API.

I worked with 3 friends to create an automated savings app which allows you to automatically allocate funds to your savings account based on customisable rules, and track your progress towards savings goals.

Check out the [code on GitHub](https://github.com/mattdean1/savings-automator)!

This will be a technical post focused on what caused the bug and how I solved it. To summarize, JS passes objects and arrays by reference, so you should be careful when updating a complex state object in React.


## The Bug

The bug appeared when attempting to create a savings goal.

Creating the first goal worked fine:

![Creating the first goal](/screenshots/immutability/02_creategoal1.png)
![First goal created](/screenshots/immutability/03_goal1created.png)

But attempting to create a second goal produced some interesting behaviour:

![Creating the second goal](/screenshots/immutability/04_creategoal2.png)
![Second goal created](/screenshots/immutability/05_goal2created.png)

So the first call worked fine, and the second call added a new goal, but also updated the values of the previous one!

Here is the relevant code:

(I realise I shouldn't be storing so much in the state but this was a hackathon after all!)


```
const sampleGoal = {
  title: '',
  goal: '',
  raised : 0,
  category: '',
  percentage: 0,
  start_date : '',
  estimated_end_date : '',
  estimated_days : 0
};

createGoal () {
  const newGoal = sampleGoal;
  newGoal.title = this.state.newGoalTitle;
  newGoal.category = this.state.newGoalCategory;
  newGoal.goal = this.state.newGoalCost;
  newGoal.start_date = new Date();

  let goalsArray = this.state.goals;
  goalsArray.push(newGoal);

  this.setState({ goals: goalsArray });
}
```

What could be causing the issue?

My initial thoughts were that something was being passed by reference where it shouldn't be, but we couldn't figure out exactly what or where.

After taking a break, I came back to tackle it again. After some extensive googling I found this [super helpful article](https://medium.com/pro-react/a-brief-talk-about-immutability-and-react-s-helpers-70919ab8ae7c).



## It’s a JS problem

Objects and arrays are passed by reference in JS. This means that a new copy is not created, and updating the 'new' object or array actually modifies the original one.

In this case I couldn't use `array.concat` or similar non-destructive methods, or `object.assign` as suggested in the article because I am attempting to modify a nested object so JavaScript will always pass by reference.


## Immutability helper

The article I linked earlier references the built-in React Immutability Helpers, however when I visit the suggested [page in the React docs](https://facebook.github.io/react/docs/update.html), I find that "`update` is a legacy add-on. Use [kolodny/immutability-helper instead](https://github.com/kolodny/immutability-helper)."

This is a fantastic little module that allows us to update e.g. a complicated nested state object "without changing how the data is represented". The syntax is similar to mongodb queries, so didn't take long to get used to.

If you're running into issues related to the immutability in more than one place in your application, you might want to look into a more full-featured solution like Facebook's [Immutable.js](https://facebook.github.io/immutable-js/).


## The Solution

Remembering to import the library, the createGoal function now looks like this:

```
createGoal () {
  const newGoal = sampleGoal;
  newGoal.title = this.state.newGoalTitle;
  newGoal.category = this.state.newGoalCategory;
  newGoal.goal = this.state.newGoalCost;
  newGoal.start_date = new Date();

  let goalsArray = update(this.state.goals, { $push: [newGoal] })

  this.setState({ goals: goalsArray });
}
```

The key line is

```
let goalsArray = update(this.state.goals, { $push: [newGoal] })
```

instead of


```
let goalsArray = this.state.goals;
goalsArray.push(newGoal);
```

This ensures JavaScript makes a deep copy of the necessary nested elements, instead of passing the object by reference.

Many thanks to the creator of this library and to my team for having patience while we got to the bottom of this one!
