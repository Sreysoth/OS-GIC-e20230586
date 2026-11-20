# Class Activity 4 — Shared File API

- **Student Name:** Sreysoth Samreth
- **Student ID:** e20230586
- **Partner Name:** N/A (Completed Solo using 3 Terminal Windows)
- **Partner Student ID:** N/A
- **Server Machine Owner:** Sreysoth Samreth
- **Server IP Address:** 192.168.71.173

---

## Task 1: C++ Before Mutex

![C++ before mutex](screenshots/cpp_before_mutex.png)

- Expected score after 20 total client requests: 20
- Actual score: [REPLACE WITH YOUR OBSERVED SCORE, e.g., 3]
- What happened: Multiple detached threads read `shared_score.txt` simultaneously before any thread finished sleeping and writing back, causing lost updates (race condition) where threads overwrote each other's increments.

---

## Task 2: C++ After Mutex

![C++ after mutex](screenshots/cpp_after_mutex.png)

- Expected score after 20 total client requests: 20
- Actual score: 20
- What changed after adding mutex: `std::lock_guard<std::mutex>` forced each thread to wait until the active thread finished reading, incrementing, and writing to `shared_score.txt`, ensuring every request incremented the score sequentially to 20.

---

## Task 3: Java Before Synchronized

![Java before synchronized](screenshots/java_before_synchronized.png)

- Expected score after 20 total client requests: 20
- Actual score: [REPLACE WITH YOUR OBSERVED SCORE, e.g., 4]
- What happened: Without synchronization, multiple client handler threads read the same initial score from `shared_score.txt` concurrently during the 200ms sleep window and overwrote each other's writes, resulting in a final score below 20.

---

## Task 4: Java After Synchronized

![Java after synchronized](screenshots/java_after_synchronized.png)

- Expected score after 20 total client requests: 20
- Actual score: 20
- What changed after adding synchronized: Adding the `synchronized` keyword to `updateScore()` locked the method on the class monitor so only one thread could read and write `shared_score.txt` at a time, producing an exact final score of 20.

---

## Questions

1. **Why should clients send requests to the server instead of writing the file directly?**
   Centralizing file access in a single server API prevents arbitrary external processes from corrupting or overwriting the file concurrently, enforces validation and access control, and allows a single coordinator to manage synchronization in one place.

2. **Why does the server still have a race condition before mutex or `synchronized`?**
   Because the server spawns a separate thread for each incoming client connection (`std::thread` in C++ and `new Thread` in Java). Without mutual exclusion, multiple server threads enter the critical section (`update_score` / `updateScore`) at the same time, read stale values before the 200ms delay completes, and overwrite each other's updates.

3. **In the C++ fixed version, what does `std::lock_guard<std::mutex>` protect?**
   It protects the critical section inside `update_score()`—specifically reading from `shared_score.txt`, sleeping/incrementing the score variable, writing the updated score back to `shared_score.txt`, and printing the log message—using RAII so the mutex automatically unlocks when the function returns.

4. **In the Java fixed version, what does `synchronized` protect?**
   Because `updateScore` is a `static synchronized` method, it acquires the intrinsic monitor lock on the `ScoreServerSync.class` object, ensuring only one thread at a time can execute the file read, 200ms delay, increment, and file write sequence.

5. **Why is the final score expected to be 20 when Student A sends 10 requests and Student B sends 10 requests?**
   `shared_score.txt` starts at `0`, and each of the 20 total client requests triggers a `score++` operation (10 from Student A + 10 from Student B = 20 increments), so $0 + 20 = 20$ when no updates are lost.

6. **What could happen if two separate servers update the same file at the same time?**
   In-memory thread locks (`std::mutex` or Java `synchronized`) only coordinate threads within a single process. Two separate server processes would bypass each other's thread locks and create a race condition again unless they used OS-level file locking (`flock`/`fcntl`) or a shared database.

---

## Reflection

Both C++ and Java solve the race condition by enforcing mutual exclusion around the critical section, though their syntax and lock management differ. C++ uses an explicit `std::mutex` object paired with `std::lock_guard<std::mutex>`, which follows RAII to guarantee the lock is released when leaving scope. Java simplifies this at the language level by letting us add the `synchronized` keyword directly to the method signature, automatically acquiring and releasing the class monitor lock. This activity demonstrated that moving shared file access behind a server API is not enough on its own—whenever a server handles requests concurrently across threads, shared resources must still be protected with synchronization primitives.
