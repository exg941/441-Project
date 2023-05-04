# 441-Project

ABSTRACT
In this game, the player must traverse the world between various cities to get to the end goal. The city placements and routes between them are randomly generated as well as the starting position of the Reaper. Traveling also costs money depending on how far away the two cities are from each other. While traveling between cities, the player may encounter a bandit and will have to fight to survive. Fights are not all scary, however, because each win awards gold which is essential to make it to the end. The actual thing to be scared of is the Reaper which will end the game if the player encounters it.

The game includes a few AI components to help it run, including the agents that control enemies which are touched on next.

Run the game through the 'agent_enviroment' file as it contains the main game loop. You can choose to play the game yourself or have the Player Agent give it a go.

AI COMPONENTS
1. Reaper Agent
2. Player Agent
3. Bandit Agent
4. GA System

PROBLEMS SOLVED
--Reaper Agent--
The Reaper character adds another layer of difficulty to the game by instantly ending the game if the Player ever comes into contact with him. The Player will need to choose whether to try and stay as far as possible from him or risk an encounter and lose everything. The Reaper and the Player always move towns at the same time and the Reaper always has a record of the Player's current location. The Reaper will then choose one of the adjacent cities to travel to using pathfinding to choose which city to travel to next to get closer to the Player. The Reaper teleports from city to city, so the Player will never run into him while traveling. Game over happens only if the Reaper and the Player are in the same city at the same time.

--Player Agent--
The Player Agent is capable of playing the entire game without human input.

--Bandit Agent--
The Bandits are the primary adversary for the Player as they are traveling between cities. When attacked, the Player and the Bandit will have a rock-paper-scissor type battle where they both pick a weapon and the owner of the losing weapon also loses health. The battle ends when one of the parties' health reaches 0. If the Player loses, it's game over. If the Player wins, they get a random amount of gold between 10-20. The Bandit chooses their weapon with conditional statements based on their own health.

--GA System--
The GA System helps create a more realistic environment for the Player to traverse. The system aims to spread out the cities apart from each other and keep them away from areas of incredibly high and low elevation.

APPENDIX
--Chat GPT Conversation that Inspired the Reaper--
ME: What's an easy ai component that I can include in my pygame project?
GPT: One easy AI component that you can include in your Pygame project is a simple decision-making algorithm. For example, you could create a game where an enemy character moves around the screen and tries to catch the player-controlled character. You could use a basic algorithm to control the movement of the enemy character, such as a simple "chase" behavior where the enemy moves towards the player's position.

Here's an example of how you could implement this algorithm using Pygame:

Create a "Player" class that represents the player-controlled character. This class should have attributes for the player's position on the screen, as well as methods for moving the player.

Create an "Enemy" class that represents the enemy character. This class should also have attributes for the enemy's position on the screen, as well as methods for moving the enemy.

In your game loop, update the positions of both the player and the enemy characters.

To implement the "chase" behavior for the enemy, you could use a simple algorithm like this:

Calculate the distance between the enemy and the player using the Pythagorean theorem.
If the distance is greater than a certain threshold, move the enemy towards the player's position using a simple "move towards" algorithm. You can do this by calculating the direction from the enemy to the player and then moving the enemy a small distance in that direction each frame.
If the distance is less than the threshold, the enemy has caught the player and the game is over.
This is just one example of a simple AI component that you can include in your Pygame project. Depending on the complexity of your game, you may want to explore more advanced AI techniques like pathfinding or machine learning.

--Chat GPT Conversation to Help the Reaper in its Pathfinding--
ME: Write a pathfinding algorithm in python that returns the next node in the shortest path to the goal
GPT: Sure, here's an implementation of Dijkstra's algorithm in Python that returns the next node in the shortest path to the goal:

```python
import heapq

def dijkstra(graph, start, goal):
    """
    Implementation of Dijkstra's algorithm that returns the next node in the shortest path to the goal.

    Args:
    - graph (dict): a dictionary representing the graph where the keys are the nodes and the values are lists of tuples representing the edges and their weights.
    - start (any): the starting node.
    - goal (any): the goal node.

    Returns:
    - The next node in the shortest path to the goal.
    """
    # Initialize the distance and visited dictionaries
    distance = {node: float('inf') for node in graph}
    distance[start] = 0
    visited = {}

    # Initialize the priority queue
    pq = [(0, start)]

    while pq:
        # Get the node with the smallest distance
        (dist, current_node) = heapq.heappop(pq)

        # If we've reached the goal, return the next node in the shortest path to the goal
        if current_node == goal:
            return visited[goal]

        # If the node has already been visited, continue
        if current_node in visited:
            continue

        # Mark the node as visited
        visited[current_node] = None

        # Update the distances to the neighboring nodes
        for (neighbor, weight) in graph[current_node]:
            new_distance = dist + weight
            if new_distance < distance[neighbor]:
                distance[neighbor] = new_distance
                heapq.heappush(pq, (new_distance, neighbor))
                visited[neighbor] = current_node

    # If we've gone through the entire graph and haven't found the goal, return None
    return None
```

Note that this implementation assumes that the graph is represented as a dictionary where the keys are the nodes and the values are lists of tuples representing the edges and their weights. The `visited` dictionary keeps track of the previous node for each visited node, which allows us to reconstruct the shortest path later.