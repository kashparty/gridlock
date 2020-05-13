# Simulating traffic and navigation

While reading about Dijkstra's algorithm in my Computing textbook, I felt the need to implement something similar myself. I wanted to see if I could gain any understanding into how more complex systems, such as the ones behind our satnavs work. I also thought it would be a really interesting experiment to see how playing around with different parameters would effect the congestion in my simulation.

I wanted to write the code for this without doing any further research - it was meant to be an exercise in taking a theory from a book and putting it into practice. I later learned that the A* algorithm would be a more appropriate algorithm to use here, since it uses heuristics to make the process faster.

## The idea

Here are the basic rules of the game:

- The roads are represented by a 20 x 20 grid. This means that any square on the grid can be the origin for a car, and any square can be the destination for a car.
- Each car is just a block on the grid, which is able to move - it has a starting position and a destination which it moves towards.
- Cars can move through each other, as if each road had multiple lanes. Also, this stops two cars going in opposite directions getting completely stuck forever like two pawns on a chess board.
- Each car leaves behind a trail of "congestion". This is basically just a number to say that a car has recently been in that area. This number decreases to zero over time, so congestion is allowed to "fade" if no more cars pass through the area.
- The more cars that pass through an area, the higher the nearby congestion score.
- Cars make their pathfinding decisions based on the congestion in different areas of the board. This will be explained in more detail shortly.

## The pathfinding algorithm

First, I considered the problem without the congestion values.

When I came up with the pathfinding algorithm, I thought that using dynamic programming would be effective. It means that in order to calculate the shortest path between the starting point and the destination point, we can solve smaller subproblems to lead us to the final answer. 

For example, finding the shortest distance between two adjacent points is obvious - the answer is just 1, since you only need to move one square to get there. Therefore, the shortest distance between the starting point and the points right next to it is 1.

We can then store the shortest distance from the starting point to each other point on a grid of values. For example, if the green square is the starting square:



