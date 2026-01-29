# Milestone 4️⃣ - Front-End 

## 🎯 Objective:
Develop a fully interactive front-end prototype for your web application using React. The prototype should demonstrate all key functionalities and interactivity. While the UI design phase is now optional, a reference Figma file is required to evaluate your ability to translate UI requirements into code.

## 🛠️ Github Setup:
### 1. All students should get the Github Education Pack:
- Access this link [github.com/education](https://github.com/education)
- Fill the necessary requirement to apply the student pack here [education.github.com/discount_requests/application](https://education.github.com/discount_requests/application)
- You can see the benefits here [education.github.com/pack](https://education.github.com/pack)

### 2. How to create/clone the GitHub repository:
- Tutorial how to `Create the Github repository`: [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository)
- Tutorial how to `Clone the Github repository`: [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository). There you can find many option how to clone Github repository. Either it's from Mac, Windows, or Linux and by using Github CLI, [Desktop](https://github.com/apps/desktop), or Web browser.

### 3. How to create Git branches:
- This is the official tutorial from Github to create and delete branches: [Click here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository)
- The code on `main` or master `branch` is used to production phase (deployed live)
- Use another branches to do the development before merge it into `main` or `master` branch.
- Change between branch by using `git checkout target_branch_name`.

### 4. How to commit/push/pull commits and into the Git repository:
#### 4.1 The basic flow:
  ```
  git add file_name.extension
  git commit -m "commit message, LGTM! (Looks good to merge)"
  git push origin main
  ```
- `git add` basically to set which files that are needed to be pushed on the repository. [Source](https://github.com/git-guides/git-add).
- `git commit` is to give the commit message. It can be used to give the information about the changes/updates. For example in [this commit](https://github.com/hammadojh/web_course/commit/273fd6ef0d626681ad1c234c89df4c9accf4b2f9), the commit message is `Update the Tentative Lectures Plan`. [Source](https://github.com/git-guides/git-commit).
- `git push` is to push the changes into the Github repository. You can change the `origin` into your repository URL and change `main` branch into your desired branch. [Source](https://github.com/git-guides/git-push).
- Kindly read the flow [here](https://medium.com/@itsmepankaj/git-workflow-add-commit-push-pull-69adf44cf812).

#### 4.2 Pulling the updates
- `git pull` basically pulling/downloading the latest changes from the specific branch into your local branch (in development environment).
- Kindly read more about the Git Pull [here](https://www.w3schools.com/git/git_pull_from_remote.asp).

Note:
- May be it's intimidating when trying the Git flow on the first time. But it's very usefull for who want to working in digital industry as well. They're using Git (github or gitlab) daily.
- For first user, please get used with those git commands. Those are the basic commands to working collaborately using Git.
- When merging the `development` branch into `main` branch you can use the GUI instead of through CLI.

## 🥋 Instructions:

### 1. UI Design (OPTIONAL but Recommended):
- If you choose to design the UI, create a **Figma file** that includes:
  - Key screens and use cases for your application (e.g., Login, Dashboard, Profile, Error Pages, etc.).
  - High-fidelity designs with **pixel-perfect representation** (colors, fonts, icons, and images).
  - Interactive components (e.g., dropdowns, modals, form submissions).
  - Responsive designs for both desktop and mobile views.
  - Prototyped user flows linking all screens.
- If you skip the UI design, you must still provide a **reference Figma file** (e.g., a basic wireframe or template) to guide your front-end implementation.

### 2. Front-End Implementation:
- Use **React** as the front-end framework to build your application.
- Implement the HTML, CSS, and JavaScript based on your Figma design.
- You may use a CSS framework (e.g., Bootstrap, TailwindCSS) to enhance your design and save time.

### 3. Functional Requirements:
- Ensure that the following are implemented:
  - All user flows and features as outlined in the design.
  - Fully interactive components (e.g., buttons, forms, menus).
  - Responsive design to support both desktop and mobile views.

### 4. GitHub Repository:
- Create a GitHub repository for your project.
  - Add all team members as collaborators.
  - Each team member must contribute to the repository using their account.
  - Contributions will be monitored via GitHub's contribution graph, so avoid pushing all code from a single account. We can see the contributors from the commit history also.

#### Repository Guidelines:
- Documentation:
  - Include a README.md file with:
    - Project title and description.
    - Setup and installation instructions.
    - Usage instructions and examples.
    - Team member names and roles.
  - Any additional documentation required for setting up the front-end (e.g., API keys, environment variables) should be provided but not hard-coded.
- Best Practices:
  - Use `.gitignore` to exclude unnecessary files such as libraries, node modules, and sensitive information (e.g., API keys, .env files).
  - Structure your repository logically (e.g., src folder for components, assets folder for images).

### 4. Submission Guidelines:
- Submit your GitHub repository link via Blackboard under the designated assignment.
  - Ensure the repository is publicly accessible or grant access to instructors/teaching assistants.
  - Push all completed code to GitHub before the deadline.
- A GitHub repository containing:
  - Well-documented code.
  - A clear README file with installation and usage instructions.
  - Proper file and folder structure.
- Submit the Figma Prototype Link via Blackboard under the designated submission area (OPTIONAL).
  - Ensure the link is set to “View Only” access.

### 5. Notes:
- Ensure your front-end is as close as possible to the your Figma design.
- Document your GitHub repository clearly to make it easy to set up and understand:
  - Add installation and usage instructions.
  - Explain dependencies and frameworks used.
- Contribution will be graded based on GitHub's contribution metrics. Ensure that all team members contribute code individually.

## 📊 Grading Rubric:
The submission will be graded out of 100 points, divided as follows:

| **Criteria (Points)** | **Excellent (90-100%)** | **Very Good (80-89%)** | **Good (70-79%)** | **Acceptable (60-69%)** | **Poor (0-59%)** |
|-----------------------|-------------------------|------------------------|-------------------|-------------------------|------------------|
| **Accuracy and Completeness of Design (30)** | The implemented design matches the Figma prototype perfectly, including all details and screens. | The design closely matches the Figma prototype with minor deviations or missing elements. | The design matches the Figma prototype partially, with noticeable missing elements or inaccuracies. | The design has significant deviations from the Figma prototype or missing key elements. | The design is incomplete, inconsistent, or lacks significant alignment with the Figma prototype. |
| **Functionality and Interactivity (30)** | All front-end functionalities work flawlessly, and the app is fully interactive with a seamless experience. | Most functionalities and interactivity are implemented with minor issues. | Some functionalities are implemented, but there are noticeable gaps in interactivity or functionality. | Minimal functionality is implemented, with significant interactivity gaps. | Functionality and interactivity are either missing or non-functional. |
| **Responsiveness (10)** | The layout is fully responsive across all devices, with no issues on desktop or mobile. | The layout is responsive, with minor issues on either desktop or mobile. | The layout is somewhat responsive, with noticeable issues in responsiveness. | The layout has limited responsiveness, with significant issues on multiple devices. | The layout is not responsive and does not work properly on desktop or mobile. |
| **Clear Documentation (10)** | GitHub repository is well-documented, including a detailed README with setup instructions and usage details. | GitHub repository is documented, but setup instructions or some details are unclear. | GitHub documentation exists but is incomplete or lacks clarity. | GitHub documentation is minimal and insufficient for understanding the project.  | GitHub repository lacks documentation or contains inaccurate information. |
| **File Structure and Version Control (10)** | Repository has a clear file structure, proper `.gitignore` usage, and excellent version control practices. | Repository has a mostly clear file structure and good version control, with minor improvements needed. | Repository has an acceptable file structure but lacks proper `.gitignore` usage or good version control practices. | Repository file structure or version control is poorly implemented. | Repository lacks organization, `.gitignore`, or version control practices. |
| **Individual Contributions (10)** | All team members have significant and tracked contributions on GitHub. | Most team members have significant contributions tracked on GitHub. | Some team members have tracked contributions, but participation is uneven. | Contributions are minimal, and a few team members dominate the work. | Contributions are absent or lack any evidence of teamwork. |
