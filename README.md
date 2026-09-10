# 📚 Library Management API — Postman + Newman + CI/CD

![Postman](https://img.shields.io/badge/Postman-API%20Testing-orange)
![Newman](https://img.shields.io/badge/Newman-Automation-brightgreen)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-blue)
![JSON Server](https://img.shields.io/badge/JSON%20Server-REST%20API-lightgrey)

## 📌 Project Overview

This project is a practical **API Testing project** built around a Library Management API.

The objective was not only to send API requests with Postman, but to build a complete testing workflow covering:

**API Test Design → Postman → Assertions → Test Data → Newman → GitHub Actions → CI/CD**

The project demonstrates how API tests can be designed, validated and then executed automatically in a Continuous Integration pipeline.

The initial API testing work was performed with **Postman**, while **Newman** is used as the command-line test runner for automation and CI/CD integration.

---

# 🎯 Project Objectives

The main objectives of this project are to demonstrate the ability to:

- analyse an API and identify test scenarios;
- design positive and negative API tests;
- validate HTTP responses;
- validate response body content;
- validate business rules;
- validate data consistency between API resources;
- use dynamic test data;
- use Postman variables and environments;
- write automated assertions with Postman scripts;
- execute Postman collections with Newman;
- integrate API tests into a CI/CD pipeline;
- analyse automated test results;
- detect regressions automatically.

The project therefore goes beyond basic Postman usage and demonstrates an end-to-end **API QA automation workflow**.

---

# 🏗️ Project Architecture

```text
                         ┌──────────────────────────┐
                         │   Library Management API  │
                         │                          │
                         │       JSON Server        │
                         │       Port: 3000         │
                         └─────────────┬────────────┘
                                       │
                                       │ REST API
                                       ▼
                         ┌──────────────────────────┐
                         │         Postman          │
                         │                          │
                         │  API Requests            │
                         │  Test Scenarios          │
                         │  Assertions              │
                         │  Test Scripts            │
                         │  Environment Variables   │
                         └─────────────┬────────────┘
                                       │
                                       │ Collection
                                       ▼
                         ┌──────────────────────────┐
                         │          Newman          │
                         │                          │
                         │ Command-line execution   │
                         │ Automated API testing    │
                         └─────────────┬────────────┘
                                       │
                                       ▼
                         ┌──────────────────────────┐
                         │      GitHub Actions      │
                         │                          │
                         │       CI Pipeline        │
                         │                          │
                         │ Install → Start API →    │
                         │ Run Newman → Report      │
                         └──────────────────────────┘
```

---

# 📁 Project Structure

The GitHub repository is intended to evolve toward the following structure:

```text
Library-Management-API/
│
├── README.md
│
├── postman/
│   ├── collections/
│   │   └── Library_Management.postman_collection.json
│   │
│   └── environments/
│       └── Library_Management.postman_environment.json
│
├── test-data/
│   └── db.json
│
├── documentation/
│   ├── test-strategy.md
│   ├── test-design.md
│   ├── test-cases.md
│   └── api-test-report.md
│
├── scripts/
│   └── start-server.sh
│
└── .github/
    └── workflows/
        └── postman-api-tests.yml
```

---

# ⚙️ Automation with Newman

Postman is excellent for designing and executing API tests interactively.

For CI/CD, the collection can be executed using **Newman**, the command-line collection runner for Postman.

The target workflow is:

```text
Postman Collection
        │
        ▼
      Newman
        │
        ▼
Automated API Tests
        │
        ▼
   Test Results
```

Example command:

```bash
newman run postman/collections/Library_Management.postman_collection.json \
  -e postman/environments/Library_Management.postman_environment.json
```

Newman allows the same collection developed in Postman to be executed automatically without opening the Postman application.

---

# 🚀 CI/CD with GitHub Actions

The next stage of the project is to integrate Newman into **GitHub Actions**.

The target CI pipeline is:

```text
Developer Push
      │
      ▼
GitHub Repository
      │
      ▼
GitHub Actions
      │
      ├── Checkout repository
      │
      ├── Install Node.js
      │
      ├── Install JSON Server
      │
      ├── Start API
      │
      ├── Install Newman
      │
      ├── Execute Postman Collection
      │
      ├── Generate Test Report
      │
      └── Publish Result
      │
      ▼
   PASS / FAIL
```

The objective is to make API testing part of the development lifecycle rather than an activity performed only manually.

---

# 🔁 CI/CD Quality Gate

The automated test execution can act as a quality gate.

```text
Code / API Change
       │
       ▼
GitHub Actions
       │
       ▼
API Tests
       │
   ┌───┴────┐
   │        │
  PASS     FAIL
   │        │
   ▼        ▼
 Continue   Investigation
 pipeline   required
```

A failing API test should therefore provide immediate feedback that a regression or another problem may have been introduced.

---

# 📊 Test Reporting

The CI/CD implementation will generate automated execution results.

The objective is to make the pipeline provide:

- number of executed tests;
- passed tests;
- failed tests;
- execution duration;
- failure details;
- test reports available as CI artifacts.

The report will support the QA investigation rather than replacing it.

---

# 🐞 Defect and Regression Detection

An important objective of the CI integration is **early regression detection**.

For example:

```text
API Change
    │
    ▼
GitHub Actions
    │
    ▼
Newman
    │
    ▼
Existing API Tests
    │
    ├── PASS → No regression detected
    │
    └── FAIL → QA investigation
```

A failed automated test does not automatically mean that the application contains a defect.

The QA analysis must determine whether the failure is caused by:

- an application defect;
- an API contract change;
- incorrect test data;
- an environment problem;
- a test script problem;
- an obsolete expectation.

