# Milestone 5 Back-End Implementation

## Objective:
Develop the back-end of your web application using Node.js and Express.js. Integrate a MongoDB database to manage your application data. This milestone focuses on building and implementing the server-side logic, database interactions, and APIs required for your application.

## Instructions:

### 1. Back-End Implementation:
- Use Node.js and Express.js as your back-end framework to implement the functionality defined in your project requirements (Milestone 3).
- Set up a MongoDB database for storing and managing application data.
  - Use a cloud database service like MongoDB Atlas **OR** a local instance of MongoDB. Here is the tutorial how to set up MongoDB Atlas: [click](https://www.mongodb.com/resources/products/platform/mongodb-atlas-tutorial).
  - Make sure you are able to connect the MongoDB and NodeJS to perform the DB operation on your [Express](https://expressjs.com/) website. Kindly follow the tutorial [here](https://www.mongodb.com/docs/drivers/node/current/quick-start/) or [here](https://www.w3schools.com/nodejs/nodejs_mongodb.asp).

### 2. Functional Requirements:
- Implement RESTful APIs to support the operations required by your application.
  - Examples: User authentication, CRUD operations, and data retrieval based on user input.
- Ensure proper data validation for all incoming requests.
- Implement error handling and return appropriate HTTP status codes for success and failure scenarios.

### 3. Repository Management:

#### 3.1 Collaboration:
- Use the same GitHub repository created for the project.
- Contributions will be monitored via GitHub, so ensure all team members participate actively in coding. We can see the contributors from the Github's commit histories.

#### 3.2 Documentation:
- Update the README.md to include:
  - Clear instructions for setting up and running the back-end server.
  - Details about the environment variables required for the database connection or other configurations.
  - API documentation (routes, methods, request/response structure), including example requests and responses.

#### 3.3 Best Practices:
- Ensure proper folder structure. Actually there is no the correct folder structure for every NodeJS project because every project has their own characteristic. But please consider these references to structuring your files:
    - [Reference 1](https://mr-alien.medium.com/folder-structure-for-nodejs-expressjs-project-56be9ec35548)
    - [Reference 2](https://blog.logrocket.com/organizing-express-js-project-structure-better-productivity/)
    - [Reference 3](https://www.geeksforgeeks.org/folder-structure-for-a-node-js-project/)
    - [Reference 4](https://medium.com/@ibrahimhz/my-node-js-express-js-project-folder-structure-for-maintainability-and-scalability-2c578eb863f2)
    - [Reference 5](https://dev.to/nermine-slimane/how-to-structure-your-express-and-nodejs-project-3bl)
  - Structuring your files is benefiting you when you are working on large group and real-world project.
- Follow best practices for version control:
  - Make regular commits with clear commit messages.
  - Avoid pushing sensitive information (e.g., API keys, database credentials) to the repository.
  - Use `.gitignore` to exclude unnecessary files like `node_modules` and sensitive configuration files.

### 4. Integration:
- Ensure your back-end APIs can communicate effectively with the front-end prototype developed in Milestone 4.
- Test all API endpoints using tools like **[Postman](https://www.postman.com/downloads/) or cURL** before integrating them with the front end. To get to know quickly about Postman and cURL, kindly check the tutorial [here Postman](https://www.geeksforgeeks.org/postman-tutorial/) and [here (cURL)](https://www.geeksforgeeks.org/using-curl-to-make-rest-api-requests/).

### 5. Submission Guidelines:

#### 5.1 Code:
- Push all back-end code changes to the GitHub repository created for your project.
- Submit the GitHub repository link via Blackboard under the designated assignment.

#### 5.2 AI Usage Declaration:
- Every submission for this milestone **must** include an AI Usage Declaration, following the [AI Usage  Guidelines](./0%20-%20AI%20Usage%20Guidelines.md).
- Submit via Blackboard:
  1. `Team [N] SWE 363-[SEC] - Phase 5 - AI Declaration.pdf`, with an individual declaration from **every** team member, signed by all members.
  2. `Team [N] SWE 363-[SEC] - Phase 5 - AI Evidence.zip`, containing **full copies of all AI conversations and intermediate artifacts** (required if any member used AI).
- In your GitHub repository, **append** a **"Phase 5 – Back-End"** section to `AI_USAGE.md` (do not overwrite the Phase 4 section).
- **Never** paste database connection strings, API keys, or `.env` content into AI tools or into the logs. Redact them as `[REDACTED]`.
- If no member used AI, you must still submit the declaration, with each member choosing the **"I did not use any AI tools"** option, and state this in `AI_USAGE.md`.
- **No declaration = 0 for this milestone.** A declaration that reports AI use without the full conversations and artifacts is treated as missing.
- A false "No AI" declaration, or undeclared AI use, will be treated as a **plagiarism case** and handled according to KFUPM regulations.
- Every member must be able to explain the code they committed, including AI-assisted code.

## Grading Rubric:
> The AI Usage Declaration is a mandatory requirement. Without it, the grade for this milestone is **0**, regardless of the rubric below.

The submission will be graded out of 100 points, divided as follows:

| **Criteria (Points)** | **Excellent (90-100%)** | **Very Good (80-89%)** | **Good (70-79%)** | **Acceptable (60-69%)** | **Poor (0-59%)** |
|-----------------------|-------------------------|------------------------|-------------------|-------------------------|------------------|
| **Proper use of Node.js and Express.js (20)** | Node.js and Express.js are used efficiently, with well-structured routes and middleware implemented. | Node.js and Express.js are used effectively, but there are minor inefficiencies in structure. | Node.js and Express.js are used, but the implementation lacks modularity or clarity. | Node.js and Express.js are used minimally, with significant structural issues. | Improper or missing use of Node.js and Express.js. |
| **Functional and Tested APIs (20)** | All APIs are functional, thoroughly tested, and cover all necessary use cases. | Most APIs are functional and tested, with minor gaps in coverage or functionality. | APIs are functional, but testing is incomplete, or some endpoints have issues. | Few APIs are functional, with limited testing and significant gaps in use cases. | APIs are non-functional or not implemented. |
| **Integration with MongoDB (20)** | Full integration with MongoDB, including proper schema design and efficient queries. | Integration with MongoDB is functional, with minor issues in schema design or queries. | MongoDB integration is partially functional, with noticeable inefficiencies or missing features. | MongoDB integration is minimal, with significant issues in schema design or queries. | MongoDB integration is absent or non-functional. |
| **Modular and Clean Code (10)** | Code is modular, well-organized, and adheres to industry best practices. | Code is mostly modular and organized, with minor issues in best practices. | Code has some modularity, but structure or organization needs improvement. | Code lacks modularity, with disorganized structure and minimal adherence to best practices. | Code is poorly organized, with no modularity or adherence to best practices. |
| **Error Handling and Input Validation (15)** | Comprehensive error handling and input validation are implemented and tested thoroughly. | Most errors are handled, and input validation is implemented, with minor gaps. | Basic error handling and input validation are implemented, but significant gaps exist. | Minimal error handling or input validation is implemented. | Error handling and input validation are missing or inadequate. |
| **README and API Documentation (15)** | README.md is detailed, including setup instructions, API documentation, and examples. | README.md is clear and includes setup instructions and API documentation, with minor gaps. | README.md exists but is incomplete or unclear in sections such as API documentation or setup. | README.md is minimal, with insufficient or unclear documentation. | README.md is missing or unhelpful. |
