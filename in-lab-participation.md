# SWE 363 - 252 In-Lab Participation

## Overview
Hands-on coding demonstrations and collaborative exercises during class time. About 20 demos throughout the semester, each worth about 0.5% of final grade.


## Requirements

- **Timing**: Complete during class time only (no submissions outside class time are allowed)
- **Format**: Live coding with instructor and peers observing
- **Mandatory**: Class attendance, active engagement


## Technical Requirements

- Code editor (Cursor, VS Code, Sublime Text, etc.)
- Web browser with developer tools
- Git (latest version)
- Node.js for JavaScript development
- Terminal/Command Prompt access

## GitHub Classroom Instructions

### What is GitHub Classroom?
GitHub Classroom is a tool that automatically creates individual repositories for each student when they accept an assignment. This eliminates the need for manual forking and simplifies the submission process.

### How to Accept and Submit the Assignment (GitHub Classroom)

Please **read these instructions carefully**. Incorrect acceptance or submission will result in **marks deduction**.

---

### Important Rules (Read First)

- You must **accept the assignment only via the GitHub Classroom link** provided in **`demos.md`**.
- **Do NOT fork** the assignment repository manually from `Web-Engineering-KFUPM` or anywhere else.
- **Do NOT push** your work to your personal GitHub repositories.
- **Pushing the assignment anywhere other than your GitHub Classroom repository will result in marks deduction.**

---

### Initial Setup (One-time)

1. Open the **`demos.md`** file in this repository.
2. Locate the **Demo Table**.
3. Click the **GitHub Classroom invitation link** for your lab.
4. **Accept the assignment** using that link.
5. **Authorize GitHub Classroom** to access your GitHub account (if prompted).

After acceptance, **your individual repository** will be automatically created.

### Repository Naming Format After Accepting Assignment

```
Demos_Repo_Name_<your_github_username>
```

**Example:**
```
2-1-html-basics-jawwad183
```

This is the **only valid repository** for submission.

---

### Before Each Lab Session

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

### During Lab Sessions (How to Submit Your Work)

1. **Complete all assigned tasks and TODOs** in your local repository.
2. **Add and commit your changes** for each TODOusing clear, descriptive messages:

```bash
git add .
git commit -m "Complete lab exercise: [brief description]"
```

3. **Push your changes** to your GitHub Classroom repository:

```bash
git push origin main
```

This push is your **official submission**.

---

### Submission Requirements

- **Timing**: Must be pushed **before the due date and section time**
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
- Pushing to **any repository not created by GitHub Classroom**

**Only the GitHub Classroom repository will be graded.**

---

## GitHub Classroom Troubleshooting (Quick Guide)

### 1) Verify Correct GitHub Account
- Use the GitHub account registered with your **KFUPM email**.
- If unsure, confirm with your instructor or TA.

### 2) Clear Browser Authentication
- Sign out of all GitHub accounts.
- Clear browser cache and cookies.
- Log in again using your KFUPM-registered account.
- If needed, try Incognito/Private Mode or a different browser.

### 3) Accept the Lab Link
- Open the GitHub Classroom link from `demos.md`.
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

## Optional: GitHub Setup Assignment

Students new to Git and GitHub are encouraged to complete the **optional GitHub setup assignment**, which covers:

- Basic Git commands (`add`, `commit`, `push`, `pull`)
- GitHub repository navigation
- Branching basics
- Resolving merge conflicts

This assignment is **not graded**, but **highly recommended**.

---

## Support Resources

- Instructor office hours
- Teaching assistants during lab sessions
- Peer collaboration during lab time
- Online documentation and tutorials
- **GitHub Starter Course**: https://github.com/Web-Engineering-KFUPM/github-starter-course

---


