# Assignment 3️⃣ – Advanced Functionality

## **Due: Week 13 | Weight: 2%**

## 🎯 Objective

This is your third step in developing your personal portfolio web application. The goal here is to expand your skills further and demonstrating stronger programming practices. In this assignment you will:

- Implement complex web application features
- Integrate external APIs and services
- Demonstrate advanced JavaScript programming
- Showcase problem-solving and debugging skills

By the end of this assignment, you will have a more powerful and feature-rich portfolio web application that highlights your ability to work with advanced functionality and external integrations, building on the foundations from Assignments 1 and 2.

## 🥋 Instructions

### 1. Repository Setup

- **Public Repository**: Create a public GitHub repository called `assignment-3`.
- **Clear Structure**: Well-organized file and folder structure
- **Documentation**: Comprehensive README.md files
- **Commit History**: Meaningful commit messages showing development progress
- **Branching**: Use of feature branches for development (recommended)
- Organize your files in a simple structure like this:

```
assignment-3/
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

### 2. API Integration

Your web application must connect to at least one external API to fetch and display data in a meaningful way. The examples below are a few suggestions to help you get started, choose an API that makes sense for your portfolio.

- Display your latest GitHub repositories using the GitHub API.
- Show current weather information using a free weather API.
- Fetch and display inspirational quotes from a quotes API.
- Pull in images or icons from a public image API (for example: Unsplash or Pexels).
- Integrate a news or article feed that updates dynamically.

⚡ Guideline: Always handle errors gracefully (for example: if the API is unavailable, show a friendly message instead of leaving a blank section).

💡 Pro Tip: Many APIs offer free versions with no signup required. Start with something simple and relevant to your portfolio. For instance, fetching your GitHub projects can make your website feel “live” and up-to-date.

### 3. Complex Logic

Implement sophisticated application logic in your project by adding features that use conditions, rules, or multiple steps of logic. This does not need to be complicated, the goal is to show that you can think beyond one-click interactions.

- Create a project list that can be both filtered and sorted (for example: “Show Web Projects” and then sort them by date).
- Add a contact form with extra checks (for example: make sure fields are not empty, confirm the email looks valid, and only then allow submission).
- Show different messages or sections depending on user choices (for example: if a visitor selects “Beginner,” show beginner projects; if “Advanced,” show advanced ones).
- Add a timer or counter (for example: display how long a visitor has been on your site, or count down to an event).

⚡ Guideline: Focus on clear, step-by-step logic that improves your portfolio. Even small features can feel “sophisticated” if they combine more than one condition or rule.

### 4. State Management

Handle application state effectively so your web application remembers and updates information as users interact with it.

- Keep track of whether the site is in light mode or dark mode and update it instantly.
- Remember if a user is logged in or logged out (you can simulate this with a simple toggle).
- Show or hide a section based on a button click (for example: click "Show Projects" to display, and "Hide Projects" to remove it).
- Remember a visitor’s name after they type it once, and display it in a greeting message.

⚡ Guideline: Good state management makes your application feel consistent and reliable. Focus on small but useful features that show you can store and update information correctly.

### 5. Performance

Optimize your web application for speed and efficiency so it loads quickly and runs smoothly.

- Compress or resize large images so they load faster.
- Remove unused code, files, or images that slow things down.
- Use efficient CSS and JavaScript (for example: avoid repeating the same code many times).
- Test your site with tools like Lighthouse or PageSpeed Insights to check loading speed.

⚡ Guideline: Focus on easy steps that reduce load time and create a smoother experience for visitors.

### 6. AI Innovation

Use AI to create unique features or solve complex problems in your web application. Examples of acceptable use include:

- **Code Generation**: GitHub Copilot, ChatGPT, Claude, etc.
- **Debugging**: AI-powered debugging assistants
- **Code Review**: AI tools for code quality improvement
- **Documentation**: AI assistance for writing documentation
- **Design**: AI tools for UI/UX suggestions

For every use of AI:

- **Documentation**: Clearly document how AI was used in each assignment
- **Understanding**: Demonstrate understanding of AI-generated code
- **Modification**: Show ability to modify and improve AI suggestions
- **Ethics**: Use AI responsibly and ethically
- **Learning**: Use AI as a learning tool, not a replacement for understanding

The assignment must include a report detailing:

- **Tools Used**: List of AI tools and services utilized
- **Use Cases**: Specific ways AI was employed in development
- **Benefits**: How AI improved the development process
- **Challenges**: Difficulties encountered with AI tools
- **Learning Outcomes**: Skills gained through AI-assisted development

⚡ Guideline: You must document all AI usage in `docs/ai-usage-report.md`. Include the tool you used, the prompt, the output, your edits, and what you learned.

### 7. Documentation

Your `README.md` should include:

- A description of the project.
- Instructions on how to run it locally.
- A short summary of AI tools used (with the detailed log kept in `ai-usage-report.md`).
- Optional: a link to a live deployment (GitHub Pages, Netlify, or Vercel).

## 📦 Deliverables

- Advanced web application with API integration
- Comprehensive technical documentation
- API integration report and usage examples
- Performance benchmarks and optimization strategies

## 📂 Submission Process

1. **Repository Setup**: Create a new repository for the assignment
2. **Development**: Complete all requirements and testing
3. **Documentation**: Update README and technical documentation
4. **Final Review**: Ensure all requirements are met
5. **Submission**: Submit repository link through Blackboard

## 🛠 Support and Resources

Take advantage of the following resources to guide and support your learning:

### Available Help

- Office Hours: Attend regular instructor office hours for technical support.
- Discussion Board: Use the course discussion board for peer-to-peer help, sharing ideas, or asking questions.
- Documentation: Review the course materials and recommended external resources.
- AI Tools: For coding assistance, debugging, and exploration (see recommended tools below).

### Recommended AI Tools

- **GitHub Copilot**: Code completion and generation
- **ChatGPT/Claude**: Problem-solving and code explanation
- **Cursor**: AI-powered code editor
- **Replit**: AI-assisted online development environment
- **CodeWhisperer**: AWS AI code generators

## 📜 Academic Integrity

### Permitted Collaboration

- AI Tools: You may fully use AI-assisted development tools.
- Peer Discussion: Talking about concepts, approaches, and general ideas is allowed.
- Documentation: You may share setup guides or documentation references.
- Code Review: Providing or receiving high-level feedback is acceptable.

### Prohibited Activities

- Direct Code Sharing: Do not copy/paste code from classmates.
- Plagiarism: Do not submit work that is not your own.
- Unauthorized Collaboration: Do not work jointly on individual assignments.
- Misrepresentation: Do not present unmodified AI-generated work as entirely your own.

⚡ Guideline: Always be transparent about your workflow. If AI or peers helped, document it. What matters most is that you understand your solution and can explain it clearly.

## 💯 Grading Rubric

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

## 📝 Notes

- Keep this assignment focused on implementing advanced functionality and solving problems.
- This assignment is worth 2% of your grade.
- Use AI responsibly, your documentation should clearly explain how AI supported your work and learning process.
- The advanced features you add here will continue building your professional portfolio website, so aim for clarity, strong logic, and functionality you can showcase with confidence.

## 🎉 Wrapping Up

Think of these guidelines as a help guide with ideas to get you started. You don’t have to follow every example, feel free to explore and shape the web application in a way that reflects your own interests. Creativity and originality are welcome as long as the core requirements of the assignment are met.

Most importantly, enjoy building, experimenting, and making the web application your own! 🚀
