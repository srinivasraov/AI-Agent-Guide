# AI Specification Templates Reference

Quick templates for writing specifications that AI coding agents can implement effectively.

## How to Use This Guide

### What Are Specifications?
Specifications are detailed instructions that tell AI coding agents exactly what to build. Think of them as blueprints that an AI can follow to generate consistent, high-quality code.

### When to Use Each Template

| Situation | Use This Template | Save As |
|-----------|------------------|----------|
| Planning a new feature | Technical Design | `.ai-context/specifications/SPEC-001-feature-name.md` |
| Ready to code a feature | Feature Implementation | `.ai-context/specifications/SPEC-002-feature-name.md` |
| Fixing a bug | Bug Fix | `.ai-context/specifications/BUG-001-issue-name.md` |
| Improving existing code | Refactoring | `.ai-context/specifications/REFACTOR-001-component.md` |
| Setting up tests | Testing Strategy | `.ai-context/specifications/TEST-001-feature.md` |
| Automating deployment | CI/CD Pipeline | `.ai-context/specifications/PIPELINE-001-service.md` |

### Step-by-Step Process

1. **Choose the Right Template**
   - Pick based on what you're trying to accomplish
   - Don't worry about getting it perfect the first time

2. **Fill Out the Template**
   - Replace all `[placeholders]` with your specific details
   - Remove sections that don't apply
   - Add sections if needed

3. **Save in the Right Place**
   ```
   your-project/
   └── .ai-context/
       └── specifications/
           ├── SPEC-001-user-auth.md
           ├── SPEC-002-payment.md
           └── BUG-001-login-timeout.md
   ```

4. **Reference in Your AI Tool**
   
   **For Cursor:**
   ```
   "Implement the user authentication feature according to SPEC-001-user-auth.md"
   ```
   
   **For Claude Code:**
   ```
   "Read .ai-context/specifications/SPEC-001-user-auth.md and implement it"
   ```

### Pro Tips

- **Start Simple**: Your first spec doesn't need every section. Add detail as you learn what works.
- **Be Specific**: Instead of "validate input", write "validate email format using regex pattern"
- **Include Examples**: AI understands much better with concrete examples
- **Version Control**: Treat specs like code - commit them, review them, update them

### Example: From Idea to Implementation

Let's say you need a user registration feature:

1. **Start with Technical Design** template to plan the architecture
2. **Create Feature Implementation** spec with specific requirements
3. **Reference in AI**: "Implement user registration from SPEC-003-user-registration.md"
4. **AI generates**: Complete implementation following your specifications
5. **Update spec** if implementation revealed missing details

---

## Table of Contents
1. [Technical Design Template](#technical-design)
2. [Feature Implementation Template](#feature-implementation)
3. [Bug Fix Template](#bug-fix)
4. [Refactoring Template](#refactoring)
5. [Testing Strategy Template](#testing)
6. [CI/CD Pipeline Template](#cicd)

---

## Technical Design Template {#technical-design}

Copy this template into a new file:

```
# SPEC-[NUMBER]: [Feature Name] Technical Design

## Overview
**Problem**: [What needs solving]
**Solution**: [High-level approach]
**Impact**: [Who benefits and how]

## API Design
endpoint: /api/v1/[resource]
method: POST
request:
  type: object
  properties:
    name: 
      type: string
      minLength: 3
      maxLength: 100
response:
  201:
    schema:
      id: string
      name: string
  400:
    schema:
      error: string

## Data Model
CREATE TABLE [table_name] (
    id UUID PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);

## Business Logic
1. Validate input
2. Check permissions
3. Process data
4. Store in database
5. Return response

## Acceptance Criteria
- [ ] API endpoint works as specified
- [ ] Data validates correctly
- [ ] Errors handled gracefully
- [ ] Tests pass
- [ ] Documentation updated
```

---

## Feature Implementation Template {#feature-implementation}

Copy this template into a new file:

```
# SPEC-[NUMBER]: [Feature Name]

## User Story
As a [user type]
I want to [action]
So that [benefit]

## Requirements

### Must Have (MVP)
- [ ] [Core feature 1]
- [ ] [Core feature 2]
- [ ] [Core feature 3]

### Nice to Have
- [ ] [Enhancement 1]
- [ ] [Enhancement 2]

## Technical Implementation

### Frontend
- Component: [ComponentName]
- State management: [approach]
- API calls: [endpoints to use]

### Backend
- Service: [ServiceName]
- Database changes: [if any]
- API endpoints: [list]

### Testing
- Unit tests for [components]
- Integration tests for [flows]
- E2E test for [user journey]

## Success Metrics
- [Metric 1]: [target]
- [Metric 2]: [target]
```

---

## Bug Fix Template {#bug-fix}

Copy this template into a new file:

```
# BUG-[NUMBER]: [Title]

## Problem
**What's happening**: [Current behavior]
**What should happen**: [Expected behavior]
**Impact**: [Who's affected]

## Root Cause
[Why this is happening]

## Fix Approach
[How to fix it]

## Test Plan
1. Verify bug exists
2. Apply fix
3. Verify bug is fixed
4. Check for regressions

## Prevention
[How to prevent similar issues]
```

---

## Refactoring Template {#refactoring}

Copy this template into a new file:

```
# REFACTOR-[NUMBER]: [Component Name]

## Goals
1. [Improvement 1]
2. [Improvement 2]

## Current Issues
- [Problem 1]
- [Problem 2]

## Proposed Changes
1. [Change 1]
2. [Change 2]

## What Stays the Same
- Public API
- Business logic
- Database schema

## Migration Plan
1. [Step 1]
2. [Step 2]

## Success Criteria
- [ ] All tests pass
- [ ] Performance improved by X%
- [ ] Code complexity reduced
```

---

## Testing Strategy Template {#testing}

Copy this template into a new file:

```
# TEST-SPEC-[NUMBER]: [Feature] Testing

## Test Pyramid
- Unit Tests: 70%
- Integration Tests: 20%
- E2E Tests: 10%

## Unit Tests
describe('ComponentName', () => {
  it('should handle happy path', () => {
    // Test implementation
  });
  
  it('should handle error case', () => {
    // Test implementation
  });
});

## Integration Tests
- API endpoint testing
- Database interaction
- Service communication

## E2E Tests
Feature: User Profile
  Scenario: Update profile
    Given I am logged in
    When I update my email
    Then I should see success message
    And email should be updated

## Performance Tests
- Load: 1000 concurrent users
- Response time: <200ms p95
- Throughput: 100 req/sec
```

---

## CI/CD Pipeline Template {#cicd}

Copy this template into a new file:

```
# PIPELINE-SPEC-[NUMBER]: [Service Name]

## Pipeline Stages

### 1. Build
- Checkout code
- Install dependencies
- Compile/build
- Run linters

### 2. Test
- Unit tests
- Integration tests
- Security scan
- Coverage report

### 3. Deploy
- Build Docker image
- Push to registry
- Deploy to staging
- Run smoke tests
- Deploy to production

## Configuration
name: CI/CD Pipeline
on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: npm install
      - run: npm run build
      - run: npm test

## Success Criteria
- Build time: <5 minutes
- Zero-downtime deployment
- Automatic rollback capability
```

---

## Usage Tips

1. **Start simple** - Don't over-specify initially
2. **Include examples** - AI understands better with examples
3. **Be explicit** - State assumptions clearly
4. **Test incrementally** - Specify testing approach
5. **Version control** - Treat specs like code

Remember: Good specifications lead to good implementations. Invest time in clarity upfront to save time debugging later.
