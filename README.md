# Git Branch Management Guide

This guide provides step-by-step instructions to **switch branches, check branch status, push specific files to `main` or `extra-learning` branches, and merge changes when necessary**.

---

## 1. **Check Available Branches**
To see all branches in your repository:
```sh
git branch
```
If you want to see remote branches as well:
```sh
git branch -a
```

---

## 2. **Switch Between Branches**
To switch to an existing branch:
```sh
git checkout main   # Switch to the main branch
git checkout extra-learning  # Switch to the extra-learning branch
```
If the branch does not exist, create and switch:
```sh
git checkout -b new-branch-name
```

---

## 3. **Add and Push Some Files to `main` Branch**
### **Steps:**
1. Switch to the `main` branch:
   ```sh
   git checkout main
   ```
2. Add specific files to be committed to `main`:
   ```sh
   git add important_file.txt
   ```
3. Commit the changes:
   ```sh
   git commit -m "Added important_file.txt to main"
   ```
4. Push the changes to the remote `main` branch:
   ```sh
   git push origin main
   ```

---

## 4. **Add and Push Some Files to `extra-learning` Branch**
### **Steps:**
1. Switch to the `extra-learning` branch:
   ```sh
   git checkout extra-learning
   ```
2. Add files to be committed to `extra-learning`:
   ```sh
   git add extra_notes.md extra_resources/
   ```
3. Commit the changes:
   ```sh
   git commit -m "Added extra notes and resources to extra-learning"
   ```
4. Push the changes to the `extra-learning` branch:
   ```sh
   git push origin extra-learning
   ```

---

## 5. **Add a README.md File to Both Branches**
### **Example Scenario:**
Suppose you want to add `README.md` to both `main` and `extra-learning` branches.

### **Steps:**
1. Create the file:
   ```sh
   echo "# Project Documentation" > README.md
   ```
2. Add and commit it to `main`:
   ```sh
   git checkout main
   git add README.md
   git commit -m "Added README.md to main"
   git push origin main
   ```
3. Switch to `extra-learning` and merge from `main`:
   ```sh
   git checkout extra-learning
   git merge main
   ```
4. Push the changes to `extra-learning`:
   ```sh
   git push origin extra-learning
   ```
This ensures that `README.md` exists in both branches.

---

## 6. **Merge Files or Folders into `main` from `extra-learning`**
If you need to merge specific changes from `extra-learning` to `main`:

### **Steps:**
1. Switch to the `main` branch:
   ```sh
   git checkout main
   ```
2. Merge changes from `extra-learning`:
   ```sh
   git merge extra-learning
   ```
3. If conflicts occur, resolve them manually, then:
   ```sh
   git add .
   git commit -m "Resolved merge conflicts"
   ```
4. Push the merged changes to `main`:
   ```sh
   git push origin main
   ```

---

## 7. **Delete a Branch (If No Longer Needed)**
To delete a branch locally:
```sh
git branch -d branch-name
```
To delete a branch remotely:
```sh
git push origin --delete branch-name
```

---

## Conclusion
- Use `git checkout` to switch branches.
- Use `git add`, `commit`, and `push` to manage files in specific branches.
- Merge branches when necessary to keep changes in sync.
- Keep `main` for core content and `extra-learning` for additional materials.
- Follow the example to ensure important files like `README.md` exist in both branches.

By following these steps, you can efficiently manage your project workflow in Git. 🚀

