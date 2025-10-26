ACID Transactions

Imagine you’re running an e-commerce application.
A customer places an order, and your system needs to deduct the item from inventory, charge the customer’s credit card, and record the sale in your accounting system—all at once.

What happens if the payment fails but your inventory count has already been reduced? Or if your application crashes halfway through the process?
This is where ACID transactions come into play. They ensure that all the steps in such critical operations happen reliably and consistently.

ACID is an acronym that refers to the set of 4 key properties that define a transaction: Atomicity, Consistency, Isolation, and Durability.

1.Atomicity:
Atomicity means a transaction is all-or-nothing either all its operations succeed, or none are applied. If any part fails, the entire transaction is rolled back to keep the database consistent.

Commit: If the transaction is successful, the changes are permanently applied.
Abort/Rollback: If the transaction fails, any changes made during the transaction are discarded.
Example: Consider the following transaction T consisting of T1 and T2 : Transfer of $100 from account X to account Y .
![Data](https://github.com/anjali22-lgtm/System-Design/blob/8b9ea6c4649f3c04ab777576a872cef8f2c00ff2/ato.png)


2.Consistency:
Consistency in transactions means that the database must remain in a valid state before and after a transaction.

A valid state follows all defined rules, constraints, and relationships (like primary keys, foreign keys, etc.).
If a transaction violates any of these rules, it is rolled back to prevent corrupt or invalid data.
If a transaction deducts money from one account but doesn't add it to another (in a transfer), it violates consistency.
Example: Suppose the sum of all balances in a bank system should always be constant. Before a transfer, the total balance is $700. After the transaction, the total balance should remain $700. If the transaction fails in the middle (like updating one account but not the other), the system should maintain its consistency by rolling back the transaction.

Total before T occurs = 500 + 200 = 700 .
Total after T occurs = 400 + 300 = 700 .
![Data](https://github.com/anjali22-lgtm/System-Design/blob/8b9ea6c4649f3c04ab777576a872cef8f2c00ff2/con.png)


3.Isolation:
Isolation ensures that transactions run independently without affecting each other. Changes made by one transaction are not visible to others until they are committed.
It ensures that the result of concurrent transactions is the same as if they were run one after another, preventing issues like:

Dirty reads: reading uncommitted data
Non-repeatable reads: data changes between two reads
Phantom reads: new rows appear during a transaction
Example: Consider two transactions T and T''.

X = 500, Y = 500
![Data](https://github.com/anjali22-lgtm/System-Design/blob/8b9ea6c4649f3c04ab777576a872cef8f2c00ff2/iso.png)

Isolation ensures that transactions run independently without affecting each other. Changes made by one transaction are not visible to others until they are committed.
It ensures that the result of concurrent transactions is the same as if they were run one after another, preventing issues like:

Dirty reads: reading uncommitted data
Non-repeatable reads: data changes between two reads
Phantom reads: new rows appear during a transaction
Example: Consider two transactions T and T''.

X = 500, Y = 500


4.Durability:
Durability ensures that once a transaction is committed, its changes are permanently saved, even if the system fails. 
The data is stored in non-volatile memory, so the database can recover to its last committed state without losing data.

Example: After successfully transferring money from Account A to Account B, the changes are stored on disk.
Even if there is a crash immediately after the commit, the transfer details will still be intact when the system recovers, ensuring durability.


SQL Vs NOSQL

1.SQL:
SQL databases use a relational data model where data is stored in tables (often referred to as relations).
Each table has rows (tuples) representing individual records, and columns representing attributes of those records.
The primary key uniquely identifies each record, while foreign keys link tables together, allowing for relational queries.

2.NOSQL:
NoSQL databases use flexible, non-relational data models, allowing for various ways of storing and managing data.
a) Key-Value Model (e.g., Redis)
The key-value model is the simplest NoSQL model, where data is stored as key-value pairs. This model works well for applications that need fast lookups by a unique key.

b) Document Model (e.g., MongoDB)
In the document model, data is stored as documents in formats such as JSON or BSON.
Each document contains a unique identifier (key) and a set of key-value pairs (attributes). Documents can have varying structures, making the document model schema-less or flexible.

c) Column-Family Model (e.g., Cassandra)
In the column-family model, data is organized into rows and columns, but unlike the relational model, each row can have a variable number of columns.
It is optimized for fast querying and large-scale distributed storage.

d) Graph Model (e.g., Neo4j)
In the graph model, data is stored as nodes, edges, and properties. This model is ideal for applications where data relationships are complex and highly interconnected (e.g., social networks).
In our user management system, users can be represented as nodes, and relationships between them (e.g., friendships or orders) can be represented as edges.
Graph Representation:

Nodes: Users, Orders
Edges: PLACED_ORDER
(John) --PLACED_ORDER--> (Laptop)
(Mike) --PLACED_ORDER--> (Smartphone)
(Ron) --PLACED_ORDER--> (Headphones)

![Data](https://github.com/anjali22-lgtm/System-Design/blob/8b9ea6c4649f3c04ab777576a872cef8f2c00ff2/SQL.png)


BLOOM FILTERS

Have you ever wondered how Netflix knows which shows you've already watched? Or how Amazon avoids showing you products you've already purchased?
Using a traditional data structure like a hash table for these checks could consume significant amount of memory, especially with millions of users and items.

Instead, many systems rely on a more efficient data structure—a Bloom Filter.

What is bloom filters?
Bloom filter is a space-efficent probabilistic data structure that tells whether an elementmay be in set or definitely is not. If we look up an item in the bloom filter, we can get two possible results.
-the item is not present in the set: true negative.
-the item might be present in the set. can be either a False positive or true positive.

How Does a Bloom Filter Work?
A Bloom filter works by using multiple hash functions to map each element in the set to a bit array.
![Data](https://github.com/anjali22-lgtm/System-Design/blob/8b9ea6c4649f3c04ab777576a872cef8f2c00ff2/bloom.png)

1. Initialization:
A Bloom filter starts with an empty bit array of size m (all bits are initially set to 0).
It also requires k independent hash functions, each of which maps an element to one of the m positions in the bit array.

3. Inserting an Element:
To insert an element into the Bloom filter, you pass it through each of the k hash functions to get k positions in the bit array.
The bits at these positions are set to 1.

5. Checking for Membership:
To check if an element is in the set, you again pass it through the k hash functions to get k positions.
If all the bits at these positions are set to 1, the element is considered to be in the set (though there's a chance it might be a false positive).
If any bit at these positions is 0, the element is definitely not in the set.


Example: Using a Bloom Filter for URL Checking
Imagine you're building a web crawler that needs to keep track of which URLs it has already visited.

Instead of storing every URL (which would require a lot of memory), you decide to use a Bloom Filter.

Step 1: Set Up the Bloom Filter
Set Up the Bloom Filter
Initialize a Bit Array: Let’s assume our Bloom Filter uses a bit array of size 10, initially all set to 0.
Choose Hash Functions: We’ll use two hash functions in this example. These hash functions take an input (like a URL) and output an index in the bit array.
Step 2: Adding a URL to the Bloom Filter
Suppose we want to add the URL example.com to our Bloom Filter.

Hash Function 1 generates an index of 3 for example.com.
Hash Function 2 generates an index of 7 for example.com.
Adding a URL to the Bloom Filter
We set the bits at indices 3 and 7 in the bit array to 1.

Step 3: Adding Another URL
Now, let's add another URL, algomaster.io.

Hash Function 1 generates an index of 1 for algomaster.io.
Hash Function 2 generates an index of 4 for algomaster.io.
Adding Another URL
We set the bits at indices 1 and 4 in the bit array to 1.

Step 4: Checking for a URL in the Bloom Filter
Suppose we want to check if example.com is already in the Bloom Filter.

Hash Function 1 generates index 3 for example.com.
Hash Function 2 generates index 7 for example.com.
Checking for a URL in the Bloom Filter
Since both bits at indices 3 and 7 are set to 1, we can say that example.com is probably in the set (there's a small chance of a false positive).

Step 5: Checking for a Non-Existent URL
Now, let's check if nonexistent.com is in the Bloom Filter.

Hash Function 1 generates index 2 for nonexistent.com.
Hash Function 2 generates index 5 for nonexistent.com.
Checking for a Non-Existent URL
Since the bits at indices 2 and 5 are both 0, we can confidently say that nonexistent.com is not in the set.

Limitations of Bloom Filters
1. False Positives
Bloom Filters can produce false positives, meaning they may incorrectly indicate that an element is present in the set when it is not.
Example: Consider a scenario where a non-existent key is checked against a Bloom Filter. If all the hash functions map to bits that are already set to 1, the filter falsely signals the presence of the key.

Such false positives can lead to unnecessary processing or incorrect assumptions about data.
For instance, in a database system, this might trigger unnecessary cache lookups or wasted attempts to fetch data that doesn’t actually exist.
The likelihood of false positives can be reduced by choosing an optimal size for the bit array and an appropriate number of hash functions, but they can never be completely eliminated.

2. No Support for Deletions
Standard Bloom Filters do not support element deletions. Once a bit is set to 1 by adding an element, it cannot be unset because other elements may also rely on that bit.
This limitation makes Bloom Filters unsuitable for dynamic sets where elements are frequently added and removed.
Variants like the Counting Bloom Filter can allow deletions by using counters instead of bits, but this requires more memory.

3. Limited to Set Membership Queries
Bloom Filters are specifically designed to answer set membership queries. They do not provide information about the actual elements in the set, nor do they support complex queries or operations beyond basic membership checks.
Example: If you need to know the details of an element (e.g., full information about a user ID), you would need another data structure in addition to the Bloom Filter.

4. Not Suitable for Exact Set Membership
Bloom Filters are probabilistic, meaning they cannot provide a definite “yes” answer (only a “probably yes” or “definitely no”).
For applications requiring exact membership information, Bloom Filters are not suitable. Other data structures like hash tables or balanced trees should be used instead.

5. Vulnerable to Hash Collisions
Hash collisions are more likely as the number of elements in the Bloom Filter grows. Multiple elements can end up setting or relying on the same bits, increasing false positives.

As hash collisions accumulate, the filter’s effectiveness decreases. With a high load factor, the filter may perform poorly and become unreliable.
The use of additional hash functions can help reduce collisions, but increasing the number of hash functions also increases the complexity and the memory requirements.


