# Basics of Time and Space Complexity in Computer Science

## Why Time Complexity Evaluation? 

With any program, you will want to know how fast it will run. Most developers are intrinsically aware of this, testing apps with suites like Selenium or just spot testing with different devices. 'Good enough' is usually how these type of tests get evaluated, with performance being banished to a later sprint.

On many smaller, even mid-scale type of websites, this kind of thinking is lazy but it's honestly fine on a certain scale of project. If you're building an annual report, a simple static site or even a blog, you can probably get away with a serverless architecture or just sticking a CDN or reverse-proxy cache in front of whatever code you've got and get away with it.

But once you reach a certain scale or get upvoted by Hacker News, performance becomes a major consideration of every release. That's when time complexity evaluation becomes a valuable tool to analyze your site.

## Basics of Time Complexity Evaluation

The most basic element of a time complexity evaluation is to **audit your program**. I'm a web-developer, so my complier is the browser. I love Chrome Dev Tools 'Network' tab, where you can record the loading a page to get a sense of it's responsiveness. 

Most programs you'll write typically run fast on the types of machines devs use, loaded with memory and fast internet connections. Where things start to take a dive is on mobile. You can simulate different loading speeds within the 'Network' tab (there is a little dropdown that says 'Online' - click it and you'll see slower options.)

Next step is to try to navigate and use your website a bit now that you've slowed it down. See where it gets clunky. Chances are you're going to run into a function you didn't build quite right or that could be refactored into something better. But maybe not.

What I like to do during an audit like this is find repeat offenders. Look for utility-type functions; they are a good place to hunt. Maybe your project has a special sort going on, custom filters over a big data set - something like that. Operations that occur often are where time complexity analysis will pay the most dividends.

## Calculating the Time Complexity of an Algorithm

Let's say you've identified a minimum value algorithm that's dragging things down (unlikely, but hey, good place to start learning). 

What we're going to do is go through the algorithm, line by line, identifying each operation and how often those operations occur.

```js
/** 
 * Min Value Algorithm
 * Given a random array, get the smallest value
 * [3,2,9] => 2
 * 
 * Time complexity example
 */

function getMinimum(array) {
  let min // operation 1, set up a variable

  // operation 2, create a loop
  // Now, when you introduce a loop, it will have a multiplier effect on time complexity
  // Why? Well it's a loop so everything inside of the loop will run n times, where n is the size of array in this example
  for (let i = 0; i < array.length; i++) {

    if(array[i] < min || min === undefined) { // operation 1 inside of loop (comparison)
      array[i] = min // operation 2 inside of loop (assignment)
    }
  }

  return min // operation 3, return value
}

// Run function with a basic array
getMinimum([3,2,9])
```

Breaking this down, you can see we have five operations in this algorithm, 2 of which get repeated `n` times because they are inside of a loop.

This gives us a time complexity of `2n + 3`, where three of operations occurring just once (variable creation, loop creation, return of value), and the other two operations occurring `2n` times (`n` being the size of the array multiplied by the two operations (comparison and assignment) inside the loop).

## Asymptotic Analysis of Time Complexity

Even though our `getMinimum` algorithm is 2n + 3, we really want to know it's impact over a large amount of runs. If the algorithm runs 20 times, it's not a big deal. What about 20,000, 200,000 times, more?

| n (size)       | Operations     | Complexity   |
| :------------- | :------------: | -----------: |
| 20             | 2(20) + 3      | 43           |
| 20,000         | 2(20,000) + 3  | 40,003       |
| 200,000        | 2(200,000) + 3 | 400,003      |

We can quickly see the `+ 3` part of our time complexity analysis is pretty meaningless. The part we care about is the `2n` part. Another way to say this is to say, 

> 'As `n` gets sufficiently large, the results of `2n+3` will converge to `2n`.' 

This is called asymptotic analysis, deriving it's name from the algebraic asymptote, which is when a set of data converge on a result without ever quite hitting it.

This type of analysis is an easy way for us to simplify our algebraic time complexity calculations, which get more sophisticated as algorithms get more complicated. You always want to look for the part that is the most complicated in your equation.

## Calculating the Space Complexity of an Algorithm

Looking at that same algorithm, we can also get a sense of how much memory it will take up. We do that by tracking how many variables get created and will take up memory. 

We're only making one variable in this algorithm `min` so it's pretty easy to see that space complexity doesn't increase no matter how large the array size `n` becomes. Therefore, the space complexity is only `1`.

## Space Complexity of an Algorithm, Level 2

Let's ramp this idea up a bit with a slightly more complex algorithm. This is based off an algorithm I wrote for a custom sort that orders items as if there weren't any preceding articles in their titles (specifically 'A' and 'The'). I'm leaving some things out of this but it should still make sense:

```js
function sortWithoutLeadingArticle(array) {
  // Build a sortableArray from the original array
  let sortableArray = []; // variable 1, an array

  array.forEach((title, index) => {
    // Split the title string into an array
    let titleParse = title.split(" "); // variable 2, array inside a loop

    // We're sniffing out ones that start with 'A' and 'The', get rid of them
    if (titleParse[0] === "A" || titleParse[0] === "The") {
      titleParse.shift();
      sortableArray.splice(index, 1, titleParse.join(" "));
    } 

    // If no 'A' or 'The', we just splice original title
    else {
      sortableArray.splice(index, 1, title);
    }
  });

  // Sorting is the easy part, just using JS built-in sort
  // I believe this uses the Quicksort algorithm under the as it's the fastest
  return sortableArray.sort();
}
sortWithoutLeadingArticle(data) // assume `data` is an array of titles...
```

In this example, we can see we're creating two variables. Both are arrays (`.split` returns an array) so you might assume `2n` space complexity. But look a bit closer.

The first variable, `sortableArray` always gets created as a single array even if you put more arrays into this algorithm. So it's really just `n` complexity because of `titleParse` which will scale at the same rate as the `array` parameter in the function.
