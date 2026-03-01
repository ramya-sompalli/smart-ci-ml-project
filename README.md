#  Smart CI/CD Pipeline with ML-Driven Failure Prediction

An intelligent CI/CD pipeline using GitHub Actions, integrated with a Machine Learning model that predicts commit failure probability — optimizing build time and improving efficiency while ensuring reliability.

##  Project Overview

Instead of running the full test suite for every commit, this pipeline uses ML logic to decide whether to run all tests or skip heavy tests based on predicted risk level.


##  Problem Statement

Traditional CI/CD pipelines run the entire build and test process for every code change, regardless of risk level. This leads to:

-  Increased execution time
-  Higher compute and infrastructure usage
-  Slower feedback to developers

To solve this, we implemented a pipeline that integrates an ML prediction service to classify commit risk and conditionally execute testing.

##  Proposed Solution

An ML prediction API is integrated inside the CI workflow to determine commit risk.

### Conditional Execution Logic

| Condition | Action |
|---|---|
| Failure probability **> 0.6** | Run full test suite |
| Failure probability **≤ 0.6** | Skip heavy tests |
| ML API fails | Full tests run (fallback) |

This ensures optimized execution while preventing false negatives.

##  DevOps Implementation

###  CI Trigger
- The pipeline triggers automatically on every `push` to the `main` branch
- A scheduled **weekly full pipeline run** is configured to prevent model drift

###  ML Integration & Conditional Pipeline Logic

1. GitHub Actions is triggered on push to `main`
2. ML Prediction API returns failure probability
3. Probability is extracted inside the workflow
4. Conditional logic decides which steps to run

###  Execution Time Monitoring

Execution time is measured by capturing timestamps at the start and end of the workflow — helping demonstrate time saved with ML-driven decisions.

###  Fallback Safety Mechanism

If the ML API fails or responds incorrectly:
- Pipeline defaults to executing the **full test suite**
- Ensures reliability and correctness at all times

##  Workflow Architecture
```
Developer Push
      ↓
GitHub Actions Trigger
      ↓
ML Prediction API Call
      ↓
Evaluate Failure Probability
      ↓
Conditional Execution of Tests
      ↓
Execution Time Logging
```

##  Technologies Used

| Component | Technology |
|---|---|
| CI/CD | GitHub Actions |
| Workflow Config | YAML |
| Scripting | Bash |
| JSON Parsing | jq |
| Runtime | Python |

##  DevOps Contribution

As the DevOps Engineer for this project, I was responsible for:

- Designing and implementing the GitHub Actions CI/CD pipeline
- Integrating the ML prediction service into the CI workflow
- Implementing threshold-based conditional test execution logic
- Adding execution time monitoring
- Implementing fallback logic for safety
- Configuring scheduled full pipeline runs

##  Key Features

-  ML-driven decision logic inside CI
-  Execution time comparison
-  Conditional test execution
-  Fallback safety mechanism
-  Scheduled periodic full run

##  Outcome

-  Reduced execution time
-  Optimized resource usage
-  Faster feedback to developers
-  Maintained pipeline reliability
-  Demonstrated real integration of ML with DevOps

##  Project Structure
```
smart-ci-ml-project/
├── .github/
│   └── workflows/
│       └── smart-ci.yml       # GitHub Actions CI workflow
├── smart-ci.yml               # CI configuration / pipeline definition
└── README.md
```

##  Author

**Ramya Sompalli**  
[GitHub](https://github.com/ramya-sompalli)
