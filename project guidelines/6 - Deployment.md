# Milestone 6️⃣ Deployment of the Final Application

## 🎯 Objective:
Deploy your web application to a live environment, making it accessible to users via a public URL. This milestone focuses on ensuring your project is fully functional, accessible online, and represents a polished, production-ready version of your application.

## 🥋 Instructions:

### 1. Deployment Platform:
- Deploy your application on **any hosting platform of your choice**. Examples include:
  - Cloud Platforms: AWS, Google Cloud, Microsoft Azure.
  - Web Hosting Services: Vercel, Netlify, Heroku, Render.
  - Dedicated Server: VPS services like DigitalOcean, Linode, or any custom server.
- Ensure the platform you choose supports both your front-end and back-end.
- Kindly check [this](https://medium.com/@avinashukla0704/how-to-deploy-a-combined-react-and-node-js-app-on-vercel-2cb75574cad9) or [this](https://youtu.be/YYmzj5DK_5s?si=pRFOK_nxDQNRy1Xi) tutorial as a references to deploy React + Express app.

### 2. Deployment Requirements:
- Deploy both the front-end and back-end to the same or compatible hosting environments.
  - Ensure the back-end is properly configured to handle API requests and interact with the database.
  - Ensure the front-end fetches data from the back-end without errors.
- Use an appropriate (cloud) database hosting solution **if required**. For example, MongoDB Atlas for MongoDB.

### 3. Configurations:
- Configure your environment for production:
  - Use appropriate environment variables for sensitive data (e.g., API keys, database URIs).
  - Ensure security configurations like CORS and HTTPS are properly handled.
- Optimize your application for deployment:
  - Minify assets (CSS, JavaScript, images) to improve performance.
  - Ensure responsiveness and proper rendering across devices.

### 4. Testing:
- Test the live application thoroughly to ensure:
  - All functionalities work as intended (forms, APIs, responsiveness, etc.).
  - There are no fatal errors or broken links.
  - The application performs well under typical usage (both in mobile and desktop views).

### 5. Submission Guidelines:
- Submit the URL of your live application via Blackboard under the designated assignment.
- Ensure the URL is accessible to anyone with the link (no authentication required to view the main page).
- If applicable, include any additional credentials (e.g., demo user login details) in the submission to facilitate testing.
- It’s fine if there are still some bugs or small features that are not finished. As long as you tell us where they are, what is the solution to it's problem, and all of it can be resolved before the presentation day.
- Short video about how to use your website properly.

## 📊 Grading Rubric:
The submission will be graded out of 100 points, divided as follows:

| **Criteria (Points)** | **Excellent (90-100%)** | **Very Good (80-89%)** | **Good (70-79%)** | **Acceptable (60-69%)** | **Poor (0-59%)** |
|-----------------------|-------------------------|------------------------|-------------------|-------------------------|------------------|
| **Front-End and Back-End Functionality (25)** | Front-end and back-end are fully functional with seamless integration, meeting all requirements. | Front-end and back-end are mostly functional, with minor issues or limitations in integration. | Front-end and back-end are functional but have noticeable bugs or missing features. | Front-end and back-end have significant functional gaps or unreliable integration. | Front-end and back-end are non-functional or not implemented. |
| **Database Integration (25)** | Database is fully integrated, with efficient queries and no errors. | Database is integrated, with minor inefficiencies or occasional errors. | Database integration is partially functional, with noticeable inefficiencies or bugs. | Database integration has significant issues, errors, or incomplete functionality. | Database integration is absent or non-functional. |
| **Performance (10)** | Application loads quickly and handles user interactions seamlessly under realistic conditions. | Application performs well but shows minor delays or performance issues. | Application is functional but has noticeable performance delays or interaction lags. | Application is functional but suffers from frequent delays or unresponsive behavior. | Application is slow, unresponsive, or crashes frequently. |
| **Accessibility and Responsiveness (10)** | Application is fully responsive and accessible on both mobile and desktop, with no layout issues. | Application is responsive and accessible, with minor layout or accessibility issues. | Application has basic responsiveness but lacks consistent accessibility across devices. | Application is minimally responsive and has significant layout or accessibility gaps. | Application is not responsive or accessible. |
| **Environment Variables and Security (10)**| Environment variables and sensitive information are properly handled and secured. | Environment variables and sensitive information are mostly secured, with minor vulnerabilities.  | Environment variables are used but have noticeable security or handling gaps. | Minimal use of environment variables or security measures, with significant issues. | Environment variables and security measures are absent or poorly implemented. |
| **HTTPS and Security Measures (10)** | HTTPS is implemented, and other security measures (e.g., authentication, authorization) are robust. | HTTPS is implemented, with minor issues or gaps in other security measures. | Basic security measures are implemented but lack robustness or completeness. | Minimal security measures are implemented, with significant vulnerabilities. | Security measures are absent or inadequate. |
| **Live URL Submission (5)** | Live URL is submitted and accessible without errors. | Live URL is submitted and accessible with minor issues. | Live URL is submitted but has noticeable errors or is inaccessible at times. | Live URL is submitted but is largely inaccessible or error-prone. | Live URL is not submitted or is completely inaccessible. |
| **Peer Review Submission (5)**| Peer review is submitted on time, with constructive and detailed feedback provided for other groups. | Peer review is submitted on time, with helpful but slightly less detailed feedback. | Peer review is submitted but lacks depth or significant constructive feedback. | Peer review is minimally completed, with little useful feedback provided. | Peer review is missing, incomplete, or submitted late without justification. |