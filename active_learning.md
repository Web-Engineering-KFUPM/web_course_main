# SWE 363 - 261 Active Learning

## Overview
Hands-on learning using exercises and pracive material is essential for mastering the course material. 

## Requirements
### How to get the active learning efforts marks?
- **Mandatory**: Class attendance, active engagement, visiable in-lab learning efforts.
- **Format**: Live coding with instructor, peers observing, hands-on exercises, practice material, etc.
- **Timing**: Complete exercies and practice by assigned deadlines(no submissions after dedline are allowed)

### How to lose the active learning efforts marks?
- Not attending the class.
- Leaving the class early after the lecture part is completed.
- Not completing the exercises and practice material by assigned deadlines.
- Not following the instructions provided in the active learning efforts guidelines.

## Technical Requirements

- Code editor (e.g. Cursor, WebStorm, VS Code, Sublime Text, etc.)
- Web browser with developer tools (e.g. Chrome, Firefox, Edge, etc.)
- Git (latest version)
- Node.js for JavaScript development (e.g. Node.js, npm, npx, etc.)
- Terminal/Command Prompt access (e.g. Terminal, Command Prompt, PowerShell, etc.)
- Github account, GitHub CLI

## Classroom50 Instructions

The full Classroom50 student guide (setup, screenshots, tag submission, and troubleshooting) is in [`Classroom50 Student Guide.md`](./exercises%20guidelines/Classroom50%20Student%20Guide.md).

### Important Rules (Read First)

- You must **accept the assignment via the Classroom50 link** provided in **`exercises.md`**.
- **Do NOT fork** the assignment repository manually from `Web-Engineering-KFUPM` or anywhere else.

---

### Initial Setup (One-time)

1. Open the **`exercises.md`** file in this repository.
2. Locate the **exercises Table**.
3. Click the **Classroom50 invitation link** for your lab.
4. **Accept the assignment** using that link.
5. **Authorize Classroom50** to access your GitHub account (if prompted).

After acceptance, **your individual repository** will be automatically created.

### Repository Naming Format After Accepting Assignment

```
Exercises_Repo_Name_<your_github_username>
```

**Example:**
```
2-1-html-basics-jawwad183
```

This is the **only valid repository** for submission.

---

### Before Each Exercise Session

1. **Clone your assignment repository** (only once):

```bash
git clone https://github.com/Web-Engineering-KFUPM/[ASSIGNMENT-NAME]-[YOUR-USERNAME].git
cd [ASSIGNMENT-NAME]-[YOUR-USERNAME]
```

2. **Pull the latest updates** (if any):

```bash
git pull origin main
```

---

### During Exercise Sessions (How to Submit Your Work)

1. **Complete all assigned tasks and TODOs** in your local repository.
2. **Add and commit your changes** for each TODOusing clear, descriptive messages:

```bash
git add .
git commit -m "Complete lab exercise: [brief description]"
```

3. **Push your changes** to your Classroom50 repository:

```bash
git push origin main
```

This push is your **official submission**.

---

### Submission notes

- **Timing**: Must be pushed **before the due date**
- **Content**: All required files and **all TODOs must be completed**
- **Quality**: Code must be functional and properly formatted
- **Documentation**: Add comments where appropriate
- **Commit Messages**: Use descriptive and professional messages

**Full marks** are awarded only if **all conditions above are met**.

---

### Mistakes Students Commonly Make

Forking the assignment repository manually

Accepting the assignment correctly but:
- Pushing to your **personal GitHub repository**
- Pushing to a **forked repository**
- Pushing to **any repository not created by Classroom50**

**Only the Classroom50 repository will be graded.**

---

## Classroom50 Troubleshooting (Quick Guide)

### 1) Verify Correct GitHub Account
- Use the GitHub account registered with your **KFUPM email**.
- If unsure, confirm with your instructor or TA.

### 2) Clear Browser Authentication
- Sign out of all GitHub accounts.
- Clear browser cache and cookies.
- Log in again using your KFUPM-registered account.
- If needed, try Incognito/Private Mode or a different browser.

### 3) Accept the Lab Link
- Open the Classroom50 link from `demos.md`.
- If successful, your private assignment repository will be created.

### 4) Clone the Repository

```bash
git clone <classroom_repo_link>
```

### 5) Make Changes and Commit

```bash
git status
git add .
git commit -m "Your commit message"
```

### 6) Fix Push / Commit Issues

If `git push` fails, configure your Git identity:

```bash
git config --global user.name "Your GitHub Name"
git config --global user.email "your_kfupm_email@example.com"
```

### 7) Push Your Changes

```bash
git push origin main
```

### 8) Still Having Issues?
- Confirm you are using the GitHub account linked to Classroom
- Re-authenticate GitHub on your machine
- Contact the instructor or TA to verify Classroom account mapping

---

## Support Resources

- Instructor office hours
- Teaching assistants office hours
- Peer collaboration during lab time
- Online documentation and tutorials
- **GitHub Starter Course**: https://github.com/Web-Engineering-KFUPM/github-starter-course

---


