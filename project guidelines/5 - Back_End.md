# Milestone 5️⃣ Back-End Implementation

## 🎯 Objective:
Develop the back-end of your web application using Node.js and Express.js. Integrate a MongoDB database to manage your application data. This milestone focuses on building and implementing the server-side logic, database interactions, and APIs required for your application.

## 🥋 Instructions:

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
- Use the same GitHub repository created for the project.
  - Push all back-end code to the repository.
  - Ensure proper folder structure. Actually there is no the correct folder structure for every NodeJS project because every project has their own characteristic. But please consider these references to structuring your files:
      - [Reference 1](https://mr-alien.medium.com/folder-structure-for-nodejs-expressjs-project-56be9ec35548)
      - [Reference 2](https://blog.logrocket.com/organizing-express-js-project-structure-better-productivity/)
      - [Reference 3](https://www.geeksforgeeks.org/folder-structure-for-a-node-js-project/)
      - [Reference 4](https://medium.com/@ibrahimhz/my-node-js-express-js-project-folder-structure-for-maintainability-and-scalability-2c578eb863f2)
      - [Reference 5](https://dev.to/nermine-slimane/how-to-structure-your-express-and-nodejs-project-3bl)
  - Structuring your files is benefiting you when you are working on large group and real-world project.
  - Update the README.md to include:
    - Instructions for running the back-end server.
    - Details about the environment variables required for the database connection or other configurations.
    - API documentation (routes, methods, request/response structure).

### 4. Integration:
- Ensure your back-end APIs can communicate effectively with the front-end prototype developed in Milestone 4.
- Test all API endpoints using tools like **[Postman](https://www.postman.com/downloads/) or cURL** before integrating them with the front end. To get to know quickly about Postman and cURL, kindly check the tutorial [here Postman](https://www.geeksforgeeks.org/postman-tutorial/) and [here (cURL)](https://www.geeksforgeeks.org/using-curl-to-make-rest-api-requests/).

### 5. Submission Guidelines:
- Push all code changes to the GitHub repository created for your project.
- Update the README.md file with:
  - Clear instructions for setting up and running the back-end.
  - API documentation, including example requests and responses.
- Submit the GitHub repository link via Blackboard under the designated assignment.

### 6. Notes:
- Follow best practices for version control:
  - Make regular commits with clear commit messages.
  - Avoid pushing sensitive information (e.g., API keys, database credentials) to the repository.
  - Use `.gitignore` to exclude unnecessary files like `node_modules` and sensitive configuration files.
- Contributions will be monitored via GitHub, so ensure all team members participate actively in coding. We can see the contributors from the Github's commit histories.

## 📊 Grading Rubric:
The submission will be graded out of 100 points, divided as follows:

| **Criteria (Points)** | **Excellent (90-100%)** | **Very Good (80-89%)** | **Good (70-79%)** | **Acceptable (60-69%)** | **Poor (0-59%)** |
|-----------------------|-------------------------|------------------------|-------------------|-------------------------|------------------|
| **Proper use of Node.js and Express.js (20)** | Node.js and Express.js are used efficiently, with well-structured routes and middleware implemented. | Node.js and Express.js are used effectively, but there are minor inefficiencies in structure. | Node.js and Express.js are used, but the implementation lacks modularity or clarity. | Node.js and Express.js are used minimally, with significant structural issues. | Improper or missing use of Node.js and Express.js. |
| **Functional and Tested APIs (20)** | All APIs are functional, thoroughly tested, and cover all necessary use cases. | Most APIs are functional and tested, with minor gaps in coverage or functionality. | APIs are functional, but testing is incomplete, or some endpoints have issues. | Few APIs are functional, with limited testing and significant gaps in use cases. | APIs are non-functional or not implemented. |
| **Integration with MongoDB (20)** | Full integration with MongoDB, including proper schema design and efficient queries. | Integration with MongoDB is functional, with minor issues in schema design or queries. | MongoDB integration is partially functional, with noticeable inefficiencies or missing features. | MongoDB integration is minimal, with significant issues in schema design or queries. | MongoDB integration is absent or non-functional. |
| **Modular and Clean Code (10)** | Code is modular, well-organized, and adheres to industry best practices. | Code is mostly modular and organized, with minor issues in best practices. | Code has some modularity, but structure or organization needs improvement. | Code lacks modularity, with disorganized structure and minimal adherence to best practices. | Code is poorly organized, with no modularity or adherence to best practices. |
| **Error Handling and Input Validation (15)** | Comprehensive error handling and input validation are implemented and tested thoroughly. | Most errors are handled, and input validation is implemented, with minor gaps. | Basic error handling and input validation are implemented, but significant gaps exist. | Minimal error handling or input validation is implemented. | Error handling and input validation are missing or inadequate. |
| **README and API Documentation (15)** | README.md is detailed, including setup instructions, API documentation, and examples. | README.md is clear and includes setup instructions and API documentation, with minor gaps. | README.md exists but is incomplete or unclear in sections such as API documentation or setup. | README.md is minimal, with insufficient or unclear documentation. | README.md is missing or unhelpful. |
