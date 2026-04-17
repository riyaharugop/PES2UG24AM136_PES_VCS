PES-VCS Lab Submission

Name: Riya Harugop
SRN: PES2UG24AM136

Additional Files
.env
This file contains the PES_AUTHOR environment variable required for commit identification:

PES_AUTHOR="Riya Harugop <PES2UG24AM136>"

Purpose:
The PES-VCS system reads the author information from this variable while creating commits.

Usage:
Run the following before executing any pes commands:
source .env


Phase 1: Object Storage Foundation
Implementation Summary
In this phase, I implemented a content-addressable object storage system using SHA-256 hashing. The system ensures:

Efficient storage using hashing
Deduplication of identical files
Data integrity verification



Phase 2: Tree Objects
Implementation Summary
Implemented tree structures to represent directory hierarchy. This includes:

Recursive directory handling
Tree serialization and deserialization
Linking files and subdirectories using hashes


Phase 3: Index (Staging Area)
Implementation Summary
Implemented the staging area using a text-based index file:

Tracks staged files
Stores metadata (hash, size, timestamps)
Uses atomic updates for safety


Phase 4: Commits and History
Implementation Summary
Implemented commit functionality:

Snapshot creation using tree objects
Parent linking for history tracking
Author and timestamp management


🧠 Analysis Questions
Q5.1: Checkout Implementation

To implement pes checkout <branch>:

Update .pes/HEAD to point to the selected branch
Read commit hash from .pes/refs/heads/<branch>
Load the corresponding tree

Working directory changes:

Replace files with snapshot from selected commit
Remove files not present in target tree

Challenges:

Handling uncommitted changes
Avoiding accidental data loss
Managing directory structures properly
Q5.2: Dirty Working Directory Detection

To detect conflicts:
Compare working directory files with index
Compare index with last committed version

If:
File is modified AND differs from target branch → conflict

Then:
Abort checkout to prevent data loss


Q5.3: Detached HEAD

Detached HEAD occurs when:
HEAD points directly to a commit instead of a branch

Effects:
New commits are not attached to any branch
They can be lost if not saved

Recovery:
Create a new branch pointing to that commit
Q6.1: Garbage Collection

Steps:

Start from all branch references
Traverse commits, trees, and blobs
Mark all reachable objects
Delete unreachable ones

Data structure used: Hash set



Q6.2: GC Race Condition

Problem:
Garbage collector may delete objects being used by a commit

Solution:

Use locking mechanisms
Delay deletion (grace period)
Ensure safe object handling
Commit History

This repository contains multiple commits across all phases showing progressive development of the project.
https://github.com/riyaharugop/PES2UG24AM136_PES_VCS/tree/main


Before running commands:
source .env


Declaration

I declare that this submission is my own work.

Signature: Riya Harugop
Date: 17.04.2026
