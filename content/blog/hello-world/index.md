---
title: How to Fix useEffect Hook executing in an endless loop?
date: "2020-06-05T10:50:00.169Z"
description: "This Blog is about how to Fix the React Hook, useEffect executing in an endless loop"
---

##First of all let us see what useEffect Hook does?
Using useEffect Hook, tells React that your component needs to do something after render. React will remember the function you passed and call it later after performing the DOM updates.

##Does useEffect run after every render?
Yes! By default, it runs both after the first render and after every update. Unlike componentDidMount, useEffect is not executed when the component finished mounting, but each time the component is rendered.
That means if you modify the components state inside useEffect, it will cause a re-render of the component, which again causes the execution of useEffect.

    useEffect(() => {
    //This is executed each time the component is rendered.
    });

That’s why useEffect takes an array of dependencies as a second argument. If we don’t pass an array of dependencies, the Hook will be executed in a loop.

You can tell React to skip applying an effect if certain values haven’t changed between re-renders, By passing an array as an optional second argument to useEffect each time one of those objects change, React will execute this Hook. You could pass in any number of values into the array and useEffect will only run when any one of the values change.

    useEffect(() => {
    Document.title = `You clicked ${count} times`;
    },[count]); // Only re-run the effect if count changes

But what if we only want the hook to execute when the component is mounted and rendered the first time?
We already know, if we don’t pass an array of dependencies, the Hook will be executed in a loop. But what if our hook does not depend on any other object?

##So we pass an empty array.
By passing in an empty array, we're telling React not to track any changes, only run once, effectively simulating componentDidMount.

That’s it:

    useEffect(() => {
      // this is only executed once
    }, [])

If we pass an empty array to useEffect, it’s only executed after the first render.

This is even mentioned in [the official React Hooks API documentation](https://reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects):

> If you want to run an effect and clean it up only once (on mount and unmount), you can pass an empty >array ([]) as a second argument. This tells React that your effect doesn’t depend on any values from >props or state, so it never needs to re-run. This isn’t handled as a special case — it follows >directly from how the dependencies array always works.
