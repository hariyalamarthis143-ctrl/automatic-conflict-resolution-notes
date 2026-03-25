# Automatic Conflict Resolution System for Notes

## 📖 Overview
This project aims to automatically detect and resolve conflicts in note-taking applications when multiple edits occur across different devices. It ensures data consistency, prevents loss of information, and improves user experience.

---

##  Features
-  Conflict Detection (local vs remote versions)
-  Automatic Merge for non-overlapping changes
-  Assisted Conflict Resolution (UI-based)
-  No data loss guarantee
-  Seamless synchronization across devices

---

##  System Workflow
![Diagram](https://chatgpt.com/backend-api/estuary/content?id=file_000000009c2c71fab2331f6994f1fbc6&ts=492897&p=fs&cid=1&sig=d55c112166f764f795172827210b806c04ebdbc807c1a55df966672e2a38a80a&v=0)

---

## 🧠 Algorithm Approach

### 1. Conflict Detection
- Compare local and remote versions
- Identify insertions, deletions, modifications

### 2. Merge Strategy
- Non-overlapping changes → auto merge
- Overlapping changes → mark conflict

### 3. Assisted Resolution
- Show:
  - Local version
  - Remote version
  - Original version
- Provide suggestions to user

---

## 💻 Sample Implementation

```ts
function mergeNotes(local: string, remote: string): string {
    if (local === remote) return local;

    let merged = "";
    const localLines = local.split("\n");
    const remoteLines = remote.split("\n");

    for (let i = 0; i < Math.max(localLines.length, remoteLines.length); i++) {
        if (localLines[i] === remoteLines[i]) {
            merged += (localLines[i] || "") + "\n";
        } else {
            merged += `<<<<<<< LOCAL\n${localLines[i] || ""}\n=======\n${remoteLines[i] || ""}\n>>>>>>> REMOTE\n`;
        }
    }

    return merged;
}
```