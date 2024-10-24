# Maze-Game
## Search-Algorithms-Depth-First-Search-DFS
This Python script is designed to solve a maze using the depth-first search (DFS) algorithm. Let’s break it down step by step:

### 1. **Node Class**:
- **Node** is a fundamental building block in searching algorithms. Each node represents a single state (or position) in the maze.
- It stores:
  - `state`: The position of the node in the maze (as coordinates, like `(row, column)`).
  - `parent`: A reference to the parent node, which helps trace the path back once we find the solution.
  - `action`: The direction taken to reach this node (like "up", "down", etc.).

### 2. **StackFrontier Class**:
- This class manages the *frontier*, which is the set of nodes we can explore next.
- A **stack** is used (Last In, First Out structure) because DFS uses this approach.
  - `add(node)`: Adds a node to the frontier.
  - `contains_state(state)`: Checks if a specific state (position) is already in the frontier.
  - `remove()`: Removes and returns the most recently added node (the one on top of the stack).
  - `empty()`: Checks if the frontier is empty (i.e., no more nodes to explore).

### 3. **QueueFrontier Class** (inherits StackFrontier):
- This class modifies the `remove()` method to behave like a queue (First In, First Out), which is used in breadth-first search (BFS).
- Instead of removing the last node added, it removes the first one added.

### 4. **Maze Class**:
This is the core class that reads the maze from a file, solves it, and outputs both a text-based and image-based solution.

- **`__init__(self, filename)`**:
  - Reads the maze file (provided as `maze.txt`) and determines the maze’s size, including its height and width.
  - Identifies the start (`A`) and goal (`B`) positions.
  - It also creates a 2D array (`self.walls`) that stores whether each cell in the maze is a wall (True) or empty (False).

- **`print(self)`**:
  - Prints the maze in a human-readable format, showing walls as "█", start as "A", goal as "B", and the solution path as "*".

- **`neighbors(self, state)`**:
  - Given a position in the maze, this method returns all possible neighboring positions that can be moved to (up, down, left, or right), as long as they are not blocked by walls.

- **`solve(self)`**:
  - The method that solves the maze using DFS:
    1. It starts by creating a `Node` for the starting point (`A`) and adding it to the frontier.
    2. Then it explores nodes one by one, checking if each node is the goal (`B`).
    3. If a node reaches the goal, it backtracks to construct the solution path.
    4. If a node is not the goal, it adds its unexplored neighbors to the frontier.
    5. If no solution is found (i.e., the frontier is empty), it raises an exception.

- **`output_image(self, filename)`**:
  - Uses the Python Imaging Library (PIL) to generate an image of the maze.
  - It colors the walls, the start, the goal, the solution path (if found), and optionally the explored states.

### 5. **Main Code Logic**:
- The script expects a command-line argument that specifies the filename of the maze (e.g., `python maze.py maze.txt`).
- It then:
  1. Initializes the `Maze` object with the given file.
  2. Prints the maze.
  3. Attempts to solve the maze using DFS.
  4. Displays the number of states explored and the solution path.
  5. Saves an image of the solved maze, showing both the solution and the explored states.

### Example:

If you had a file `maze.txt` like this:

```
A ####
#    #
# ## #
#  B #
######
```

Running the script would:
1. Read the maze from the file.
2. Solve it using DFS.
3. Print out the solved maze, showing the path from `A` to `B` with `*` symbols.
4. Create an image of the maze with colors representing different elements.

### Key Points:
- **DFS (Depth-First Search)** is used to explore the maze. This explores as deep as possible before backtracking.
- The `Maze` class handles reading the maze, solving it, and visualizing the solution.
- The `StackFrontier` manages the nodes to be explored (using a stack for DFS), while `QueueFrontier` would manage them differently (for BFS).
