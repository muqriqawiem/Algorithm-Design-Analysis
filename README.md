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

### Discussion
- Problem: Decode a specific secret message to find the next clue to Part 6.
- The secret message are as below:
    ```
    Ymfy ujwxts nx htrnsl ktw rj! Nk dtz knsi ymnx styj, qttp fwtzsi rd
    uwtujwyd. Mnsy: N anxnyji ymj fwjf bnym rd ywtqqjd kwtr ymj lfwijs
    xmji.
    ```
- Assumptions:
    1. The secret message is short and cannot be decoded using advanced algorithms such as Frequency Analysis Algorithm or Index of Coincidence (IOC).
    2. The victim, being a businessman, might not have knowledge of professional encryption strategies and might have used his creativity to create the secret message.
    3. There might be a clue left by the victim on how to decode the secret message.
- Based on these assumptions, the secret message was likely implemented using a simple encryption method and could be solved using the Brute Force Algorithm.
    - Notable variations of the algorithm that could be used include Caesar Cipher, Vigenere Cipher, and Transposition Cipher.
    - To choose the best variation, a comparison check is needed.

| |Caesar Cipher|Vignere Cipher|Transposition Cipher|
|-|-------------|--------------|--------------------|
|Introduction to Algorithm|A simple substitution cipher where each letter in the message is shifted a certain number of positions down or up the alphabet. To decode a message encoded with a Caesar Cipher, we can apply the opposite shift to each letter|Works by using a keyword or phrase to determine multiple letter shofts during decryption. Each letter of the message is shifted based on the corresponding letter of the keyword. This creates a more complex encryption pattern compared to the simple letter shofting of the Caesar Cipher. To decode the message, the same keyword is used to reverse the shifting process and retrieve the original message.|Transposition cipher works by rearranging the order of characters in the message based on a predetermined key. By applying the key's arrangement pattern in revese, the recipient can restore the original order of the character and reveal the message. Transposition ciphers do not change the actual characters but manipulate their positions, making it important to know the correct ket yo successfully decode the message|
|Key parameter| Shift value|Repeating keyword|Transposition rule|
|Security level|Relatively weak|Stronger than Caesar cipher if keyword is long|Security depends on complexity and secrecy of the transposition rule|
|Limitation|Limited key space - the caesar cipher has a fixed key space of 25 possibilities since there are only 25 potential shifts in the English alphabet. This means that if the actual key used for encryption if not known, we would need to try all possible shifts to find the correct decryption|Keyword dependency - requires knowledge of the keyword used during the encryption. If the length of the keyword is unknown, it is hard to determine the exact key length. If the keyword is long or randomly generated, decryptinh the message without the correct key becomes extremely difficult|Keyword dependency - heavily relies on the knowledge of the correct key or arrangement pattern used during encryption. Without the correct key, it becomes extremely difficult to decrypt the message accurately.|

- The chosen variation of the Brute Force algorithm is the Caesar cipher.
    - It provides the best solution for simple decoding problems and is suitable for the assumed lower security level of the secret message.
    - The clue left behind by the victim in the secret message is assumed to be the negative integer (-5), which stands out as a pattern by itself.
    - Out of all three variations, only the key for Caesar cipher needs to be in a single integer value.

### Pseudocode
1. Initialize an empty string called plaintext to store the decrypted message.
2. Iterate through each character, denoted as char, in the given ciphertext.
3. If char is alphabetic:
    i. Determine the ASCII offset based on whether char is lowercase or uppercase.
    ii. Decrypt the character by subtracting the ASCII offset and the given shift value, then take the modulo 26 and add the ASCII offset back.
    iii. Append the decrypted character, denoted as decrypted_char, to the plaintext.
4. If char is not alphabetic, simply append it to the plaintext.
5. Return the plaintext as the decrypted message.
6. Set the ciphertext as the encrypted message you want to decrypt.
7. For each shift value from 1 to 25:
    i. Decrypt the ciphertext using the current shift value in a forward direction and store it in a variable called decrypted_message_forward.
    ii. Decrypt the ciphertext using the negative of the current shift value in a backward direction and store it in a variable called decrypted_message_backward.
    iii. Print both decrypted messages for the current shift value and a blank line to improve readability.

### Running Time Complexity
- The running time complexity of the Caesar cipher algorithm is generally O(n), where n represents the length of the message being decoded.
- Best case: The shift value is 0, meaning no decryptions are needed. The time complexity is O(1) or constant time.
- Worst case: The shift value is at its max (25), meaning the algorithm needs to iterate through the problem 25 times to perform shifts on the characters. The time complexity is O(n).
- Average case: The total number of shifts is between the best and worst case (not 0 and 25). The time complexity is still O(n).

### Code
```
def caesar_decrypt(ciphertext, shift):
    plaintext = ""
    for char in ciphertext:
        if char.isalpha():
            ascii_offset = ord('a') if char.islower()
        else
            ord('A')
            decrypted_char = chr((ord(char) - ascii_offset - shift) % 26 + ascii_offset)
        plaintext += decrypted_char
    else:
        plaintext += char
    return plaintext

ciphertext = "Ymfy ujwxts nx htrnsl ktw rj! Nk dtz knsi ymnx styj,qttp fwtzsi rd uwtujwyd. Mnsy: N anxnyji ymj fwjf bnym rd ywtqqjdkwtr ymj lfwijs xmji. - 5"
# Try all possible shift values from 1 to 25
for shift in range(1, 26):
    decrypted_message_backward = caesar_decrypt(ciphertext, shift)
    decrypted_message_forward = caesar_decrypt(ciphertext, -shift)
print(f"Shift {shift} (Forward): {decrypted_message_forward}")
print(f"Shift {shift}(Backward):{decrypted_message_backward}")
print()
```

## Part 6: Find The Next Clue

### Discussion
|Item|Weight|
|----|------|
|A sack of corn for the chicken at the barn| 12kg|
|A hoe for the green house|5kg|
|An oil tank filled with fuel for the boat at lake|10kg|
|Four pieces of tyres for the car in the garage|16kg|

- Mr. Marshall visits a shed and discovers a trolley and several items.
- Problem: Find out which item was carried on the trolley.
- The trolley has a maximum weight capacity of 30 kg.
- Assumptions:
    * Items are independent of each other.
    * The trolley has a maximum weight capacity.
- Three proposed algorithms: **Dynamic Programming, Greedy Algorithm, and Brute Force**.

|Algorithm|Dynamic Programming|Greedy Algorithm|Brute Force|
|---------|-------------------|----------------|-----------|
|Introduction to algorithm|An algorithmic technique that solves optimization problems by breaking them into smaller overlapping subproblems. It efficiently stores and reuses computed results to avoid redundant computations, leading to improved time and space complexity| Makes locally optimal choices at each step, hoping to find a globally optimal solution. It selects the best available option at each stage without considering long-term consequences. Greedy algorithms are simple to implement and often provide fast solutions, but they may not always guarantee an optimal solution|A straightforward approach that exhaustively explores all possible solutions to a problem.|
|Advantages|Efficiently solves complex optimization problems by breaking them down into smaller overlapping subproblems|Simple to implement and understand|Guarantees finding an optimal solution by systematically exploring all possible solutions|
|Limitations|If the shed contains a large number of items, the dynamic programming algorithm's memory usage may become a limitation, especially if the available computational resources memory capacity are limited|May select the heaviest item first and continue adding items based on weight until the trolley's capacity is reached|May computationally expensive when deling with larger sets of items|

- **Dynamic Programming** is used to determine which item was carried on the trolley.
- It is well-suited for optimization problems where we want to find the best solution within given constraints.
- Dynamic Programming allows us to explore various combinations of items while considering their weights and the trolley's weight capacity.
- This allows us to find the best combination of items that maximizes the trolley's weight capacity without surpassing it.

### Pseudocode
1. Initialize the number of items as the length of the "items" list.
2. Create a 2D list, "dp," with dimensions (num_items + 1) x (trolley_capacity + 1) and fill it with zeros.
3. Iterate over each item from 1 to num_items:
    a. Get the weight of the current item.
    b. Iterate over each capacity from 1 to trolley_capacity:
        - If the weight of the current item is less than or equal to the current capacity:
            - Set dp[i][capacity] as the maximum value between dp[i-1][capacity] and dp[i-1][capacity - weight] + weight.
        - Otherwise, set dp[i][capacity] as dp[i-1][capacity].
4. Initialize an empty list, "carried_items," and set capacity as trolley_capacity.
5. Retrieve the total weight carried on the trolley from dp[num_items][trolley_capacity].
6. Iterate over the items in reverse order (from num_items to 1):
    - If dp[i][capacity] is not equal to dp[i-1][capacity]:
        - Add the current item and its weight to the "carried_items" list.
        - Decrease the capacity by the weight of the current item.
7. Reverse the order of "carried_items" to correct the item order.
8. Return the "carried_items" list and the total weight.

### Running Time Complexity
- Worst Case: Time complexity is O(n * W), where n represents the number of items and W represents the trolley capacity.
- Best Case: Time complexity is O(1) when the trolley capacity is very small or when the items list is empty.
- Average Case: Time complexity is also O(n * W), assuming a random distribution of item weights and trolley capacity.

### Code
```
def findCarriedItem(items, trolley_capacity):
    num_items = len(items)
    dp = [[0] * (trolley_capacity + 1) for _ in range(num_items + 1)]

    # Filling in the dynamic programming table
    for i in range(1, num_items + 1):
        weight = items[i - 1][1]
        for capacity in range(1, trolley_capacity + 1):
            if weight <= capacity:
                dp[i][capacity] = max(dp[i - 1][capacity], dp[i - 1][capacity - weight] + weight)
            else:
                dp[i][capacity] = dp[i - 1][capacity]

    # Tracking the carried items and remaining capacity
    carried_items = []
    capacity = trolley_capacity
    total_weight = dp[num_items][trolley_capacity]

    # Tracing back to determine the carried items
    for i in range(num_items, 0, -1):
        if dp[i][capacity] != dp[i - 1][capacity]:
            item, weight = items[i - 1]
            carried_items.append(item)
            capacity -= weight

    carried_items.reverse()  # Correcting the order of the carried items

    return carried_items, total_weight


# Example usage
items = [
    ("A sack of corn for the chicken at the barn.", 12),
    ("A hoe for the greenhouse.", 5),
    ("An oil tank filled with fuel for the boat at the lake.", 10),
    ("Two pieces of tires for the car in the garage.", 8),
    ("Two pieces of tires for the car in the garage.", 8)
]
trolley_capacity = 30

carried_items, total_weight = findCarriedItem(items, trolley_capacity)
print("The item(s) carried on the trolley are:")
for item in carried_items:
    print("- " + item)

print("Total weight carried on the trolley:", total_weight)
```

## Part 7: ALmost There!

### Discussion
Based on the items carried, I visited all the areas. I found another secret message in a bottle in one of the areas!

![Picture](https://i.imgur.com/XWCJFIT.png)

- The task is to unjumble a secret message.
- Assumptions:
    * The capital letters of each secret word is the first letter of it.
    * A sentence will be made once all the words are unjumbled.
- A dictionary file is used to compare with the secret message.
- Three proposed solutions: Brute Force Algorithm, Modified Pattern Matching Algorithm, and Anagram Algorithm.

|Algorithm|Brute Force Algorithm|Modified Pattern Matching Algorithm|Anagram Algorithm|
|---------|---------------------|-----------------------------------|-----------------|
|Introduction to Algorithm|Straightforward method of solving a problem that relies on sheer computing power and trying every possibility rather than advanced techniques to improve efficiency|Compare the length of the jumbled up words with the one inside the dictionary|Algotirhm that compares two strings by arraging both strings alphabetically|
|Advantages|Guaranteed way to finf the correct solution by listing all the possible candidate solutions for the problem|Just like Brute Force, a guaranteed way to find the correct solution|Faster compared to previous algorithms. Reduced time complexity|
|Limitations|Iterates through all permutations|Not widely recognized but closely resembles a pattern matching algorithm|Requires memory to store the sorted words inside the dictionary|
|Modifications|Add another requirement when comparing the permutations with the words inside the dictionary|Add another requirement when comparing the words with the words inside the dictionary|Add another requirement when comparing the words with the words inside the dictionary|

- The chosen algorithm is the Anagram Algorithm.
- It has a lower time complexity compared to Brute Force.
- It has a higher time complexity compared to Modified Pattern Matching, but the sorting operation is generally more efficient than the string manipulations used in Modified Pattern Matching.

### Pseudocode
1. Load a dictionary of valid words.
2. Accept the jumbled word as input.
3. Arrange the word alphabetically.
4. Arrange the words inside the dictionary alphabetically.
5. Compare the arranged word and the arranged words in the dictionary.
6. If there’s a match, add it to the list of solutions.
7. Repeat step 3-6 for all the other words.
8. Display the sentence.

### Running Time Complexity
- The running time complexity is O(w * m * (k log k)), where w is the number of words in the list, m is the number of words in the dictionary, and k is the length of the longest word.
- Compared to Brute Force Algorithm, this algorithm has a shorter running time complexity, lower memory usage, and a more efficient search process.
- Best Case: Time complexity is O(1) when the input word is an anagram of a word in the dictionary and it is encountered early in the search process.
- Worst Case: Time complexity is O(w * m * k * log k) when the input word is not an anagram of any word in the dictionary.
- Average Case: Time complexity is also approximately O(w * m * k * log k), assuming a random distribution of input words.

### Code
```
'''def load_dictionary(file_path):
    with open(file_path, 'r') as file:
        word_list = [word.strip().lower() for word in file]
    return word_list'''


def anagram(word,dictionary):


    for i in range(len(word)):
        if word[i].isupper():
            front = word[i]


    sorted_word = sorted(word.lower())


    for dict_word in dictionary:
        if len(dict_word) == len(word):
            sorted_dict_word = sorted(dict_word)


            if (sorted_dict_word == sorted_word and dict_word[0]==front.lower()):
                solved_words=dict_word
    return (solved_words)
print("Anagram Algorithm\n")
#dictionary_file = "C:/Users/ACER/Desktop/Python/dictionary.txt"
words = ['haTt','enPros', 'asH', 'eMvito']
answer = []


# dictionary = load_dictionary(dictionary_file)
dictionary = ["mom","dad","family","that","game","life","person","cat","dog","bird","has","ash","people","hat","motive","working","work"]
for i in range(len(words)):
    answer.append(anagram(words[i],dictionary))


print(answer)
```

## Part 8: Murder Suspect

### Discussion
So from the last message, I know the murderer must have a strong motive. Is it money? Or something else? I list each family member's characteristics, relationship with Mr Marshall and net worth below

|Name|Relationship|Character|Net Worth($)|
|----|------------|---------|------------|
|Jones Marshall|Son|Always rude to people especially his father|1 Mil|
|Jenna Marshall|Daughter|The quiet one in the family|700K|
|Peter Marshall|Brother|Animal lover|50K|
|Penelope Marshall|Sister|Playful despite of her old age|500K|
|Will Marshall|Uncle|Retired army officer|10K|

- Problem: Who has the most significant motive to be the suspect in this murder?
- Solution suggestion: Use a scoring approach to determine the suspects in the murder case.
- The scoring quantitatively assesses various factors related to each family member, including their relationship, characteristics, and net worth.
- The algorithm assigns weights to specific attributes and characteristics to capture their potential significance in relation to the motive for murder.
- Assumptions:
    * Certain attributes, such as being a son or daughter or having specific characteristics, can contribute to a higher motive for murder.
    * The net worth of each family member can potentially influence their motive for murder.

| |Greedy Algorithm|Dynamic Programming|Brute Force Algorithm|
|-|----------------|-------------------|---------------------|
|Introduction to algorithm|Greedy algorithm that makes the locally optimal choice at each step in the hope of finding a globally optimal solution|Dynamic programming is an algorithm that solves a problem by first solving smaller versions of the problem and then using the solutions to the smaller problems to solve the larger problem|Trying all possible solutions.Tries every possible values until it finds a combination that solves the problem|
|Advantages|Simple to understand|Can be used to solve problems that are too complex for the greedy algorithm|A guarantee to find the optimal solution, if one exist|
|Limitations|Not always guaranteed to find the optimal solution|Can be difficult to implement and inefficient for problems with large numbers of subproblems|Tries all possible solutions to the problem, which can be very time-consuming for problem with large numbers of possible solutions|

- The chosen algorithm is the Greedy Algorithm, which is the simplest and most efficient algorithm.
- The Greedy Algorithm is a good compromise between speed and accuracy.
- The original Greedy Algorithm focuses on making locally optimal choices at each step to achieve the overall best solution.
- In the modified code, a dictionary is introduced to store each family member's information, allowing multiple properties to be associated with each family member.

### Pseudocode
1. Initialize a set of suspects to be empty.
2. For each family member:
    1. Calculate the motive score for the family member.
    2. If the motive score is greater than the current maximum motive score:
        1. Set the current maximum motive score to the motive score.
        2. Add the family member to the suspects set.
3. Sort the set of suspects by their motive scores, in descending order.
4. Return the top k suspects from the set of suspects, where k is the number of suspects that we want to return.

### Running Time Complexity
- Best Case: Time complexity is O(1) when the number of family members is very small.
- Average Case: Time complexity is O(n log n) when the number of family members is moderate.
- Worst Case: Time complexity is also O(n log n) when the number of family members is large.

### Code
```
def greedy_suspect(family_members, max_suspects):
    # Calculate the motive score for each family member.
    for member in family_members:
        motive_score = calculate_motive_score(member)
        member["motive_score"] = motive_score

    # Sort the family members by their motive score, in descending order.
    family_members.sort(key=lambda x: x["motive_score"], reverse=True)

    # Extract the names of the top max_suspects family members.
    suspects = [member["name"] for member in family_members[:max_suspects]]

    # Return the list of suspect names.
    return suspects

def calculate_motive_score(member):
    motive_score = 0

    # Assign motive score based on relationship
    if "Son" in member["relationship"] or "Daughter" in member["relationship"]:
        motive_score += 3
    elif "Brother" in member["relationship"] or "Sister" in member["relationship"]:
        motive_score += 2
    elif "Uncle" in member["relationship"]:
        motive_score += 1

    # Assign motive score based on characteristics
    if "rude" in member["character"]:
        motive_score += 3
    elif "quiet" in member["character"]:
        motive_score += 2
    elif "lover" in member["character"] or "playful" in member["character"] or "retired" in member["character"]:
        motive_score += 1

    # Assign motive score based on net worth
    if member["net_worth"] < 100000:
        motive_score += 1
    elif member["net_worth"] > 99999:
        motive_score -= 1

    return motive_score

def main():
    # Get the number of family members from the user.
    num_members = int(input("Enter the number of family members: "))

    # Create a list to store the family members' information.
    family_members = []

    # Prompt the user for each family member's information.
    for i in range(num_members):
        name = input("Enter the name of family member {}: ".format(i+1))
        relationship = input("Enter the relationship of {}: ".format(name))
        character = input("Enter the character of {}: ".format(name))
        net_worth = float(input("Enter the net worth of {} ($): ".format(name)))

        # Create a dictionary to store the family member's information.
        member = {
            "name": name,
            "relationship": relationship,
            "character": character,
            "net_worth": net_worth
        }
        # Add the member to the list.
        family_members.append(member)

    # Find the most likely suspect using the greedy algorithm.
    suspects = greedy_suspect(family_members, 1)

    # Print the result.
    print("The most likely suspects are:")
    for suspect in suspects:
        print(suspect)

if __name__ == "__main__":
    main()
```