# Assignment 2 – Interactive Features

## **Due: Week 9 | Weight: 2%**

## Objective 

In this assignment, you will continue developing your personal portfolio website by improving the work you completed in Assignment 1.

Your main goal is to make your website more interactive and modern.

In this assignment, you are required to:

- Use your Assignment 1 portfolio as the starting point

- Add interactivity (for example: buttons, dynamic content, or user actions)

- Apply modern web development techniques

- Improve the user experience using JavaScript and dynamic behavior

- Use AI-assisted tools when appropriate to enhance your work

By the end of this assignment:

You should have a portfolio website that is more interactive, more engaging, and clearly shows progress beyond Assignment 1.

## Instructions

### 1. Repository Setup

- Create a public GitHub repository named **`id-name-assignment2`**  
  (replace `id` with your student ID and `name` with your first and last name with no space).
- Maintain a clear folder structure, meaningful commit history, and a well-written `README.md`.
- Use branches (recommended).
### Suggested Structure
```
assignment-2/
├── README.md
├── index.html
├── css/
│   └── styles.css
├── js/
│   └── script.js
├── assets/
│   └── images/
├── docs/
│   ├── ai-usage-report.md
│   └── technical-documentation.md
└── .gitignore
```
---
### 2. Dynamic Content

Your web application **must include at least one dynamic feature** where the content changes based on **user interaction**.

#### Requirement
Implement **at least ONE** of the following (or something similar):

- Display content that updates based on user input (e.g., a greeting using a name or time of day)
- Filter or sort content (e.g., show specific projects or reorder them)
- Switch between sections using buttons or tabs (e.g., About, Projects, Contact)
- Show or hide content when clicked (expand / collapse sections)
- Filter content live while typing (simple search functionality)

> You do **not** need to implement all options.  
> Choose **one feature** that fits your portfolio website.

#### Guideline
- The feature must respond to user actions (click, type, select, etc.)
- It should make the site **more interactive and useful**
- It should **not** be purely decorative

#### Tip
Explore professional websites (e.g., [Apple](https://www.apple.com/), [Airbnb](https://www.airbnb.com/)) and observe how content changes when users interact.  
Even a **simple interactive feature** is sufficient if it works correctly and is clearly implemented.

---
### 3. Data Handling

Your project must demonstrate **basic data handling** using JavaScript.

#### Requirement  
Implement **at least ONE** of the following:

- Use **localStorage** to save user preferences (e.g., dark or light theme , name, settings)
- Fetch and display data from a **public API** (e.g., books, music, sports, fun facts)
- Create a **simple form** that validates user input and shows a confirmation message

#### Guideline
- If data fails to load, show a **clear and friendly error message**
- Do not leave the user without feedback

---

### 4. Animation and Transitions

Use **simple animations or transitions** to improve the user experience.

#### Requirement  
Add **at least ONE** of the following:

- Smooth transitions when switching sections
- Hover effects on buttons, cards, or links
- Fade-in or slide-in effects for text or images
- Animated success or error messages

#### Guideline
- Animations should be **smooth and helpful**
- Avoid distracting or heavy effects

---

### 5. Error Handling and User Feedback

Your application must clearly communicate with the user.

#### Requirement  
Include **basic user feedback**, such as:

- Error messages for invalid or empty form inputs
- Friendly messages when an API request fails
- A loading indicator (e.g., “Loading…”) when fetching data
- Empty state messages (e.g., “No projects found”)

#### Guideline
- Always tell the user **what happened** and **what to do next**

---

### 6. AI Enhancement

You must use **AI tools** to assist with at least **one part** of this assignment.
  List the AI tools you used (e.g., ChatGPT, Copilot) and explain how you used each tool during the assignment.
  - **Recommended AI Tools**
    - GitHub Copilot → Code completion & generation  
    - ChatGPT / Claude → Problem-solving & explanations  
    - Cursor → AI-powered code editor  
    - Replit → AI-assisted online IDE  
    - AWS CodeWhisperer → AI code generation 

#### Acceptable AI Uses
- Code generation or suggestions
- Debugging help
- Code review or improvements
- Writing documentation or text
- UI/UX or accessibility suggestions

#### Requirements
- You must **understand** any AI-generated code
- You must **edit or improve** the AI output
- AI should support learning, not replace it

#### Documentation (Required)
You must include a report at:`docs/ai-usage-report.md`



### 7. Documentation
Your `README.md` should include:  
- Project description  
- Setup instructions (how to run locally)  
- Short summary of AI use (detailed in `ai-usage-report.md`)  
- Optional live deployment link (GitHub Pages, Netlify, Vercel)  

---

### 8. Submission Process
1. Create a new GitHub repository for the assignment.  
2. Develop and test all required features.  
3. Update `README.md` and technical documentation.  
4. Review to ensure all requirements are met.  
5. Submit your repository link through Blackboard.  


### 9. Academic Integrity
#### Allowed
- AI-assisted tools  
- Peer discussion of ideas  
- Sharing setup guides or references  
- High-level feedback  

#### Not Allowed
- Copying code from classmates  
- Plagiarism or misrepresentation  
- Unauthorized collaboration  
- Submitting unmodified AI output as your own  

`Always be transparent: document how you used AI or peer help, and ensure you understand your solution.`  

### 10. Grading Rubric

The submission will be graded out of 100 points, divided as follows:

| **Criteria** (points)        | **Excellent** (90–100%)                                      | **Very Good** (80–89%)                 | **Good** (70–79%)                         | **Acceptable** (60–69%)              | **Poor** (0–59%)                 |
| ---------------------------- | ------------------------------------------------------------ | -------------------------------------- | ----------------------------------------- | ------------------------------------ | -------------------------------- |
| **Technical Implementation** |                                                              |                                        |                                           |                                      |                                  |
| Functionality (10)           | All required features fully implemented; website functional. | Most features work; minor issues.      | Some features missing/ partially working. | Few features working; major gaps.    | Features missing or site broken. |
| Code Quality (10)            | Clean, readable, well-structured, consistently formatted.    | Mostly clean; minor inconsistencies.   | Functional but messy/ inconsistent.       | Poor structure; minimal comments.    | Disorganized or incomplete.      |
| Performance (10)             | Efficient, optimized; loads quickly across devices.          | Mostly efficient; minor slowdowns.     | Adequate performance; noticeable delays.  | Performance issues in several areas. | Very slow/ inefficient.          |
| Compatibility (10)           | Works seamlessly across major browsers/ devices.             | Works on most platforms; minor issues. | Works but limited compatibility.          | Many compatibility problems.         | Not compatible across platforms. |
| **Documentation**            |                                                              |                                        |                                           |                                      |                                  |
| README Quality (10)          | Comprehensive, professional, well-structured.                | Mostly complete; minor gaps.           | Basic README; limited details.            | Minimal README.                      | README missing/ unusable.        |
| Setup Instructions (10)      | Easy-to-follow installation/ usage guides.                   | Clear but missing minor detail.        | Exists but not fully clear.               | Minimal/ confusing instructions.     | Missing instructions.            |
| Technical Details (10)       | Proper technical documentation provided.                     | Mostly complete; minor gaps.           | Basic details with gaps.                  | Minimal documentation.               | No technical details.            |
| User Experience (10)         | Clear, user-friendly guidance/ explanations.                 | Mostly clear; some gaps.               | Adequate but not user-friendly.           | Minimal focus on user clarity.       | No UX guidance.                  |
| **AI Integration**           |                                                              |                                        |                                           |                                      |                                  |
| Effective Use (5)            | AI tools used meaningfully and appropriately.                | AI tools used effectively; minor gaps. | AI used but not well aligned.             | Minimal/ shallow AI use.             | No AI use.                       |
| Documentation (5)            | Clear and complete documentation of AI usage.                | Mostly clear; minor gaps.              | Exists but lacks detail.                  | Minimal documentation.               | No documentation.                |
| Understanding (5)            | Strong comprehension of AI outputs/ adaptations.             | Good understanding; minor gaps.        | Partial understanding shown.              | Weak comprehension.                  | No understanding demonstrated.   |
| Innovation (5)               | Creative, innovative use of AI for problem-solving.          | Some creativity and innovation.        | Limited innovation.                       | Minimal innovation.                  | No innovation.                   |

##  Notes

- Keep this assignment focused on adding interactivity and usability rather than trying to build a perfect design.
- This assignment is worth 2% of your grade.
- Use AI responsibly, your documentation should clearly explain how AI supported your work and learning process.
- The features you build here will become part of your professional portfolio website in later assignments, so aim for clarity, good structure, and functionality you can expand on.

##  Wrapping Up

Think of these guidelines as a help guide with ideas to get you started. You don’t have to follow every example, feel free to explore and shape the web application in a way that reflects your own interests. Creativity and originality are welcome as long as the core requirements of the assignment are met.

Most importantly, enjoy building, experimenting, and making the web application your own! 
