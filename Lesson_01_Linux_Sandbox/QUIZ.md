# 📝 Lesson 01: Linux Sandbox Evaluation Assessment

Evaluate your understanding of the 80:20 Linux core framework. Try to answer without looking back at the cheat sheet guide!

---

### Question 1: The Parent Directory Flag Strategy
You are standing in an empty directory. You need to create a nested structural file path sequence `level1/level2/level3` using a single execution command block. Which command is syntactically correct?

- [ ] A) `mkdir level1/level2/level3`
- [ ] B) `mkdir -p level1/level2/level3`
- [ ] C) `touch level1/level2/level3`
- [ ] D) `cd level1/level2/level3`

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** Standard `mkdir` fails if parent directories do not already exist. Passing the `-p` (parents) flag forces the Linux kernel engine to auto-generate missing nested folders in the path sequence sequentially without throwing system crashes.
</details>

---

### Question 2: Copy (`cp`) vs Move (`mv`) Mechanics
What happens to the original source script layout framework file inside the system file tree structure when you execute a `mv` command versus a `cp` command?

- [ ] A) `mv` duplicates the file; `cp` deletes the original file.
- [ ] B) Both commands duplicate files identically but rename variables.
- [ ] C) `cp` keeps the original file and makes a mirror variant; `mv` cuts/shifts the original asset to the target destination path without duplicating it.
- [ ] D) `mv` only changes execution credentials authorizations; `cp` modifies binary extensions.

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: C**
* **Technical Reason:** `cp` (copy) performs an allocation replication leaving the source file untouched. `mv` (move) simply updates the inode path mapping index structure inside the Linux file system layout, effectively moving/shifting the exact same block element without replication overhead costs.
</details>

---

### Question 3: Runtime Security Clearance Access
You touch a fresh Python automation engine script file `camera_driver.py`. The terminal throws a `Permission Denied` execution access block error. How do you grant proper Linux security access metrics?

- [ ] A) `sudo apt update`
- [ ] B) `cd ..`
- [ ] C) `chmod +x camera_driver.py`
- [ ] D) `rm -rf camera_driver.py`

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: C**
* **Technical Reason:** Freshly created files in Linux have strict read-write safety profiles but block direct runtime execution handles. Running `chmod +x` (change mode add executable) explicitly updates the folder access matrix configuration metadata to permit binary running sequences.
</details>
