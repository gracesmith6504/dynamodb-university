# DynamoDB University

An interactive learning platform for mastering Amazon DynamoDB, built in collaboration with **Amazon Development Centre Ireland**.

Industry Mentors: Deepesh Shetty & Pano Petridis (Amazon)

> **Note:** Source code is held in a private institutional GitLab repository. This repo contains project documentation only.

---

## What It Does

DynamoDB University helps developers learn NoSQL data modelling through hands-on practice. The platform guides users through structured courses on DynamoDB concepts - from table design and primary keys to Global Secondary Indexes and access patterns - using a live DynamoDB MCP (Model Context Protocol) server for real-time validation and an LLM agent for contextual feedback.

Users configure their preferred LLM (Claude Desktop, Amazon Q, or another MCP-compatible agent), which is automatically connected to a local DynamoDB instance. They then work through exercises, interact with their LLM to design and validate data models, and answer MCQ questions to confirm their understanding before progressing.

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | Next.js, TypeScript, Tailwind CSS, MDX |
| **Auth** | Amazon Cognito via AWS Amplify |
| **Database** | Amazon DynamoDB (single-table design) |
| **MCP Integration** | DynamoDB MCP Server (AWS Labs), stdio transport |
| **IAM** | AWS IAM roles with temporary credentials |
| **Testing** | Jest (unit), Playwright (E2E) |
| **CI/CD** | GitLab CI (build, jest-test, playwright-test) |
| **Deployment** | Local (DynamoDB MCP server does not currently support remote hosting) |

---

## My Contributions

I was a **Backend Developer** on an 8-person agile team across 4 sprints (Jan-Apr 2026).

- Built `startCourse`, `startExercise`, `completeCourse`, and `completeExercise` API functions backed by DynamoDB
- Migrated all four functions to session-based authentication using `createDBClient`
- Applied TypeScript types from the shared `lib/types.ts` for type safety across the backend
- Authored the **Pagination exercise** - a full MDX content file covering DynamoDB pagination, `LastEvaluatedKey`, and best practices with a practical e-commerce example
- Created lab content for the data model validation lab
- Tested all API functions end-to-end ahead of the final client demo

---

## Architecture

The app runs entirely locally. Next.js server functions interact directly with DynamoDB via the AWS SDK, without an API Gateway or Lambda layer, keeping the architecture simple and type-safe. Amazon Cognito handles authentication via AWS Amplify, and IAM roles issue temporary credentials per session to secure DynamoDB access.

The MCP layer runs as a local stdio process. When a user configures their LLM on the setup page, the app automatically installs the DynamoDB MCP server library and writes the correct config file for their chosen agent.

---

## Key Design Decisions

- **Single-table DynamoDB design** - user progress (courses and exercises) is nested directly in the user item, avoiding extra tables and reducing query complexity
- **MDX for course content** - exercises are written in markdown with embedded components, making content easy to update without modifying Next.js page logic
- **Local-first architecture** - the MCP server runs locally via stdio, letting users experiment without cloud costs or production risk
- **Session-based auth** - temporary IAM credentials are issued per session rather than using static keys, following AWS security best practices

---

## Team

8-person agile team from Trinity College Dublin across 4 two-week sprints, with bi-weekly scrum meetings and sprint reviews with Amazon mentors.

> Source code is held in a private institutional GitLab repository. Available for discussion at interview.

---

## Demo

*Video demo coming soon.*
