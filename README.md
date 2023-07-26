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

## Part 2: Cracking the Chest Lock Code

### Discussion
![Picture](https://i.imgur.com/o0KU4X6.png)

- Problem: To open the old safe, the correct 3-digit number combination is needed. Since the actual code is not known, multiple combinations must be tried until the safe opens.
- Assumptions:
    1. The actual 3-digit number combination is assumed to be a randomized number between 0 to 999.
- There are three ways to find the correct combination:
    1. Exhausting all combinations using brute force algorithms.
    2. Using a binary search algorithm to narrow down the possible combinations.
    3. Using a randomized guessing algorithm where the program will keep guessing using random combinations until the safe is open.

|Algorithm|Brute Force Algorithm|Binary Search Algorithm|Randomized Guessing Algorithm|
|---------|---------------------|-----------------------|-----------------------------|
|Introduction to algorithm|A straightforward method os solving a problem that relies on sheer computing power and trying every possibility rather than advanced techniques to improve efficiency. In this case, we'll try every possible lock combination starting from 000 yo 999.|A methof used to find the position of a specific value, in this case the correct code in a sorted array. It works with the principle of divide and conquer.|A method that is self explanatory. The program will randomly pick a number and try it> If it fails, it'll try a different number until the safe is open|
|Advantages|A guaranteed way to find the correct solution by listing all the possible candidate solutions for the problem|Faster especially for large arrays|Utilizes random guessing strategy. This allows it to potentially crack the code in fewer attempts on average|
|Limitations| Inefficient. The time complexity goes above O(n!)|Data must be ordered|The larger the space, the longer it takes to finish|
|Modifications|Instead of letting the algorithm go through all the possible combinations, it will stop when it finds the correct one|Initial guess is randomized. This will allow it to potentially crack the code in fewer attempts on average|Create a list of guessed numbers to prevent the program from guessing the same number multiple times|

- The chosen algorithm is the Randomized Guessing Algorithm.
    - It is the 2nd fastest algorithm and is more realistic and practical to use in this situation.
    - It does not require prior knowledge of the combination like the Binary Search Algorithm.
    - It uses the element of randomness, allowing it to crack the code in fewer attempts than the brute force algorithm.

### Pseudocode
1. Pick a random number between a given range.
2. Try the number.
3. If the lock opens, the current combination is the correct one.
4. If it fails, repeat steps 1-3 until the correct combination is found.

### Running Time Complexity
- The running time complexity of the Randomized Guessing Algorithm is O(1000), which can be simplified as O(1) because the upper bound is fixed.
    - Compared to the other two algorithms, it shares the same time complexity as the Brute Force Algorithm but is better due to its randomness.
    - The Binary Search Algorithm has a lower time complexity of O(log n) but is not suitable for this situation.
- Best case: The first attempt correctly guesses the desired solution, denoted as O(1).
- Average case: Proportional to the number of possibilities, with an expected value of O(500), which simplifies to O(1).
- Worst case: After guessing all possible solutions, denoted as O(1000) or O(n).

### Code
```
import random
print("Randomized Guessing Algorithm")
code = random.randint(0,999)
guess = random.randint(0,999)
guessed = []
while(guess!=code):


    guessed.append(guess)
    while guess in guessed:
        guess=random.randint(0,999)

print("Case cracked. Code is "+str(code).zfill(3))
```

## Part 3: Same But Not Identical

### Discussion
For part 3, we need to identify differences between two letters that seem to be
identical but are actually not. Those differences are needed in order to find the next
clue for part 4. The letter are as below:

![Picture](https://i.imgur.com/5luPDap.png)

- Problem: Point out every single difference detected between two letters.
- Assumptions:
    1. Any differences in spelling will be considered as different words.
    2. The order of the different words is not important, only the words are compulsory.
- Based on these assumptions, the problem could be solved using the Longest Common Subsequences Algorithm, which works best for finding differences between two sequences.
- Other algorithms that could be used to solve the problem include Merge Sort and Quick Sort.

|Algorithm|Merge Sort|Quick Sort|Longest Common Subsequences|
|---------|----------|----------|---------------------------|
|Introduction to Algorithm|Merge sort is a recursive sorting algorithm that operates by dividing the unsorted list into smaller sublists, sorting them individually, and then merging them back together to obtain a sorted result|Follows a divide-and-conquer apprach> It starts by selecting a pivot element from the array and partitioning the other elements into two subarrays, according to whether they are less than or greated than the pivot. The pivot is then in its final sorted position|A method that finds the longest shared between two or more sequences. It works by comparing elements and creating a table to track the common elements.|
|Advantages|Provide stable and predictable performance|In-place partitioning and recursive nature reduce the need for additional memory|Efficiently finds the longest common subsequence, which helps identify the common elements between the two letters|
|Limitations|It only compares correcponding elements during the merging process|It does not consider higher-;evel linguistic structures or semantinc meaning|The time and space complexity of the algorithm can be relatively high, especially for larger inputs|

- The Longest Common Subsequences Algorithm is the chosen algorithm but it needs to be modified to record the differences between the two letters.
    1. The modified LCS algorithm tracks elements that are not part of the common subsequence.
    2. A backtracking step is introduced to trace the table, identify differing elements, and mark or store them in a separate list or data structure.
    3. During backtracking, the algorithm compares elements from the original letters to determine differences, considering their positions and order.

### Pseudocode
1. Create a function `lcsCompare` that takes `arr1`, `arr2`, `differences1`, and
`differences2` as input.
2. Implement `initializeTable` to create a table and initialize its first row and column.
3. Develop `fillTable` to populate the table based on the elements of `arr1` and `arr2`.
4. Create `backtrack` to trace the table and identify the differences between `arr1` and
`arr2`.
5. Implement `markDifference` to add non-matching elements to the respective
difference lists.
6. Inside `lcsCompare`, call `initializeTable`, `fillTable`, and `backtrack` in sequence.
7. The differences will be stored in `differences1` and `differences2` for further use.

### Running Time Complexity
- Best case: The two input arrays (letters) have no differences and are identical. The time complexity is O(m*n), where m and n represent the lengths of the input arrays.
- Average case: The two input arrays have some common elements and some differences. The time complexity is also O(m*n), with additional time proportional to the length of the LCS for backtracking and printing.
- Worst case: The two input arrays have no common elements and every element is different. The time complexity is O(m*n), where m and n represent the lengths of the input arrays.

### Code
```
def lcsCompare(arr1, arr2, differences1, differences2):
    m = len(arr1)
    n = len(arr2)
    # Initialize the table with zeros
    table = [[0] * (n+1) for _ in range(m+1)]
    # Fill the table
    for i in range(1, m+1):
        for j in range(1, n+1):
            if arr1[i-1] == arr2[j-1]:
                table[i][j] = table[i-1][j-1] + 1
            else:
                table[i][j] = max(table[i-1][j], table[i][j-1])
    # Backtrack to find the differences
    i = m
    j = n
    while i > 0 and j > 0:
        if arr1[i-1] == arr2[j-1]:
            i -= 1
            j -= 1
        elif table[i-1][j] >= table[i][j-1]:
            markDifference(arr1[i-1], None, differences1, differences2)
            i -= 1
        else:
            markDifference(None, arr2[j-1], differences1, differences2)
            j -= 1

    while i > 0:
        markDifference(arr1[i-1], None, differences1, differences2)
        i -= 1

    while j > 0:
        markDifference(None, arr2[j-1], differences1, differences2)
        j -= 1

def markDifference(element1, element2, differences1, differences2):
    if element1 is not None:
        differences1.append(element1)
    if element2 is not None:
        differences2.append(element2)

def store_essays():
    essays = []
    for i in range(2):
        essay = []
        print(f"Enter your {i + 1} essay. Press Enter on an empty line to finish.")
        while True:
            line = input()
            if line == "":
                break
            words = line.split() # Split the line into words
            essay.extend(words) # Add the words to the essay list
            essays.append(essay)
            return essays

# Example usage
essays_array = store_essays()
arr1 = essays_array[0]
arr2 = essays_array[1]

differences1 = []
differences2 = []

lcsCompare(arr1, arr2, differences1, differences2)

print("Differences in Letter 1:")
print(' , '.join(differences1))
print("\nDifferences in Letter 2:")
print(' , '.join(differences2))
```

## Part 4: Find That Book

### Discussion
- Problem: Find the possible book title in the library in the quickest time from the different words found between the two letters in Part 3.
- Assumptions:
    - The book title is derived from different words found in the second letter.
    - The unique words ‘Great’, ‘Winter’, ‘Night’, and ‘Fun time’ are potential candidates for the book title.
- Suggested algorithms to solve this problem include binary search, brute force algorithm, and Rabin-Karp algorithm.

| |Binary Search Algorithm|Brute Force Algorithm|Rabin-Karp Algorithm|
|-|-----------------------|---------------------|------------------|
Introduction to Algorithm|Binary Search is a divide-and-conquer that can be used to search for a value in a sorted list. It works by repeatedly dividing the list in half and searching the smaller half until the value is found|A simple algorihtm that can be used to search for a value in a list. It works by simple comparing the value to each item in the list until it is found|A hash-based algorithm that can be used to search for a value in a list. It works by creating a hash value for the value that we are searching for. The hash value is a unique identifier for the value, and it can be used to quickly compare the value to the items in the list|
|Advantages|A very efficient algorithm. It can find the value in a sorted list in logarithmic time|A simple algorithm. It is easy to understand and implement|It can find the value in a list in linear time. This means that the time it takes to find the value increases as the size of the list increases|
|Limitations|Requires the list to be sorted before it can be used|Inefficient for large lists. This is because the algorithms needs to compare the value to each item in the list.|Relies on a good hash function to generate the hash values for the test and pattern strings. If the hash function is not good, then the algorithm may not be able to find the pattern in the text.|

- The chosen algorithm is the binary search algorithm.
    - The books in the library are sorted alphabetically, allowing binary search to quickly narrow down the search space by repeatedly dividing it in half.
    - This significantly reduces the number of comparisons needed compared to brute force or Rabin-Karp algorithm.
- To use binary search for this problem, some modifications are needed:
    - Instead of searching for a single target element, the algorithm searches for multiple target words within the book titles.
    - The modification involves using the all() function and a list comprehension to check if all the target words are present in the current book title within the binary search loop.

### Pseudocode
1. Initialize the low and high pointers to 0 and the length of the list, respectively.
2. While the low pointer is less than or equal to the high pointer:
    a. Calculate the middle pointer by taking the average of the low and high pointers.
    b. Compare the value to the item at the middle pointer.
        i. If the value is equal to the item at the middle pointer, then the value has been found and the algorithm returns the middle pointer.
        ii. If the value is less than the item at the middle pointer, then the value must be in the lower half of the list. In this case, set the low pointer to the middle pointer + 1.
        iii. If the value is greater than the item at the middle pointer, then the value must be in the upper half of the list. In this case, set the high pointer to the middle pointer - 1.
3. Return -1 if the value is not found.

### Running Time Complexity
- The running time complexity of the binary search algorithm is generally O(log n), where n represents the number of books in the library.
- Best case: The target words are found at the beginning of the list, taking constant time, O(1).
- Average case: The target words are randomly distributed throughout the list, taking a running time complexity of O(log n).
- Worst case: The target words are not found in the list, taking a running time complexity of O(log n).

### Code
```
def binary_search(target_words, book_list):

    # sort the books alphabetically
    book_library.sort()

    start = 0
    end = len(book_list) - 1

    while start <= end:
        mid = (start + end) // 2
        mid_title = book_list[mid].lower()

        if all(word.lower() in mid_title for word in target_words):
            return mid
        elif mid_title < target_words[0].lower():
            start = mid + 1
        else:
            end = mid - 1

    return -1

def find_book(target_words, book_library):
    lower_target_words = [word.lower() for word in target_words]

    for index, title in enumerate(book_library):
        lower_title = title.lower()
        if all(word in lower_title for word in lower_target_words):
            print(f"Book containing all target words [ {', '.join(target_words)} ] found : '{title}', Index : {index}")
            return

    print(f"Book containing all target words '{', '.join(target_words)}' not found in the library.")


def search_books(target_words, book_library):
    find_book(target_words, book_library)


# library book list
book_library = [
        "The Alchemist", "To Kill a Mockingbird", "The Great Gatsby", "1984", "Harry Potter and the Sorcerer's Stone",
        "The Lord of the Rings", "The Hunger Games", "The Catcher in the Rye", "The Da Vinci Code", "Gone Girl",
        "The Girl With the Dragon Tattoo", "The Book Thief", "The Curious Incident of the Dog in the Night-Time", "The Martian", "Where the Crawdads Sing",
        "The Hitchhiker's Guide to the Galaxy", "The Kite Runner", "The Help", "The Fault in Our Stars", "Me Before You",
        "The Book of Negroes", "The Girl on the Train", "The Woman in the Window", "The Shack", "Americanah",
        "Educated", "Where the Wind Leads", "The Nightingale", "The Alice Network", "The Guernsey Literary and Potato Peel Pie Society",
        "The Seven Husbands of Evelyn Hugo", "The Midnight Library", "The Giver of Stars", "Pachinko", "The Four Winds",
        "The Last Days of Ptolemy Grey", "The Book of Longings", "The Lincoln Highway", "Malibu Rising", "The Thursday Murder Club",
        "The House in the Cerulean Sea", "The Ministry for the Future", "Project Hail Mary",
        "The Great Winter Night Time", "Don Quixote", "War and Peace", "Ulysses", "Pride and Prejudice", "In Search of Lost Time", "Great Expectations",
        "Adventures of Huckleberry Finn", "Crime and Punishment", "Mody-Dick", "Hamlet", "The Odyssey", "The Iliad", "The Adventures of Tom Sawyer",
        "Little Women", "Jane Eyre", "The Scarlet Letter", "The Adventures of Don Quixote", "The Metamorphosis", "The Grapes of Wrath", "Things Fall Apart",
        "The Color Purple", "The Handmaid's Tale", "The God of Small Things", "The Time Traveler's Wife", "Divergent", "The Secret History", "Animal Farm",
        "The Diary of a Young Girl", "The Little Prince", "Romeo and Juliet", "The Chronicles of Narnia", "Fahrenheit", "The Giver",
        "Charlotte's Web", "Of Mice and Men", "Wuthering Heights", "Night", "Gone With the Wind", "The Picture of Dorian Gray", "Brave New World",
        "Les Miserable", "Memoirs of a Geisha", "The Secret Garden", "A Christmas Carol", "The Advantures of Tom Sawyer",
        "Ender's Game", "One Hundred Years of Solitude", "A Tale of Two Cities", "The Outsiders", "Anne of Green Gables", "Winnie The Pooh",
        "A Thousand Splendid Suns", "Life of Pi", "Tuesday With Morrie", "The Count of Monte Cristo", "Catch-22", "Anna Karenina", "Flowers for Algernon",
        "Slaughterhouse-Five", "The Old Man and the Sea", "Frankenstein", "MacBeth", "Lolita", "Siddhartha", "Little House Series",
        "A Tree Grows in Brroklyn", "A Clockwork Orange", "Uncle Tom's Cabin", "The Stand", "Atles Shrugged", "All Quiet on the Western Front",
        "The Poisonwood Bible", "The Brothers Karamazov", "The Good Earth", "I Know Why the Caged Bird Sings", "A Wrinkle in Time",
        "Dracula", "Matilda", "Sense and Sensibility", "The Perks of Being a Wallflower", "Complete Tales and Poems", "Fountainhead",
        "Where the Red Fern Grows", "The Princess Bride", "East of Eden", "The Lovely Bones", "Charlie and the Chocolate Factory", "Watership Down",
        "The Five People You Meet in Heaven", "A Prayer for Owen Meany", "Rebecca", "Angel's Ashes", "Perfume", "The Bell Jar", "The Call of the Wild",
        "Dune", "Bridge of Terabithia", "Water for Elephants", "The Divine Comedy", "A Midsummer Night's Dream", "The Three Musketeers",
        "The Name of the Rose", "Persuasion", "The Red Tent", "The Road", "The Girl with the Dragon Tattoo", "The Pillars of the Earth", "Oliver Twist",
        "The Canterbury Tales", "And Then Were None", "The Secret Life of Bees", "His Dark Materials Trilogy", "On the Road", "Heart of Darkness",
        "Love in the Time of Cholera", "The Master and Margarita", "The Shadow of the Wind", "Interview With the Vampire", "Invisible Man", "In Cold Blood",
        "Aesops Fables", "Gulliver's Travels", "The Origin of Species", "Walden", "Roots", "The Glass Castle", "The Boy in the Striped Pajamas",
        "Sophie's World", "The Screwtape Letters", "Robinson Crusoe", "The Strange Case of Dr. Jekyll and Mr. Hyde", "Candide", "The Prince",
        "The Complete Sherlock Holmes", "Fight Club", "The Art of War", "The Mists of Avalon", "The Time Machine", "Watchmen", "The Godfather", "The Trial",
        "The Sun Also Rises", "Tuck Everlasting", "Stranger in a Strange Land", "Emma", "Atonement", "The Complete Brothers Grimm Fairy Tales", "Beloved",
        "James and the Giant Peach", "Leaves of Grass", "Bury My Heart at Wounded Knee", "The Things They Carried", "Their Eyes Were Watching God",
        "The Phantom Toolbooth", "Number the Stars", "Middlesex", "The World According to Garp", "A Separate Peace", "Great Winter Night Time",
        "Winter Night : A Great Time for Fun"
]

target_words = input("Enter the target words (separated by SPACE): ").split()
search_books(target_words, book_library)
```

## Part 5: Secret Message