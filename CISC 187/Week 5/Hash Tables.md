# Implementing a Hash Table with Separate Chaining

## Part 1-5
```cpp
#include <iostream>
#include <vector>
#include <list>
#include <string>
using namespace std;

class HashTable {
private:
    vector<list<pair<string, int>>> table;
    int currentSize;
    int capacity;
    int collisionCount;

    int hashFunction(const string& key) const {
        const int prime = 31;
        long long hash = 0;

        for (char c : key) {
            hash = hash * prime + c;
        }

        return (hash % capacity + capacity) % capacity;
    }

    void rehash() {
        vector<list<pair<string, int>>> oldTable = table;

        capacity *= 2;
        table.clear();
        table.resize(capacity);

        currentSize = 0;
        collisionCount = 0;

        for (const auto& bucket : oldTable) {
            for (const auto& entry : bucket) {
                insert(entry.first, entry.second);
            }
        }
    }

public:
    HashTable(int size = 11) {
        capacity = size;
        currentSize = 0;
        collisionCount = 0;
        table.resize(capacity);
    }

    void insert(const string& key, int value) {
        int index = hashFunction(key);

        // If key already exists, update value
        for (auto& entry : table[index]) {
            if (entry.first == key) {
                entry.second = value;
                return;
            }
        }

        // Count collision only if inserting new key into non-empty bucket
        if (!table[index].empty()) {
            collisionCount++;
        }

        table[index].push_back({key, value});
        currentSize++;

        if (loadFactor() > 0.75) {
            rehash();
        }
    }

    bool remove(const string& key) {
        int index = hashFunction(key);

        for (auto it = table[index].begin(); it != table[index].end(); ++it) {
            if (it->first == key) {
                table[index].erase(it);
                currentSize--;
                return true;
            }
        }

        return false;
    }

    int search(const string& key) const {
        int index = hashFunction(key);

        for (const auto& entry : table[index]) {
            if (entry.first == key) {
                return entry.second;
            }
        }

        return -1; // key not found
    }

    double loadFactor() const {
        return static_cast<double>(currentSize) / capacity;
    }

    int size() const {
        return currentSize;
    }

    bool isEmpty() const {
        return currentSize == 0;
    }

    void printTable() const {
        for (int i = 0; i < capacity; i++) {
            cout << "Bucket " << i << ": ";
            for (const auto& entry : table[i]) {
                cout << "(" << entry.first << ", " << entry.second << ") ";
            }
            cout << endl;
        }
    }

    int getCollisionCount() const {
        return collisionCount;
    }

    int getCapacity() const {
        return capacity;
    }

    int maxBucketSize() const {
        int maxSize = 0;

        for (const auto& bucket : table) {
            if ((int)bucket.size() > maxSize) {
                maxSize = bucket.size();
            }
        }

        return maxSize;
    }

    double averageBucketLength() const {
        int totalElements = 0;

        for (const auto& bucket : table) {
            totalElements += bucket.size();
        }

        return static_cast<double>(totalElements) / capacity;
    }
};

int main() {
    HashTable ht;

    // Part 5: Insert at least 100 keys
    for (int i = 1; i <= 100; i++) {
        ht.insert("student" + to_string(i), i);
    }

    cout << "===== HASH TABLE TEST =====" << endl;
    cout << "Table capacity: " << ht.getCapacity() << endl;
    cout << "Number of elements: " << ht.size() << endl;
    cout << "Load factor: " << ht.loadFactor() << endl;
    cout << "Total collisions: " << ht.getCollisionCount() << endl;
    cout << "Maximum bucket size: " << ht.maxBucketSize() << endl;
    cout << "Average bucket length: " << ht.averageBucketLength() << endl;

    cout << endl;
    cout << "Search existing key student25: " << ht.search("student25") << endl;
    cout << "Search non-existing key student999: " << ht.search("student999") << endl;

    cout << endl;
    cout << "Removing student25..." << endl;
    cout << (ht.remove("student25") ? "Removed successfully" : "Key not found") << endl;

    cout << "Removing student50..." << endl;
    cout << (ht.remove("student50") ? "Removed successfully" : "Key not found") << endl;

    cout << endl;
    cout << "Search student25 after removal: " << ht.search("student25") << endl;
    cout << "Number of elements after removals: " << ht.size() << endl;

    return 0;
}
```

## Part 6
I tested the hash table using three different input types: random strings, sequential keys, and keys with the same prefix. For each test, I recorded the total number of collisions, the maximum bucket size, and the average bucket length. These values helped show how evenly the hash function distributed the keys across the table.   
In general, the random strings produced the most even distribution because the keys were less similar to each other. The sequential keys also distributed reasonably well, but they sometimes created slightly more clustering. The same-prefix keys tended to be the most likely to group into similar buckets because many of the strings began with the same characters. This shows that input patterns can affect hash table performance, even when the hash function is designed to spread values across the table.

Video: https://youtu.be/Y2FT7qVROmU
