# PES2UG24AM136_PES_VCS
🚀 PES-VCS — My Implementation of a Version Control System

NAME: Riya Harugop
SRN: PES2UG24AM136
CLASS: CS-AIML (B)

📌 Objective

In this lab, I implemented a simplified Version Control System (PES-VCS) inspired by Git. The system is capable of tracking file changes, storing snapshots efficiently, and maintaining commit history using core Operating System concepts.

This project helped me understand:
   Content-addressable storage
   File system structures
   Hashing and data integrity
   Process of version control systems like Git

⚙️ Platform Used
   Ubuntu (Linux environment)
   GCC Compiler
   OpenSSL (for SHA hashing)

🛠️ Setup & Execution
   Installation
      sudo apt update
      sudo apt install build-essential libssl-dev

   Build
      make

   Run Test Programs
      ./test_objects
      ./test_tree

🧩 Implementation Overview

🔹 Phase 1: Object Storage

   I implemented:
      object_write()
      object_read()

   Key concepts:
      Data stored using SHA-256 hash
      Objects stored in .pes/objects/
      Deduplication achieved using hashing
      Integrity verified by recomputing hash


🔹 Phase 2: Tree Structure

   I implemented:
      tree_from_index()

   Key concepts:

      Directory hierarchy stored as tree objects
      Recursive structure for nested directories
      Each tree stores file metadata and object references


🔹 Phase 3: Index (Staging Area)

   I implemented:
      index_load()
      index_save()
      index_add()

   Key concepts:
      Tracks staged files
      Stores metadata like file size, hash, and timestamp
      Uses atomic file writing


🔹 Phase 4: Commit System

   I implemented:
      commit_create()

   Key concepts:
      Commits store snapshot of project
      Linked list of commits using parent pointer
      Uses tree structure from index
      Author info taken from environment variable


📊 Results
   Successfully created object storage system
   Verified tree construction and parsing
   Implemented staging and commit workflow
   Generated commit history using pes log


🧠 Analysis Questions 

🔹 Q5.1 — Checkout Implementation

      To implement pes checkout <branch>:

      Changes required:
         Update .pes/HEAD to point to new branch
         Read commit hash from .pes/refs/heads/<branch>
         Load corresponding tree

      Working directory update:
         Replace files with snapshot from target commit

      Complexity:
         Handling uncommitted changes
         Avoid overwriting user data
         Maintaining consistency between index and working directory


🔹 Q5.2 — Dirty Working Directory Detection

      To detect conflicts:

      Compare:
         Working directory file
         Index entry
         Last committed version
      If:
         File modified AND differs from target branch → conflict
      Then:
         Abort checkout

      This ensures no data loss.


🔹 Q5.3 — Detached HEAD

      Detached HEAD means:
         HEAD directly points to a commit (not a branch)

      If commits are made:
         They are not part of any branch
         Can be lost if not referenced
      Recovery:
         Create a branch pointing to that commit


🔹 Q6.1 — Garbage Collection

      Algorithm:
         Start from all branch references
         Traverse commits recursively
         Mark all reachable objects

      Use:
         Hash set for tracking visited objects

      Delete:
         Any object not in reachable set

      Estimate:
         ~100k commits → traverse all commits + trees + blobs


🔹 Q6.2 — GC Race Condition

      Problem:
         GC may delete objects while commit is being created

      Example:
         Commit references object
         GC deletes it before commit finishes

      Solution:
         Locking mechanism
         Temporary protection of new objects
         Git uses safe GC strategies



📂 Conclusion

This project gave me practical understanding of:

      How Git works internally
      File system design
      Data integrity using hashing
      Efficient storage techniques

