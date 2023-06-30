# Use Effect Pitfalls

Source: https://www.youtube.com/watch?v=QQYeipc_cik

## What is useEffect?

- When we update the state of a component, React will re-render the component
- useEffect is a hook that allows you to perform side effects in functional components

- UseEffect runs after the component is rendered

## UseEffect Dependencies

- If we don't want the useEffect to run after every render we can pass a second argument to useEffect, this is called useEffect dependencies
  - This second argument is an array of dependencies
  - If the dependencies don't change, the useEffect won't run
  - If the dependencies are empty, the useEffect will only run once on the first render

## 