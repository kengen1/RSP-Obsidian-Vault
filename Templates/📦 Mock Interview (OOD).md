## **Object-Oriented Design (OOP/OOD) Problem**

- **Title:** `Design a Cache and TokenManager`
- **Link:* [[Object Oriented Design Question]]

### **OOP Principles and Design Patterns to look for:**

| **Principle/Pattern**      | **Description**                                                                                                            |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Encapsulation**          | Keep `state` and TTL logic private within the `Cache` class. Expose only necessary methods (`read`, `update`, etc.).       |
| **Separation of Concerns** | Ensure the `Cache` handles state management and TTL logic, while `TokenManager` handles the management of multiple caches. |
| **Single Responsibility**  | `Cache` focuses on managing a single state's lifecycle, while `TokenManager` manages multiple caches for different APIs.   |
| **Abstraction**            | Use higher-order functions (e.g., `updateFunction`) to allow flexible and reusable refresh logic across use cases.         |
| **Singleton Pattern**      | (Optional) Ensure only one instance of `TokenManager` exists if global cache management is required.                       |
| **Factory Pattern**        | (Optional) Use a factory method in `TokenManager` for dynamic creation of caches based on API types or configurations.     |
| **Open/Closed Principle**  | The system allows extending functionality (e.g., adding new caches or modifying TTLs) without altering core logic.         |
| **Fail-Safe Design**       | Implement error handling for `updateFunction` failures or invalid TTL values to ensure system resilience.                  |
| **Lazy Initialization**    | Initialize the cache state only when `read` is called, avoiding unnecessary updates when idle.                             |

### **Understanding the Problem**

|Confirming Question|✅/❌|
|---|---|
|Clarified requirements||
|Identified key constraints||
|Asked about edge cases||
|Defined the scope clearly||
|_Score:_||

---

### **Design and OOP Principles**

|Design and OOP Criteria|✅/❌|
|---|---|
|Proposed a clean, modular design||
|Adhered to OOP principles (e.g., encapsulation)||
|Clearly defined class responsibilities||
|Considered extensibility for adding/removing caches||
|Used appropriate design patterns (e.g., Singleton, Factory)||
|_Score:_||

---

### **Implementation**

|Implementation Criteria|✅/❌|
|---|---|
|Encapsulated state and logic properly||
|Implemented `Cache` with required methods||
|Implemented `TokenManager` as per requirements||
|Handled edge cases (e.g., expired TTL, invalid input)||
|Code is clean, readable, and maintainable||
|_Score:_||

---

### **Algorithmic Thinking**

|Algorithmic Criteria|✅/❌|
|---|---|
|Efficient TTL handling||
|Clear logic for `isOutdated`, `update`, and `read` methods||
|Considered concurrency or multithreading issues (if applicable)||
|Correct time complexity analysis||
|_Score:_||

---

### **Communication**

|Communication Criteria|✅/❌|
|---|---|
|Explained the design clearly and concisely||
|Explained implementation steps effectively||
|Avoided excessive silence or confusion||
|Responded well to clarifications or follow-up questions||
|_Score:_||

---

### **Testing and Validation**

|Testing Criteria|✅/❌|
|---|---|
|Tested basic functionality of `Cache`||
|Tested basic functionality of `TokenManager`||
|Identified edge cases (e.g., invalid TTL, failed refresh)||
|Thorough and logical testing approach||
|_Score:_||

---

### **Advanced Considerations**

|Advanced Considerations|✅/❌|
|---|---|
|Suggested thread-safe caching||
|Proposed improvements like logging or retries||
|Implemented bonus features (e.g., manual `write` function)||
|Addressed production-level concerns||
|_Score:_||