# The Mystery of Marshall Mansion Murder

## Introduction
- "The Mystery of Marshall Mansion Murder" revolves around a captivating incident that occurred during a Christmas dinner at the esteemed Marshall Mansion.
    - The protagonist is invited to join a private gathering at the mansion by an acquaintance named Rivers.
    - Rivers was adopted by Mr. Phillip Marshall, the wealthy owner of the mansion, at a young age and assists him with the management of his business affairs.
    - The dinner is attended by approximately 15 individuals, including Mr. Marshall's children, siblings, uncle, and intimate friends of the family.
- The evening commences with a delightful feast but is abruptly shattered when Mr. Marshall experiences a sudden medical emergency and tragically passes away.
- The untimely demise of Mr. Marshall under mysterious circumstances forms the basis of the captivating story.
    - The protagonist becomes immersed in a quest to unravel the truth behind the enigmatic murder at Marshall Mansion.
    - The story delves into a thrilling journey as the protagonist untangles the secrets, motives, and potential suspects connected to the haunting event.
    - The climax will keep readers on the edge of their seats.

## Part 1: Who poisoned Marshall?

### Discussion
- A few moments before Mr. Marshall passed away, he whispered, “I know who did this”.
    - As a detective working for the Police department in the city, the protagonist realizes that this was not an accident but instead a murder.
- After the mansion is closed for investigation and everyone has left, the protagonist begins looking for clues.
    - The mansion is a large building with many rooms, situated on a huge piece of land with a lake.
    - The protagonist manages to obtain a layout of the building and the surrounding areas.
    - The main building is suspected to contain clues, so the protagonist decides to search all the rooms.

![Picture](https://i.imgur.com/MpKEjjL.png)

### Problem
How to search all the rooms in the building without missing any?

- Problem: There is a clue to find who murdered Mr. Marshall in one of the rooms in the main building. In order to find the clue, all the rooms in the main building need to be searched.
    - There are three possible algorithms that can be implemented to search all rooms in the mansion: **Linear Search, Breadth-First Search, and Depth-First Search**.
- Assumptions:
    1. The search will start at the entrance of the ground floor.
    2. The balconies, courtyard, and stair will be considered as rooms.
    3. There are three balconies and two utilities that will be labeled as balcony 1, balcony 2, balcony 3, utility 1, and utility 2.
    4. All the rooms will be searched although clues have been found.
- Based on these assumptions, there are three algorithms suitable to solve the problem: Linear Search, Breadth-First Search, and Depth-First Search.

|Algorithm|Linear Search|Breadh-First Search|Depth-First Search|
|---------|-------------|-------------------|------------------|
|Complexity|Simple|Moderate|Moderate|
|Data structure|List|Unweighted graph|Unweighted graph|
Advantage|Easy to implement as it require minimal and simple code|Guarantees finding the shortest path between two vertices in an unweighted graph|Beneficial for problems that require backtracking or pruning of search spaces|
|Limitation|Require visiting each room sequentially. Since the roon in the mansion is not in linear structure and has multiple routes to search all the rooms in the mansion, this algorithm is not suitable for efficiently exploring all the rooms|Since there are multiple rooms connecting to each other, it can potentially result in redundant visits to some rooms as some rooms will be explored multiple times|Will explore to the farthest room in the 1st floow before backtracking and return to the ground floow again without finishing exploring the 1st floor. This would be time consuming and inefficient|

- BFS is the most suitable algorithm for exploring all the rooms in the mansion.
    - Linear search is limited to handling simple lists and would require sorting the list of rooms first, making it less efficient.
    - DFS explores the mansion by going as deep as possible before backtracking, which can significantly increase the time taken to explore all the rooms compared to BFS.
    - BFS explores the mansion in a breadth-first manner, visiting all neighboring rooms before moving on to the next level of rooms. This ensures that all reachable rooms are visited and can be useful when finding the shortest path or determining connectivity between rooms.
- In summary, BFS is selected due to its ability to efficiently visit all reachable rooms, handle non-sequential lists, and ensure comprehensive coverage of the entire mansion.

### Pseudocode
1. Define the adjacency list representing the mansion's rooms.
2. Define the BFS function that takes the starting room as input.
3. Create an empty set to keep track of visited rooms and an empty queue.
4. Enqueue the starting room with "No clue" status and run the BFS algorithm.
5. While the queue is not empty, dequeue a room and its clue status from the queue.
6. If the room has not been visited, mark it as visited and get its neighbors from the adjacency list.
7. Check the clue status based on the current room's clue status, print it, and enqueue the neighbors with the updated clue status.
8. Perform BFS starting from the "entrance" on the ground floor.

### Running Time Complexity
- The running time complexity of the provided code is dependent on the number of rooms (n) and the connections between them in the mansion.
- In the worst-case scenario, where all rooms are interconnected, the BFS algorithm will visit each room exactly once with a time complexity of O(1) for visiting each room and its neighbors.
- Since the problem requires searching all rooms in the mansion, the best-case and average-case will be similar to the worst-case scenario.
- Therefore, the overall time complexity of the BFS algorithm is O(n), assuming that accessing the adjacency list and performing operations on the queue take constant time.

### Code
```
from collections import deque

# Define the adjacency list representing the mansion's rooms
adjacency_list = {
    "entrance": {"neighbors": ["main hall"], "clue": False},
    "main hall": {"neighbors": ["utility", "dining"], "clue": False},
    "dining": {"neighbors": ["balcony", "main hall", "kitchen"], "clue": False},
    "balcony": {"neighbors": ["dining", "kitchen"], "clue": False},
    "kitchen": {"neighbors": ["balcony", "dining", "courtyard"], "clue": False},
    "courtyard": {"neighbors": ["kitchen", "library"], "clue": False},
    "library": {"neighbors": ["courtyard", "stair"], "clue": True},
    "utility": {"neighbors": ["main hall"], "clue": False},
    "stair": {"neighbors": ["library", "room 1", "utility 2"], "clue": False},
    "room 1": {"neighbors": ["stair"], "clue": False},
    "utility 2": {"neighbors": ["stair", "master bedroom", "balcony 3"], "clue": False},
    "master bedroom": {"neighbors": ["utility", "room 2", "balcony 3"], "clue": False},
    "room 2": {"neighbors": ["master bedroom", "room 3", "balcony 2", "balcony 3"], "clue": False},
    "room 3": {"neighbors": ["room 2", "balcony 2"], "clue": False},
    "balcony 2": {"neighbors": ["room 3", "room 2", "balcony 3"], "clue": False},
    "balcony 3": {"neighbors": ["utility", "master bedroom", "room 2", "balcony 2"], "clue": False},
}

def bfs(start_room):
    visited = set()
    queue = deque([(start_room, "No clue")])

    while queue:
        room, clue_status = queue.popleft()
        if room not in visited:
            visited.add(room)
            neighbors = adjacency_list[room]["neighbors"]
            if adjacency_list[room]["clue"]:
                clue_status = "Found clue!!!"
            else:
                clue_status = "Found nothing...."
            print("Visited:", room, "-->", clue_status)
            queue.extend((neighbor, clue_status) for neighbor in neighbors)

# Perform BFS starting from the "entrance" on the ground floor
print("Begin searching:")
bfs("entrance")
```