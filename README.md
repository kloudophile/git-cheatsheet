## Ultimate Git cheatsheet

Reference ink: https://antonz.org/git-by-example/

# 🚀 THE MASTER GIT OPERATIONS & INFRASTRUCTURE MANUAL
*A Comprehensive, Chronological Reference Guide for Cloud and DevOps Engineers*

---

## 🟢 PHASE 1: THE REPOSITORY FOUNDATION (LOCAL SETTING UP)
*Every great project starts locally on your machine. Think of this phase as laying down the tracking foundation for your folder infrastructure.*

### 🛠️ Turning a Folder into a Repository
* **Command:** `git init`
* **What it does:** Installs a hidden folder named `.git` into your current directory. This turns an ordinary, inactive folder into a live, alert version-controlled repository tracking every character you type.

### 🆔 Signing Your Engineering Signature
* **Commands:**
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your.email@example.com"
  ```
* **What it does:** Registers your digital identity on your machine. Every single backup snapshot (commit) you make will be permanently stamped with this signature, allowing your engineering leads to instantly trace project updates back to you.

### 🛡️ The Secret Security Shield
* **File Name:** `.gitignore` (A hidden text file created inside your main root folder)
* **What it does:** A configuration file telling Git exactly what folders or passwords to blind itself to. 
* **Real-Time Use:** You write file types, paths, or secrets inside it (e.g., `*.pem`, `.env`, `terraform.tfstate`). Git guarantees it will completely ignore these targets and never staging or pushing them, completely neutralizing the risk of cloud credentials leaking onto the public web.

---

## 🌅 PHASE 2: TRACKING FILE MANIPULATIONS (THE LOGISTICS)
*Managing files within a version-controlled project requires specialized Git handling. Modifying names or cleaning folders directly via your OS explorer breaks tracking metadata.*

### 🔀 Safe File Renaming
* **Command:** `git mv <old_name> <new_name>`
* **What it does:** Renames or moves a file cleanly. It lets Git update its tracking markers simultaneously, bypassing the error where your OS thinks you deleted the old file and created an unrelated new one. It places the action immediately on the staging deck in green status.

### 🗑️ Complete File Deletion
* **Command:** `git rm <filename>`
* **What it does:** Deletes the file physically from your laptop's directory and records the deletion event directly onto your Git tracking blueprint.

### 🛑 The "Keep on Laptop, Clear from Cloud" Switch
* **Command:** `git rm --cached <filename>`
* **What it does:** This is a vital emergency tool. It untracks a file from Git's radar (removing it from GitHub on your next push) but safely keeps the physical file sitting right on your laptop hard drive. Crucial for moving files out of Git history and safely into your `.gitignore` rules.

---

## 🎛️ PHASE 3: THE DAILY SAVING & TRACKING LOOP (TIME MACHINE LOOPS)
*The heartbeat of your development day. This cycle represents moving your loose thoughts into secure, trackable local project saves.*

```text
 ┌───────────────┐     git add .     ┌───────────────┐  git commit -m   ┌───────────────┐
 │ Working Tree  │ ────────────────> │ Staging Deck  │ ───────────────> │ Local History │
 │ Loose Changes │                   │  (Green Mode) │                  │ Locked Secure │
 └───────────────┘                   └───────────────┘                  └───────────────┘
```

### 📊 Checking the Workspace Dashboard
* **Command:** `git status`
* **What it does:** Your control screen. Displays exactly what branch you are standing on, what files have loose untracked edits (Red Mode), and what files are ready on the launching pad (Green Mode).

### 🔍 Inspecting Unsaved Details
* **Command:** `git diff`
* **What it does:** Loads a direct line-by-line snapshot showing exactly what characters you typed or deleted before staging. 
* **Reading the output:** Green lines marked with a plus (`+`) indicate new code; Red lines marked with a minus (`-`) show deleted items.

### 🚀 Staging to the Launchpad
* **Command:** `git add .`
* **What it does:** The dot (`.`) tells Git to collect every single loose red modification across your folder and load them safely onto the Staging Area launchpad, flipping their status to green.

### 📸 Locking the Snapshot Record
* **Command:** `git commit -m "prefix: descriptive message"`
* **What it does:** Clicks the shutter on your tracking camera! Locks your green staged changes permanently into your local history book with a semantic tracking note.

### 📖 Inspecting the History Logbook
* **Command:** `git log --oneline`
* **What it does:** Prints a neat, clean timeline of your past snapshots, displaying their unique 7-character commit hash IDs and descriptive tags.

---

## 🌿 PHASE 4: SAFE PLAYGROUND TIMELINES (BRANCH MANAGEMENT)
*Cloud environments require zero downtime. You never write experimental patches directly on stable production code. You construct parallel branch playgrounds.*

### 🗺️ Listing Available Worlds
* **Command:** `git branch`
* **What it does:** Prints out your active timelines. The track you are actively coding inside will display a prominent asterisk (`*`) directly next to it.

### ⚡ Splitting the Timeline
* **Command:** `git switch -c <branch-name>`  (Or classic: `git checkout -b <branch-name>`)
* **What it does:** Instantly clones your current codebase state, creates a parallel branch channel, and drops you inside it. Your main stable line is now isolated from your changes.

### 🏃‍♂️ Shifting Worlds
* **Command:** `git switch <branch-name>`  (Or classic: `git checkout <branch-name>`)
* **What it does:** Seamlessly teleports you from your playground branch right back onto the main master line.

---

## ⚡ PHASE 5: MERGING WORLD TIMELINES (COMBINING PHASES)
*When your feature is complete and verified, you bring its updates back into your master timeline using the core merge process.*

### 🛠️ The Fusion Execution
* **Command:** `git merge <feature-branch>`
* **How it operates:** You must first stand on your destination track (`git switch main`), and then execute the merge pointing to your work branch.

### 🧬 Fast-Forward vs. Three-Way Merge Mechanics
* **Fast-Forward Merge:** Happens when your master line hasn't changed at all since you branched out. Git runs zero complex math—it just slides the master marker forward to match your new commit. Clean and linear.
* **Three-Way Merge:** Happens if a teammate pushed an update to master while you were working on your branch. Your paths have split. Git reads a common baseline point, reviews both paths, and automatically writes a custom Merge Commit to link the timelines back together.

```text
Fast-Forward: [Commit A] ───> [Commit B] ───> (Main advances smoothly to Branch)

Three-Way:     [Commit A] ──┬──> [Your Branch Updates] ──┐
                            └──> [Teammate Pushes] ─────┴─> [New Merge Commit]
```

### ⚔️ Resolving Merge Conflicts
When you and a teammate edit the exact same line of code, Git freezes the merge process, raises a warning shield, and prints a conflict section inside your file. It looks like this:

```text
<<<<<<< HEAD
server_type = "t3.micro"  (Your local code configuration)
=======
server_type = "t3.large"  (The incoming team configuration)
>>>>>>> feature-branch-id
```

#### 🛠️ Resolution Checklist:
1. Open the file in your text editor.
2. Discuss with your team to verify which line is factually correct for infrastructure stability.
3. Manually delete the mechanical markers (`<<<<<<<`, `=======`, `>>>>>>>`) and keep only the single safe code line.
4. Clean the file, stage it via `git add .`, and run `git commit -m "fix: resolve conflict with database server sizing"` to finalize the timeline stitch.

---

## ☁️ PHASE 6: CLOUD SYNC & TEAM VAULTS (HOSTING OPERATIONS)
*Connecting your computer's engine to standard public hosting backplanes like GitHub, GitLab, Bitbucket, or AWS CodeCommit.*

### 🔗 Mapping the Remote Vault Pipeline
* **Command:** `git remote add origin <HOSTING_URL>`
* **What it does:** Installs a high-speed pipeline mapping the local repository directly to your cloud storage vault, nicknaming the link path origin.

### 💾 Bringing Down an Existing Platform Ecosystem
* **Command:** `git clone <HOSTING_URL>`
* **What it does:** Downloads an entire project blueprint along with its full multi-branch tracking history down to your laptop for the first time.

### 🚀 Uploading Local Blueprints to the Cloud
* **Command:** `git push -u origin <branch-name>`
* **What it does:** Fires your snapshots up through the pipeline. The `-u` flag instructs your machine to lock this cloud endpoint mapping in memory, allowing you to just type `git push` on future loops.

### 📥 Downloading Team Master Blueprints
* **Command:** `git pull origin main`
* **What it does:** The ultimate team synchronizer. Connects to the host vault, reviews if teammates posted new commits, and downloads and merges those items directly into your active directory workspace.

---

## 🏷️ PHASE 7: IMMUTABLE INFRASTRUCTURE ROADMAPS (TAG MANAGEMENT)
*Tags are solid, permanent, freeze-frame names tied to vital points in your tracking history. Unlike branches, tags never move or change. They represent official project version milestones.*

### 🎯 Tagging the Current Milestone Release
* **Command:** `git tag <version_number>`  (e.g., `git tag v1.0.0`)
* **What it does:** Places a permanent architectural flag on your absolute latest commit, freezing it as a clear reference mark.

### 📅 Tagging an Older Historic Point
* **Command:** `git tag <version_number> <commit_hash>`
* **What it does:** Reaches back in time to map a milestone marker precisely onto an older snapshot using its 7-character ID token.

### 📊 Reading the Milestone Grid
* **Command:** `git tag -l`

* **What it does:** Outputs a clean catalog of every release tag actively logged inside the repository project history.

### ☁️ Uploading Your Project Tags to the Cloud Host
* **Command:** `git push origin --tags`
* **What it does:** Normal pushes skip tags. This command opens a tracking lane to securely stream all your project version markers up to your GitHub release pages.

---

## 🛡️ PHASE 8: THE RESCUE SWITCHES (CORRECTING ACCIDENTS)

### 🔂 Erasing a Local Save Receipt Safely
* **Command:** `git reset --soft HEAD~1`
* **Use Case:** You just ran `git commit` locally but immediately found a syntax error or forgot a file.
* **The Action:** Erases the history log entry completely, but leaves your physical edits open and green on your dashboard launchpad so you can fix them and save cleanly.

### 🚨 The Total Workspace Reset Button
* **Command:** `git reset --hard HEAD`
* **Use Case:** Total failure. Everything you typed is broken, messy, and you want to completely erase your uncommitted changes.
* **The Action:** Wipes the local slate clean. Obliterates unsaved code edits and forces your folder to warp back into alignment with your last successful save point.

### 🌐 Repairing Mistakes Already Uploaded to the Cloud
* **Command:** `git revert HEAD`
* **Use Case:** You pushed a bad commit live to GitHub that broke a server. You cannot delete history because your teammates have already synchronized with it.
* **The Action:** Moves forward in time. Generates a completely new "cancelling" commit that automatically executes the exact mathematical opposite of your error. Run `git push` afterward to restore sanity across the shared team backplane.

---

## 🏗️ PHASE 9: APPENDIX — THE INTEGRATED PRODUCTION ROADMAP (CI/CD INTEGRATION)
*How this system links directly into cloud automated logic via `.github/workflows/deploy.yml` scripts.*

```yaml
name: Enterprise DevOps Pipeline

on:
  push:
    branches: [ main ] # Trigger event: The moment code lands on main

jobs:
  production-launch:
    runs-on: ubuntu-latest # GitHub boots a temporary clean Linux server
    steps:
      - name: Fetch Current Blueprints
        uses: actions/checkout@v4 # Copies your repository files onto the engine

      - name: Run Cloud Linting Verification
        run: echo "Evaluating syntax configuration layers... Perfect."

      - name: Trigger Infrastructure Rebuild
        # This is where your Docker builds and Terraform deployments execute
        run: echo "Initializing environment. Synchronizing code definitions with live cloud."
```






