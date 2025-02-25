---
title: "How to Think Recursively - Part 1"
date: 2022-11-15T13:15:37-04:00
description: "How to break down a recursive question into smaller pieces. Easy Question"
category: "Interviewing"
tags: ["Recursion", "Dynamic Programming", "Algorithmic Thinking", "Climbing Stairs"]
---

These articles are about the gotchas I faced when trying to think recursively. The logic in principle should apply to most recursive problems. 
In this post, I will use the following question as a point of reference:

> Count how many ways you can climb a staircase. You can jump either one step at a time or two steps at a time. 

Example if there are 3 stair cases then you can either jump: 

```
1,1,1  
2,1  
1,2
```

In total there are three ways to get to the 3rd stair. It's important to mention that that:

1,1,2 or 2,2 go beyond the desired stair. Because they reach 4. Given that 4 is undesired. Anything after 4 is undesirable as well. 
## Foundational steps
- Know what it means to travel in a DFS vs BFS. Draw trees for yourself. If you haven't mastered this, then it may be best to not dive deeper yet. 
    - Try what you've learned with the most simplest examples. Like the staircase example we're using in this post.
    - Understand the term **branching factor**. That means from each node, how many new nodes will become reachable.
        - If all you can do is jump one or jump three, then your branching factor is `2`. 
        - If you were able to only jump six, then your branching factor is just `1`. 
        - If you were able to jump one or five, or nine, then your branching factor is `3`.

- Try learning about the different classic (but simple) problems that are solved using trees. Just knowing the various kinds of problems and how the traverse visually happens, helps you understand other challenges.
- Use a paper and try to visually solve the question in the simplest form of a tree example (a root and two leafs).
- Then make your tree bigger by adding one more level to your tree and try to visualize the solution again. If you struggle here, then don't go any further until you figure it out. 

> A good paradigm shift about trees is to think of them as 'decision trees' or in certain cases 'decision tables'

## Ask yourself 'what information do I need to pass down for each path, so I can have all the variables needed to make a decision'?
- A tree is basically made up of multiple paths. **Each** path needs to be able to maintain **its own state**. The state can't be shared amongst other paths. If things are shared across paths then a states path gets overridden. You don't want that.
Because of this, the state can't be a property of a class nor a local property of your function. It has to be an argument of the function that you pass down as you traverse the tree. In other words it's the stack's property.
- Here are examples of things you may need to pass down depending on the question: 
    - The _previous actions_ you took, e.g. Jumped 2, then jumped 3. Your helper function should take that as an array of previous jumps `[2,3]`
    - The _computed aggregation_ of previous jumps, e.g. the aggregation of jumps is 5. You could have jumped 5 through jumping either (5) or (1,1,3) or (4,1) or (1,4) or (2,1,1,1) etc. But all you need to pass is the sum of your jumps as `5`.
    - Other sophisticated problems may require you to pass more complex variables down your path.
## Under what conditions do I stop tree traversal? What do I return (or do — in case of a `Void` function)?
Identify condition(s) that your tree stops growing / hits a leaf / ends a path / terminates progression. Return a value. Examples:
### Jump StairCase
- End if reached the top of the stairs. 

```swift
if totalJumpSum == targetSum { return 1 }
```

Note: If you needed to return the actual jumps and not just the total 'numbers' then: 
```swift
if totalJumpSum == targetSum { 
    newAnswerArray = currentJumpsArray + lastJump // [jump2, jump5] + jump3
    answerArray += newAnswer // answerArray += [jump2,jump5,jump3]
} 
```

- Don't forget you need to also stop when you go beyond the desired target. Example:

```swift
if totalJumpSum > targetSum { return 0 }
```
So
- Return 1 if you found an answer, that would increase the total count.
- Return 0 if needed to terminate, but didn't find a good answer.

As the coder you have to identify when you should stop traversing / recursing because either you:
- You reach the _desired_ target/state.  
- You reached an _undesired_ target/state.

If you haven't reached a desired or undesired target, then you should just traverse further down the tree. Examples: 
- Array, 2D Grid: Out of bounds, beyond our target
- Range, (sliding) window or 2 pointers: left index becoming greater than your right index
- Graph: often a visited node is considered a terminated state, because you've already processed it. It could lead to redundant work or cause cycles.
- Other kinds of undesired state: 
  - Going passed a certain count
  - Going over our budget
  - Some required logic, becomes incorrect. 
    - In DFS/Backtracking: Upon violating a Sudoku rule, you undo the last step or choice and try a different option. In recursion, this means returning to a previous state and exploring other possible paths after hitting an undesired or invalid condition. For example, if placing a number in Sudoku breaks the rules, you remove that number and try a different one in the same spot.
    - In Sorted contexts or Binary Search: You go beyond the min/max values

## So I didn't hit a base case. What then? 

- Call your recursive function again. 
- Pass whatever **path specific** information was needed. 
    - You always need to mutate the previous path/state before you recurse again i.e. you have to do whatever's necessary to reflect that you've moved from one node to another.
- **Note:** You should not do any other checks at this point. Even if you know jumping 2 steps from 2, will go beyond 3 (the desired target), you shouldn't add logic to skip calling the recursive function. You should just call your recursive function. Let it terminate / exit early in the **next run** of your function's base case checks.
This was a confusing point for me personally. I was never sure if I needed to be smart and skip calling my recursive function again. Now I know I shouldn't be smart.  
Basically don't early exits to your recursive calling.

Your overall structure should be like this: 

```swift

func findSolution(inputs: [Inputs]) {
    /* 
    Call helper with its current state.
    */
}

func helper(pathState: State) -> Value {
    /*
    if reached_base_case:
        return base_case_value    
    else reached_another_base_case:
        return other_base_case_value 
    else traverse_down_tree: 
        - Traverse down the tree. 
        - Update the path/stack.
        - Return the result of all paths† together. Each question has a different trick for combining. Example of different ways to combine:
            - With `+`. Example: sum of all nodes. 
            - With `&&`. 
            - With `||`
            - With `==`
            - max of all children. Sum of all children. etc
            - Processing every previous node with the current node. Example see my post on [longest increasing subsequence](https://mfaani.com/tags/longest-increasing-subsequence/)
            - If you have a local property and are updating your sum/max, then you don't need to return a value. You just mutate the property of yours...
            - Other ways
        
        This recursive call will ultimately always lead to hitting a base case that stops recursing. Trust the process. Don't try to preemptively end it within the normal recursion 😉

    †: All paths mean all paths that stat from the root and end with your terminating (desired + undesired) states.
    */
}
```

## Figure out how to call your recursive function from your main function
Probably the easiest step. You just pass your current node and whatever target you have. The recursive helper function will bifurcate and create new branches as needed.

For our Count number of ways example: 

You're starting from stair `0`. And your starting/current answer is `0`. You also need to pass in your desired stair i.e. `3`.

## Summary of steps
So to do each of the four steps we discussed earlier: 
1. [What information do I need to pass down for each path](http:mfaani.com/posts/interviewing/how-to-think-recursively-part1/#ask-yourself-what-information-do-i-need-to-pass-down-for-each-path-so-i-can-have-all-the-variables-needed-to-make-a-decision): The sum of the jumps so far. This value is what differentiates each path/branch for another.
2. [Under what conditions do I stop tree traversal?](http:mfaani.com/posts/interviewing/how-to-think-recursively-part1/#under-what-conditions-do-i-stop-tree-traversal-what-do-i-return-or-do-in-case-of-a-void-function): If I reach the targeted stair. Or if jumped passed it.
3. [So I didn't hit a base case. What then?](http:mfaani.com/posts/interviewing/how-to-think-recursively-part1/#so-i-didnt-hit-a-base-case-what-then): Recursively call the function. Combine the results of each node using `+`. Don't be smart: Don't try not calling your function. Let it exit any of its base cases in the next function execution.
4. [Figure how to make the first recursive call](http:mfaani.com/posts/interviewing/how-to-think-recursively-part1/#figure-out-how-to-call-your-recursive-function-from-your-main-function): Pass 0 as current node. Pass 3 as you desired target.

### Solution A - Simplest choice: 

```swift
func howManyWays(num: Int) -> Int {
    return helper(origin: 0, target: num)
}

/// Recursively returns the total number of steps
/// - Parameters:
///   - origin: arrived step/node
///   - target: desired step/node
/// - Returns: Total number of ways from a given step/node
func helper(origin: Int, target: Int) -> Int {
    if origin == target {
        return 1
    } else if origin > target {
        return 0
    } else {
        return helper(origin: origin + 1, target: target) + helper(origin: origin + 2, target: target)
    }
}

print(howManyWays(num: 4))
```

### Solution B - Pass down a computed property
So instead of passing down both target and current, we can pass `remainingSteps`

```swift
func howManyWays(num: Int) -> Int {
    return helper(remainingSteps: num - 0)
}

/// Recursively returns the total number of steps
/// - Parameters:
///   - remainingSteps: The number of jumps required from current node to target node
/// - Returns: Total number of ways from a given step/node
func helper(remainingSteps: Int) -> Int {
    if remainingSteps == 0 {
        return 1
    } else if remainingSteps < 0 {
        return 0
    } else {
        return helper(remainingSteps: remainingSteps - 1) + helper(remainingSteps: remainingSteps - 2)
    }
}

print(howManyWays(num: 3))

```

## Triage your recursion:

### Do I need a helper function? 

**Managing Additional Parameters:**
- State Maintenance: If your recursive solution requires maintaining extra state or parameters (like indices, accumulators, or flags) that aren't part of the initial function call, a helper function can encapsulate these details.
- Simplifying the Public Interface: By using a helper function, you can keep the primary function's signature simple, hiding the complexity from the user.  

**Initializing Values:**
When certain initial values or conditions are required for the recursion to work correctly, a helper function can set these up without exposing them to the user.

### I can't come up with a solution
Tree solutions are often a variation of figuring out the right computation/transition for: 
- A node and its previous node.
- A node and some aggregation of all its previous nodes.
- A node and each individual previous node.
- A node and other nodes at the same level.
- Every subtree of the node and subsequent subtrees. 
- A property of the tree or subtree.

### Why does my code continue infinitely?
It implies that either you:
- Haven't handled all your base cases.
- Didn't change the state upon traversing.

> 💡: Often my codes causes stack overflow, but I'm coding in Swift Playgrounds and don't have access to a proper debugger. To be able to see logs without the Playgrounds app crashing (due to overflow), I add logs and **exit early** if I've called a recursive function more than 20 times. I just add a counter and increment it.
>
> 💡 I also add conformance to `CustomStringConvertible` protocol so I can logs in the exact way I prefer for my custom types. 

### Should I return values at the end of my recursive functions? Or should they be void functions? 
With most programming problems, you can solve it by either way. At the moment I don't have tips for when one becomes the better choice. But I'm sure there are moments when one is preferred over the other. 

### I can draw the tree and traverse it on paper. I can't do the code though. Any tips?
As humans we normally draw our trees layer by layer (BFS). However in code, we usually go deep first, then reach a leaf. Climb back then and try the next unvisited node. In code we typically do DFS not BFS. 

Understanding that difference helps. Now try this: 
- Draw the entire tree
- As you want to find an answer, just go down _one_ path i.e. go deep. 
- Ask yourself what causes mutation from previous node to next node in your path. 
- Pass that down in your helper function.

### I'm passing too many variables. What can I do? 
If you're passing in a parameter that never changes, then that's often a variable that can be eliminated. 
Example we don't need to pass down the desired stair. Instead we can just pass the remaining stairs left to jump.

### Any last tips? 
Add documentation to your code. It often creates a rubber ducky moment for you...

As a summarized alternate way of saying things:
1. Think of what terminates recursion. It's either by reaching a desirable target or reaching an undesirable target. <-- Base case
2. Think of how to traverse from an adjacent state to the terminating state. How values and state change.
3. Expand that into a formula which starts from your origin.
See [here](https://gist.github.com/mfaani/89069e38f49eea20b7e47b8f14308505#file-longest-common-subsequence-memoization-swift-L27-L35) for more.

## Optimization (avoiding repeated calculations)
I'm mainly leaving Memoization out of scope. Just a single yet important note:  

When implementing memoization, the choice of key to hash for each node is crucial to avoid redundant calculations and ensure correctness. In tree-based problems, the 
following attributes are often used to uniquely identify nodes, each serving a distinct purpose:
- The **level** of the node in the tree. Example you're at the 3rd level away from the root.
- The **value** of the node in the tree. Examples: 
  - The value of this node is `18`. 
  - `fibonacci(3)`. 
  - For more complicated problem, the value could be a complex value. For the [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/description/) question I had to create a `State` type so I can hash based off multiple values. 
- The **path** took prior to arriving at that node in the tree. Example nodes A, R, K were took before.

## More Reading

See [part 2](http://mfaani.com/posts/interviewing/how-to-think-recursively-part2/) of this article. 
