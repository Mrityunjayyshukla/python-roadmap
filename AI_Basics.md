# AI Basics
AI can use certain information and on the basis of that, it can draw out conclusions. There are various ways in which AI can work.

## 1. Search
Searching can be done by searching out the most optimal way to go from Initial to Final Point<br>
Some terminologies that can be used is:<br>
<p></p>
<b>1. Agent: </b> Entity that perceives its environment and acts upon that environment.<br>
<b>2. State: </b> Configuration of the agent and its environment.<br>
&emsp;&emsp;<b>2.1 Initial State: </b> The state in which the agent begins.<br>
&emsp;&emsp;<b>2.2 Final State: </b> The state in which the agent has to go.<br>
<b>3. Action: </b> Choices that can be made in a state.<br>
&emsp;&emsp;<i>Actions(s)</i> returns the set of actions that can be executed in a state <i>s</i>.<br>
<b>4. Transition Model: </b> a description of what state results from performing any applicable action in any state.<br>
&emsp;&emsp;<i>Result(s,a)</i> returns the state resulting from performing action <i>a</i> in state <i>s</i>.<br>
<b>5. State Space: </b> the set of all states reachable from the initial state by any sequence of actions.<br>
<b>6. Goal State: </b> a way to determine whether the current state is goal state or not.<br>
<b>7. Path Cost: </b> Numerical Cost associated with a given path (Most optimal path is the one with the minimum cost).<br>
<b>8. Solution: </b> A sequence of actions that leads from the initial state to a goal state.<br>
<p></p>
A Search problem consists of 

```Initial State``` |
```Actions``` |
```Transition Model``` | 
```Goal Test``` |
```Path cost function```
<p></p>
The Data Structure used for the information to be represented in a particular state is called <i><b>Node</b></i><br>
A Node is a data structure that keeps track of<br>

- A state
- A parent (Node that generated this node)
- An action (action applied to parent to get that node)
- A path cost (From initial state to that node)

To keep the track of the states, a data structure is used called <i><b>Frontier</b></i>. Usually <i><b>Stack</b></i> is used for it as it supports <i>Last In First Out</i> approach.
<p></p>

### Approach to find the solution 

- Start with a frontier that contains the initial state.
- Start with an empty explored set.
- Repeat<br>
  &emsp;&emsp;> If the frontier is empty, then no solution.<br>
  &emsp;&emsp;> Remove a node from the frontier.<br>
  &emsp;&emsp;> If node contains goal state, return the solution.<br>
  &emsp;&emsp;> Add the node to the explored set.<br>
  &emsp;&emsp;> Expand node, add resulting nodes to the frontier if they aren't already in     &emsp;&emsp;the frontier of the explored set.<br>

The Algorithm used here is <br>
<p>
<i><b>Depth-First Search</b></i><br>
Search algorithm that always expands the deepest node in the frontier.<br>
and<br>
<i><b>Breadth-First Search</b></i><br>
Search algorithm that always expands the shallowest node in the frontier<br>

Applying this approach in Python will be:

```
import sys

class Node():
    def __init__(self, state, parent, action):
        self.state = state
        self.parent = parent
        self.action = action


class StackFrontier():
    def __init__(self):
        self.frontier = []

    def add(self, node):
        self.frontier.append(node)

    def contains_state(self, state):
        return any(node.state == state for node in self.frontier)

    def empty(self):
        return len(self.frontier) == 0

    def remove(self):
        if self.empty():
            raise Exception("empty frontier")
        else:
            node = self.frontier[-1]
            self.frontier = self.frontier[:-1]
            return node


class QueueFrontier(StackFrontier):

    def remove(self):
        if self.empty():
            raise Exception("empty frontier")
        else:
            node = self.frontier[0]
            self.frontier = self.frontier[1:]
            return node

class Maze():

    def __init__(self, filename):

        # Read file and set height and width of maze
        with open(filename) as f:
            contents = f.read()

        # Validate start and goal
        if contents.count("A") != 1:
            raise Exception("maze must have exactly one start point")
        if contents.count("B") != 1:
            raise Exception("maze must have exactly one goal")

        # Determine height and width of maze
        contents = contents.splitlines()
        self.height = len(contents)
        self.width = max(len(line) for line in contents)

        # Keep track of walls
        self.walls = []
        for i in range(self.height):
            row = []
            for j in range(self.width):
                try:
                    if contents[i][j] == "A":
                        self.start = (i, j)
                        row.append(False)
                    elif contents[i][j] == "B":
                        self.goal = (i, j)
                        row.append(False)
                    elif contents[i][j] == " ":
                        row.append(False)
                    else:
                        row.append(True)
                except IndexError:
                    row.append(False)
            self.walls.append(row)

        self.solution = None


    def print(self):
        solution = self.solution[1] if self.solution is not None else None
        print()
        for i, row in enumerate(self.walls):
            for j, col in enumerate(row):
                if col:
                    print("â–ˆ", end="")
                elif (i, j) == self.start:
                    print("A", end="")
                elif (i, j) == self.goal:
                    print("B", end="")
                elif solution is not None and (i, j) in solution:
                    print("*", end="")
                else:
                    print(" ", end="")
            print()
        print()


    def neighbors(self, state):
        row, col = state
        candidates = [
            ("up", (row - 1, col)),
            ("down", (row + 1, col)),
            ("left", (row, col - 1)),
            ("right", (row, col + 1))
        ]

        result = []
        for action, (r, c) in candidates:
            if 0 <= r < self.height and 0 <= c < self.width and not self.walls[r][c]:
                result.append((action, (r, c)))
        return result


    def solve(self):
        """Finds a solution to maze, if one exists."""

        # Keep track of number of states explored
        self.num_explored = 0

        # Initialize frontier to just the starting position
        start = Node(state=self.start, parent=None, action=None)
        frontier = StackFrontier()
        frontier.add(start)

        # Initialize an empty explored set
        self.explored = set()

        # Keep looping until solution found
        while True:

            # If nothing left in frontier, then no path
            if frontier.empty():
                raise Exception("no solution")

            # Choose a node from the frontier
            node = frontier.remove()
            self.num_explored += 1

            # If node is the goal, then we have a solution
            if node.state == self.goal:
                actions = []
                cells = []
                while node.parent is not None:
                    actions.append(node.action)
                    cells.append(node.state)
                    node = node.parent
                actions.reverse()
                cells.reverse()
                self.solution = (actions, cells)
                return

            # Mark node as explored
            self.explored.add(node.state)

            # Add neighbors to frontier
            for action, state in self.neighbors(node.state):
                if not frontier.contains_state(state) and state not in self.explored:
                    child = Node(state=state, parent=node, action=action)
                    frontier.add(child)


    def output_image(self, filename, show_solution=True, show_explored=False):
        from PIL import Image, ImageDraw
        cell_size = 50
        cell_border = 2

        # Create a blank canvas
        img = Image.new(
            "RGBA",
            (self.width * cell_size, self.height * cell_size),
            "black"
        )
        draw = ImageDraw.Draw(img)

        solution = self.solution[1] if self.solution is not None else None
        for i, row in enumerate(self.walls):
            for j, col in enumerate(row):

                # Walls
                if col:
                    fill = (40, 40, 40)

                # Start
                elif (i, j) == self.start:
                    fill = (255, 0, 0)

                # Goal
                elif (i, j) == self.goal:
                    fill = (0, 171, 28)

                # Solution
                elif solution is not None and show_solution and (i, j) in solution:
                    fill = (220, 235, 113)

                # Explored
                elif solution is not None and show_explored and (i, j) in self.explored:
                    fill = (212, 97, 85)

                # Empty cell
                else:
                    fill = (237, 240, 252)

                # Draw cell
                draw.rectangle(
                    ([(j * cell_size + cell_border, i * cell_size + cell_border),
                      ((j + 1) * cell_size - cell_border, (i + 1) * cell_size - cell_border)]),
                    fill=fill
                )

        img.save(filename)


if len(sys.argv) != 2:
    sys.exit("Usage: python maze.py maze.txt")

m = Maze(sys.argv[1])
print("Maze:")
m.print()
print("Solving...")
m.solve()
print("States Explored:", m.num_explored)
print("Solution:")
m.print()
m.output_image("maze.png", show_explored=True)
```
<p></p>
<i><b>Uninformed Search</b></i><br>
Search Strategy that uses no problem specific knowledge.<br>
<p></p>
<i><b>Informed Search</b></i><br>
Search strategy that uses problem-specific knowledge to find solutions more efficiently.<br>
<p></p>
For Informed Search, some types of search that are used:<br>
<i><b>Greedy best-first Search</b></i><br>
Search algorithm that expands the node that is closest to the goal, as estimated by a heuristic function <i>h(n)</i>.<br>
<p></p>
<i><b>A* Search</b></i><br>
Search algorithm that expands node with lowest value of g(n) + h(n).<br>
g(n) = cost to reach node<br>
h(n) = estimated cost to goal<br>
In easy way, g(n) can be said as the number of steps that have been taken since the start and h(n) is the manhattan distance of that node from the goal.<br>
<p></p>
<b>A* Search</b> is optimal if:<br>

- h(n) is admissible (never overestimates the true cost), and<br>
- h(n) is consistent (for every node <i>n</i> and successor <i>n'</i> with step cost <i>c</i>, h(n) <= h(n') + c)
<p></p>
<i><b>Minimax</b></i><br>
It is an algorithm where the player tries to maximise it's score and tries to minimise the opponent's score.<br>

- Max(Player) aims to maximize score.
- Min(Opponent) aims to minimize score.

In the game, it contains certain elements<br>

- s0: Initial State
- Player(s): returns which player to move in state s
- Actions(s): returns legal moves in state s
- result(s,a): returns state after action a taken in state s
- Terminal(s): checks if state s is a terminal state
- Utility(s): final numerical value for terminal state s (For a game, 1 if player wins, 0 for draw and -1 if opponent wins)

<p></p>
