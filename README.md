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

