# Class Activity 2 — Processes & Inter-Process Communication

- **Student Name:** Sreysoth Samreth
- **Student ID:** e20230586
- **Date:** Nov 9, 2026

---

## Task 1: Process Creation on Linux (fork + exec)

### Compilation & Execution
![Task 1 - Compile & Run](screenshots/task1_compile_run.png)

### Process Tree
![Task 1 - Process Tree](screenshots/task1_process_tree.png)

### Output
```
[Open your result_forkchild.txt file, copy the text, and paste it right here]
```

### Questions

1. **What does `fork()` return to the parent? What does it return to the child?**
   > [Type your answer here]

2. **What happens if you remove the `waitpid()` call? Why might the output look different?**
   > [Type your answer here]

3. **What does `execlp()` do? Why don't we see "execlp failed" when it succeeds?**
   > [Type your answer here]

4. **Draw the process tree for your program (parent → child). Include PIDs from your output.**
   > [Type your answer here]

5. **Which command did you use to view the process tree (`ps --forest`, `pstree`, or `htop`)? What information does each column show?**
   > [Type your answer here]

---

## Task 2: Process Creation on Windows

### Compilation & Execution
![Task 2 - Compile & Run](screenshots/task2_compile_run.png)

### Task Manager Screenshots
![Task 2 - Task Manager Tree](screenshots/task2_taskmanager_tree.png)
![Task 2 - Task Manager Details](screenshots/task2_taskmanager_details.png)

### Questions

1. **What is the key difference between how Linux creates a process (`fork` + `exec`) and how Windows does it (`CreateProcess`)?**
   > [Type your answer here]

2. **What does `WaitForSingleObject()` do? What is its Linux equivalent?**
   > [Type your answer here]

3. **Why do we need to call `CloseHandle()` at the end? What happens if we don't?**
   > [Type your answer here]

4. **In Task Manager, what was the PID of your parent program and the PID of mspaint? Do they match your program's output?**
   > [Type your answer here]

5. **Compare the Processes tab (tree view) and the Details tab (PID/PPID columns). Which view makes it easier to understand the parent-child relationship? Why?**
   > [Type your answer here]

---

## Task 3: Shared Memory IPC

### Compilation & Execution
![Task 3 - Compile & Run](screenshots/task3_compile_run.png)

### Output
```
[Open your result-shm-ipc.txt file, copy the text, and paste it right here]
```

### Questions

1. **What does `shm_open()` do? How is it different from `open()`?**
   > [Type your answer here]

2. **What does `mmap()` do? Why is shared memory faster than other IPC methods?**
   > [Type your answer here]

3. **Why must the shared memory name match between producer and consumer?**
   > [Type your answer here]

4. **What does `shm_unlink()` do? What would happen if the consumer didn't call it?**
   > [Type your answer here]

5. **If the consumer runs before the producer, what happens? Try it and describe the error.**
   > [Type your answer here]

---

## Task 4: Message Queue IPC

### Compilation & Execution
![Task 4 - Compile & Run](screenshots/task4_compile_run.png)

### Output
```
[Open your result-mq-ipc.txt file, copy the text, and paste it right here]
```

### Questions

1. **How is a message queue different from shared memory? When would you use one over the other?**
   > [Type your answer here]

2. **Why does the queue name in `common.h` need to start with `/`?**
   > [Type your answer here]

3. **What does `mq_unlink()` do? What happens if neither the sender nor receiver calls it?**
   > [Type your answer here]

4. **What happens if you run the receiver before the sender?**
   > [Type your answer here]

5. **Can multiple senders send to the same queue? Can multiple receivers read from the same queue?**
   > [Type your answer here]

---

## Reflection
> [Write a quick reflection on what you learned about Linux vs Windows and which IPC method you preferred.]

