# Union-Find (Disjoint Set)

## 1. Overview

- the union-find structure manages a collection of disjoint sets and supports two main operations:
- **union** : merge two subsets into a single subset
- **find** : determine the root of the set containing a specific element

**Graph/Data Representation** : Union-Find is conceptually thought of as using an **adjacency matrix**

- in practice, it uses two arrays (parent and rank) to manage relationships

## 2. Structure

```cpp
class UnionFind {
private:
    vector<int> parent;  // Stores the parent of each element
    vector<int> rank;    // Stores the rank (depth) of each set

public:
    // Constructor initializes n elements with each element being its own parent
    UnionFind(int n) {
        parent.resize(n);
        rank.resize(n, 1);
        for (int i = 0; i < n; i++) {
            parent[i] = i;  // Initially, each element is its own root
        }
    }
};
```

## 3. Operations


| Operation | Description                       | Time Complexity                |
| ----------- | ----------------------------------- | -------------------------------- |
| Union     | Merge two sets                    | **O(α(n))**                   |
| Find      | Find the root of an element's set | **O(α(n))** (almost constant) |
| Initialize| Initialize `n` elements in separate sets                    | **O(n)**                   |


### 3.1 Union

#### How It Works:
- The Union operation merges two subsets by linking the root of one to the root of the other.
- To keep the structure balanced, Union by Rank is used:
    - Attach the tree with smaller rank to the tree with larger rank.
    - If both trees have the same rank, attach one as a child of the other and increase its rank by one.

#### Implementation
```cpp
void unionSets(int x, int y) {
    int rootX = find(x);
    int rootY = find(y);

    if (rootX != rootY) {
        // Union by Rank
        if (rank[rootX] > rank[rootY]) {
            parent[rootY] = rootX;
        } else if (rank[rootX] < rank[rootY]) {
            parent[rootX] = rootY;
        } else {
            parent[rootY] = rootX;
            rank[rootX] += 1;
        }
    }
}
```
---

### 3.2 Find

#### How It Works:
- The Find operation locates the root of the set containing a specific element
- It uses Path Compression to optimize future lookups by making all nodes along the path point directly to the root

#### Implementation
```cpp
int find(int x) {
    if (parent[x] != x) {
        parent[x] = find(parent[x]);  // Path compression
    }
    return parent[x];
}
```

### Example Usage
```cpp
int main() {
    UnionFind uf(5);  // Create Union-Find with 5 elements

    uf.unionSets(0, 1);  // Union of sets containing 0 and 1
    uf.unionSets(1, 2);  // Union of sets containing 1 and 2

    int rootOf2 = uf.find(2);  // Find the root of the set containing 2
    cout << "Root of 2 is: " << rootOf2 << endl;

    return 0;
}
```