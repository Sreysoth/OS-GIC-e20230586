# OS Lab 3 — Wildcards, Hard Links and Symbolic Links

- **Student Name:** Sreysoth Samreth
- **Student ID:** e20230586

## Summary of Observations
1. **Wildcards:** Unquoted `*` and `?` are expanded by Bash before running commands (skipping hidden files starting with `.`), while single quotes disable expansion and pass literal characters.
2. **Hard Links vs. Symbolic Links:** A hard link shares the exact same inode number as the original file, so it continues reading the original data (`v1`) even after the original file is renamed. A symbolic link has its own inode and stores only a path string; renaming the target makes the symbolic link dangling (`No such file or directory`), and creating a new file with the old name causes the symbolic link to read the new file (`v2`).
3. **Repair:** Replacing the symbolic link with a relative target pointing to `<name>-<tag>.txt` restores access to the original file and ensures portability if the parent directory is moved.
