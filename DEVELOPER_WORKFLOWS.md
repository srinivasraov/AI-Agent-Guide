# Developer Workflow Sequences: Using AI Coding Agents

This document shows detailed step-by-step workflows for using Cursor and Claude Code with the setup from the main guide and specification templates.

## Table of Contents
1. [Overview: How Context Loading Works](#overview)
2. [Technical Design Workflow](#technical-design)
3. [Feature Implementation Workflow](#feature-implementation)
4. [Bug Fix Workflow](#bug-fix)
5. [Refactoring Workflow](#refactoring)
6. [Testing Strategy Workflow](#testing)
7. [CI/CD Pipeline Workflow](#cicd)

---

## Overview: How Context Loading Works {#overview}

### Cursor Context Loading
- ✅ **Automatic**: `.cursor/rules/always.md` loads on every interaction
- ❌ **Manual**: Specifications must be explicitly referenced
- ❌ **Manual**: Memory bank must be explicitly mentioned or included in rules

### Claude Code Context Loading
- ✅ **Automatic**: `CLAUDE.md` loads when Claude Code starts
- ✅ **Automatic**: Can search project structure
- ❌ **Manual**: Specifications must be explicitly mentioned
- ❌ **Manual**: Memory bank must be explicitly referenced

---

## Technical Design Workflow {#technical-design}

### Detailed Cursor Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Cursor as Cursor AI
    participant Rules as .cursor/rules/
    participant Memory as memory-bank/
    participant Arch as .ai-context/architecture/
    participant Specs as .ai-context/specifications/
    
    Dev->>Cursor: "Design a payment processing system"
    Note over Cursor: always.md loads automatically
    Cursor->>Rules: Load always.md
    Rules-->>Cursor: "Check specs first, use memory bank"
    
    Dev->>Cursor: "Use planning mode"
    Cursor->>Rules: Load planning-mode.md
    Rules-->>Cursor: Planning process activated
    
    Cursor->>Dev: "Let me ask some questions:<br/>1. Payment methods needed?<br/>2. Currency support?<br/>3. Compliance requirements?"
    
    Dev->>Cursor: "Credit cards, USD only, PCI compliance"
    
    Cursor->>Memory: Read project/overview.md
    Memory-->>Cursor: Tech stack, constraints
    
    Cursor->>Arch: Read existing patterns
    Arch-->>Cursor: Service patterns, API design
    
    Cursor->>Cursor: Generate technical design
    Cursor->>Specs: Create SPEC-001-payments.md
    
    Cursor->>Dev: "Technical design created. Review?"
    Dev->>Cursor: "Looks good, update memory"
    
    Cursor->>Memory: Update architecture/decisions.md
    Cursor->>Memory: Update progress/implementation.md
```

### Detailed Claude Code Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Claude as Claude Code
    participant Config as CLAUDE.md
    participant Specs as .ai-context/specifications/
    participant Memory as memory-bank/
    participant Arch as .ai-context/architecture/
    
    Dev->>Claude: claude (starts Claude Code)
    Claude->>Config: Auto-load CLAUDE.md
    Config-->>Claude: "Always check specs first!"
    
    Dev->>Claude: "Design a payment processing system"
    
    Claude->>Claude: Agentic search activated
    Claude->>Specs: Search for payment specs
    Specs-->>Claude: No existing payment spec
    
    Claude->>Arch: Search architecture patterns
    Arch-->>Claude: Found service patterns
    
    Claude->>Dev: "I'll design a payment system.<br/>Questions:<br/>1. Payment providers?<br/>2. Transaction volume?<br/>3. International support?"
    
    Dev->>Claude: "Stripe, 1000/day, US only"
    
    Claude->>Memory: "Should I check memory bank?"
    Dev->>Claude: "Yes, check memory-bank/"
    Claude->>Memory: Read context
    
    Claude->>Claude: Generate comprehensive design
    Claude->>Specs: Write SPEC-001-payments.md
    
    Claude->>Dev: "Design complete. Should I update memory?"
    Dev->>Claude: "Yes"
    Claude->>Memory: Update relevant files
```

---

## Feature Implementation Workflow {#feature-implementation}

### Detailed Cursor Implementation Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Cursor as Cursor AI
    participant Rules as .cursor/rules/
    participant Spec as .ai-context/specifications/
    participant Code as Source Code
    participant Tests as Test Files
    participant Memory as memory-bank/
    
    Dev->>Cursor: "Implement user auth from SPEC-002-user-auth.md"
    
    Cursor->>Rules: Load always.md
    Rules-->>Cursor: "Always check specs, TDD approach"
    
    Cursor->>Spec: Read SPEC-002-user-auth.md
    Spec-->>Cursor: Full specification loaded
    
    Cursor->>Memory: Check progress/implementation.md
    Memory-->>Cursor: No prior work on auth
    
    Cursor->>Dev: "I'll implement auth per spec. Starting with tests."
    
    Cursor->>Tests: Create auth.test.js
    Cursor->>Dev: "Tests created. Running them..."
    Cursor->>Tests: npm test auth.test.js
    Tests-->>Cursor: Tests failing (expected)
    
    Cursor->>Code: Create AuthController.js
    Cursor->>Code: Create AuthService.js
    Cursor->>Code: Create auth middleware
    
    Cursor->>Tests: Run tests again
    Tests-->>Cursor: All tests passing
    
    Cursor->>Memory: Update implementation.md
    Memory-->>Cursor: Progress saved
    
    Cursor->>Dev: "Auth implementation complete.<br/>- 3 files created<br/>- All tests passing<br/>- Memory updated"
```

### Detailed Claude Code Implementation Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Claude as Claude Code
    participant Config as CLAUDE.md
    participant Spec as .ai-context/specifications/
    participant Code as Source Code
    participant Tests as Test Files
    participant Git as Git/Terminal
    participant Agent1 as Backend Agent
    participant Agent2 as Frontend Agent
    participant Agent3 as Test Agent
    
    Dev->>Claude: "Implement auth from .ai-context/specifications/SPEC-002"
    
    Claude->>Config: Load CLAUDE.md
    Config-->>Claude: "Check specs first!"
    
    Claude->>Spec: Search and read SPEC-002
    Spec-->>Claude: Auth requirements loaded
    
    Claude->>Dev: "Found SPEC-002. I'll implement with sub-agents:<br/>- Backend API<br/>- Frontend components<br/>- Test suite"
    
    Claude->>Agent1: Spawn backend agent
    Claude->>Agent2: Spawn frontend agent
    Claude->>Agent3: Spawn test agent
    
    par Parallel Implementation
        Agent1->>Code: Create auth routes
        Agent1->>Code: Create auth service
        Agent1->>Code: Add JWT logic
    and
        Agent2->>Code: Create LoginForm.jsx
        Agent2->>Code: Create auth context
        Agent2->>Code: Add auth hooks
    and
        Agent3->>Tests: Write unit tests
        Agent3->>Tests: Write integration tests
        Agent3->>Tests: Write E2E tests
    end
    
    Claude->>Git: npm test
    Git-->>Claude: All tests passing
    
    Claude->>Git: git add -A
    Claude->>Git: git commit -m "feat: implement user auth per SPEC-002"
    
    Claude->>Dev: "Auth implemented:<br/>- 8 files created<br/>- 95% test coverage<br/>- Ready for PR"
```

---

## Bug Fix Workflow {#bug-fix}

### Detailed Cursor Bug Fix Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Cursor as Cursor AI
    participant Rules as .cursor/rules/
    participant Memory as memory-bank/
    participant Code as Source Code
    participant Tests as Tests
    participant Spec as Specifications
    
    Note over Dev,Spec: Bug: Login timeout after 5 minutes
    
    Dev->>Cursor: "Fix login timeout bug"
    
    Cursor->>Rules: Load always.md
    Rules-->>Cursor: "Check known issues, write test first"
    
    Cursor->>Memory: Read project/known-issues.md
    Memory-->>Cursor: "Similar: session timeout issues"
    
    Cursor->>Code: Analyze AuthService.js
    Cursor->>Code: Trace token expiry logic
    
    Cursor->>Dev: "Found issue: refresh token not triggered.<br/>Should I write a failing test first?"
    Dev->>Cursor: "Yes"
    
    Cursor->>Tests: Create test_token_refresh_on_expiry()
    Cursor->>Tests: Run test
    Tests-->>Cursor: Test fails (as expected)
    
    Cursor->>Spec: Check SPEC-002-auth.md
    Spec-->>Cursor: Verify expected behavior
    
    Cursor->>Code: Fix TokenService.js
    Note over Code: Add refresh logic
    
    Cursor->>Tests: Run all auth tests
    Tests-->>Cursor: All tests passing
    
    Cursor->>Memory: Update known-issues.md
    Cursor->>Memory: Add to lessons-learned.md
    
    Cursor->>Dev: "Bug fixed:<br/>- Root cause: missing refresh<br/>- Test added<br/>- Memory updated"
```

### Detailed Claude Code Bug Fix Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Claude as Claude Code
    participant Config as CLAUDE.md
    participant Git as Git/Terminal
    participant Code as Source Code
    participant Memory as memory-bank/
    participant Agent as Debug Agent
    
    Note over Dev,Agent: Bug: Login timeout issue
    
    Dev->>Claude: "Debug login timeout issue"
    
    Claude->>Config: Load CLAUDE.md
    Config-->>Claude: Project context loaded
    
    Claude->>Git: git log --grep="auth\|login\|token"
    Git-->>Claude: Recent auth changes found
    
    Claude->>Agent: Spawn debug agent
    Agent->>Code: Search for timeout/expiry logic
    Agent->>Code: Analyze token handling
    Agent-->>Claude: "Found: TokenService.js:45"
    
    Claude->>Dev: "Found potential issue. Check memory-bank/known-issues?"
    Dev->>Claude: "Yes"
    
    Claude->>Memory: Read known-issues.md
    Memory-->>Claude: Previous timeout patterns
    
    Claude->>Dev: "Issue: token refresh missing.<br/>I'll fix with TDD approach."
    
    Claude->>Code: Write failing test
    Claude->>Git: npm test auth/token.test.js
    Git-->>Claude: Test fails (expected)
    
    Claude->>Code: Implement refresh logic
    Claude->>Git: Run full test suite
    Git-->>Claude: All tests pass
    
    Claude->>Memory: Update known-issues.md
    Claude->>Memory: Document fix approach
    
    Claude->>Git: git add -A
    Claude->>Git: git commit -m "fix: add token refresh on expiry"
    
    Claude->>Dev: "Fixed and committed:<br/>- Test proves fix<br/>- No regressions<br/>- PR ready"
```

---

## Refactoring Workflow {#refactoring}

### Detailed Cursor Refactoring Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Cursor as Cursor AI
    participant Rules as .cursor/rules/
    participant Arch as .ai-context/architecture/
    participant Memory as memory-bank/
    participant Code as Source Code
    participant Tests as Tests
    
    Note over Dev,Tests: UserService.java is 1500 lines
    
    Dev->>Cursor: "Refactor UserService for better separation"
    
    Cursor->>Rules: Load always.md
    Rules-->>Cursor: "Check patterns, maintain tests"
    
    Cursor->>Arch: Read service-patterns.md
    Arch-->>Cursor: Repository pattern, service layer
    
    Cursor->>Memory: Check architecture/decisions.md
    Memory-->>Cursor: "Prefer Redis for caching"
    
    Cursor->>Code: Analyze UserService.java
    Cursor->>Cursor: Identify responsibilities
    
    Cursor->>Dev: "I'll split UserService into:<br/>- UserCRUDService<br/>- UserAuthService<br/>- UserProfileService<br/>Continue?"
    Dev->>Cursor: "Yes, show the plan"
    
    Cursor->>Tests: Verify test coverage
    Tests-->>Cursor: "100% coverage confirmed"
    
    loop Incremental Refactoring
        Cursor->>Code: Extract one responsibility
        Cursor->>Tests: Run related tests
        Tests-->>Cursor: Tests still passing
        Cursor->>Dev: "[Component] extracted successfully"
    end
    
    Cursor->>Code: Update all imports
    Cursor->>Tests: Run full test suite
    Tests-->>Cursor: All tests passing
    
    Cursor->>Memory: Update architecture/patterns.md
    Cursor->>Memory: Document new structure
    
    Cursor->>Dev: "Refactoring complete:<br/>- 3 services created<br/>- All tests passing<br/>- Zero breaking changes"
```

### Detailed Claude Code Refactoring Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Claude as Claude Code
    participant Config as CLAUDE.md
    participant Arch as .ai-context/architecture/
    participant Code as Source Code
    participant Agent1 as Analysis Agent
    participant Agent2 as Refactor Agent
    participant Agent3 as Test Agent
    participant Git as Git/Terminal
    
    Note over Dev,Git: UserService needs refactoring
    
    Dev->>Claude: "Refactor UserService for microservices"
    
    Claude->>Config: Load CLAUDE.md
    Config-->>Claude: Architecture guidelines
    
    Claude->>Agent1: Spawn analysis agent
    Agent1->>Code: Deep dive into UserService
    Agent1->>Arch: Read all architecture docs
    Agent1-->>Claude: "Monolithic, 15 responsibilities"
    
    Claude->>Dev: "Current: monolithic service<br/>Target: 3 microservices<br/>Review architecture constraints?"
    Dev->>Claude: "Yes, follow our patterns"
    
    Claude->>Arch: Read microservice-patterns.md
    Arch-->>Claude: Service boundaries, API patterns
    
    Claude->>Agent2: Create refactoring plan
    Claude->>Agent3: Ensure test coverage
    
    Agent2-->>Claude: "Split plan:<br/>- UserCRUD service<br/>- Auth service<br/>- Profile service"
    
    Claude->>Git: git checkout -b refactor/user-service
    
    par Parallel Refactoring
        Agent2->>Code: Extract UserCRUD
        Agent2->>Code: Create interfaces
    and
        Agent2->>Code: Extract AuthService
        Agent2->>Code: Update dependencies
    and
        Agent3->>Git: Run tests continuously
        Agent3-->>Claude: "All passing"
    end
    
    Claude->>Git: Run performance benchmarks
    Git-->>Claude: "40% improvement"
    
    Claude->>Arch: Update service-map.md
    Claude->>Git: git commit -m "refactor: split UserService"
    
    Claude->>Dev: "Refactoring complete:<br/>- 3 services extracted<br/>- Tests passing<br/>- Performance improved 40%"
```

---

## Testing Strategy Workflow {#testing}

### Detailed Cursor Testing Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Cursor as Cursor AI
    participant Rules as .cursor/rules/
    participant Spec as .ai-context/specifications/
    participant Tests as Test Files
    participant Coverage as Coverage Tool
    participant Memory as memory-bank/
    
    Note over Dev,Memory: Payment module needs tests
    
    Dev->>Cursor: "Create comprehensive tests for payments"
    
    Cursor->>Rules: Load always.md
    Rules-->>Cursor: "90% coverage minimum, check patterns"
    
    Cursor->>Coverage: npm test -- --coverage payments
    Coverage-->>Cursor: "Current: 45% coverage"
    
    Cursor->>Spec: Read SPEC-005-payments.md
    Spec-->>Cursor: Business rules, edge cases
    
    Cursor->>Memory: Check project/test-patterns.md
    Memory-->>Cursor: "Use test builders pattern"
    
    Cursor->>Dev: "Current coverage: 45%<br/>I'll create:<br/>- Unit tests (15 cases)<br/>- Integration tests (8 cases)<br/>- E2E tests (3 flows)"
    
    Cursor->>Tests: Create PaymentService.test.js
    Note over Tests: Unit tests with builders
    
    Cursor->>Tests: Create payment.integration.test.js
    Note over Tests: API endpoint tests
    
    Cursor->>Tests: Create payment.e2e.test.js
    Note over Tests: Full user flows
    
    Cursor->>Coverage: Run tests with coverage
    Coverage-->>Cursor: "Coverage: 92%"
    
    Cursor->>Memory: Update test-patterns.md
    Note over Memory: Document new test helpers
    
    Cursor->>Dev: "Testing complete:<br/>- 26 tests added<br/>- 92% coverage<br/>- All edge cases covered"
```

### Detailed Claude Code Testing Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Claude as Claude Code
    participant Config as CLAUDE.md
    participant Spec as .ai-context/specifications/
    participant Code as Source Code
    participant Agent1 as Analysis Agent
    participant Agent2 as Test Agent
    participant Agent3 as Coverage Agent
    participant Terminal as Terminal
    
    Note over Dev,Terminal: Payment service needs tests
    
    Dev->>Claude: "/project:comprehensive-tests payment-service"
    
    Claude->>Config: Load CLAUDE.md
    Config-->>Claude: Testing standards loaded
    
    Claude->>Agent1: Analyze current coverage
    Agent1->>Terminal: npm test -- --coverage
    Terminal-->>Agent1: "45% coverage, gaps identified"
    
    Agent1->>Code: Map untested code paths
    Agent1->>Spec: Extract test scenarios
    Agent1-->>Claude: "Need 47 new tests:<br/>- Unit: 28<br/>- Integration: 12<br/>- E2E: 7"
    
    Claude->>Agent2: Generate comprehensive tests
    Claude->>Agent3: Monitor coverage improvement
    
    par Parallel Test Creation
        Agent2->>Code: Write unit tests
        Agent2->>Spec: Validate against spec
    and
        Agent2->>Code: Write integration tests
        Agent2->>Code: Mock external services
    and
        Agent2->>Code: Write E2E tests
        Agent2->>Code: Full flow validation
    end
    
    Agent3->>Terminal: Run tests incrementally
    Terminal-->>Agent3: "All passing"
    
    Claude->>Terminal: npx stryker run
    Note over Terminal: Mutation testing
    Terminal-->>Claude: "Mutation score: 85%"
    
    Claude->>Code: Add edge case tests
    Claude->>Terminal: Final coverage check
    Terminal-->>Claude: "Coverage: 94%"
    
    Claude->>Dev: "Test suite complete:<br/>- 47 tests added<br/>- 94% coverage<br/>- 85% mutation score<br/>- All specs validated"
```

---

## CI/CD Pipeline Workflow {#cicd}

### Detailed Cursor CI/CD Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Cursor as Cursor AI
    participant Rules as .cursor/rules/
    participant Memory as memory-bank/
    participant Template as .ai-context/templates/
    participant Pipeline as .github/workflows/
    
    Note over Dev,Pipeline: Auth service needs CI/CD
    
    Dev->>Cursor: "Set up CI/CD for auth service"
    
    Cursor->>Rules: Load always.md
    Rules-->>Cursor: "Security scanning required"
    
    Cursor->>Memory: Check project/infrastructure.md
    Memory-->>Cursor: "Using GitHub Actions, AWS deploy"
    
    Cursor->>Template: Load ci-cd-template.yml
    Template-->>Cursor: Standard pipeline structure
    
    Cursor->>Dev: "I'll create a pipeline with:<br/>- Build & test<br/>- Security scan<br/>- Deploy to staging<br/>- Deploy to prod (manual)"
    
    Cursor->>Pipeline: Create auth-service.yml
    
    Cursor->>Pipeline: Add build stage
    Note over Pipeline: Install, build, lint
    
    Cursor->>Pipeline: Add test stage
    Note over Pipeline: Unit, integration tests
    
    Cursor->>Pipeline: Add security stage
    Note over Pipeline: SAST, dependency check
    
    Cursor->>Pipeline: Add deploy stages
    Note over Pipeline: Staging auto, prod manual
    
    Cursor->>Memory: Update infrastructure.md
    Note over Memory: Document pipeline
    
    Cursor->>Dev: "Pipeline created:<br/>- Triggers on PR/push<br/>- Auto-deploy staging<br/>- Manual prod deploy<br/>Need to add secrets manually"
```

### Detailed Claude Code CI/CD Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Claude as Claude Code
    participant Config as CLAUDE.md
    participant Git as Git/Terminal
    participant Agent1 as Pipeline Agent
    participant Agent2 as Security Agent
    participant Agent3 as Deploy Agent
    participant GH as GitHub API
    
    Note over Dev,GH: Need CI/CD for microservices
    
    Dev->>Claude: "Create complete CI/CD for all microservices"
    
    Claude->>Config: Load CLAUDE.md
    Config-->>Claude: Project structure loaded
    
    Claude->>Git: Analyze repository structure
    Git-->>Claude: "5 services detected"
    
    Claude->>Agent1: Design pipeline architecture
    Claude->>Agent2: Add security stages
    Claude->>Agent3: Create deployment strategy
    
    Agent1-->>Claude: "Monorepo strategy:<br/>- Service detection<br/>- Parallel builds<br/>- Shared stages"
    
    Claude->>Git: Create .github/workflows/main.yml
    Note over Git: Master workflow file
    
    par Pipeline Creation
        Agent1->>Git: Add build matrices
        Agent1->>Git: Configure caching
    and
        Agent2->>Git: Add security scans
        Agent2->>Git: Add SAST/DAST
    and
        Agent3->>Git: Add deploy jobs
        Agent3->>Git: Configure environments
    end
    
    Claude->>GH: gh api /repos/{owner}/{repo}/environments
    Claude->>GH: Create staging environment
    Claude->>GH: Create production environment
    
    Claude->>GH: gh secret set AWS_ACCESS_KEY
    Claude->>GH: gh secret set DATABASE_URL
    Note over GH: Secrets configured
    
    Claude->>Git: git add .github/
    Claude->>Git: git commit -m "ci: add multi-service pipeline"
    Claude->>Git: git push
    
    Claude->>Git: gh workflow run main.yml
    Git-->>Claude: "Pipeline running"
    
    Claude->>Dev: "CI/CD complete:<br/>- 5 service pipelines<br/>- Parallel execution<br/>- Secrets configured<br/>- First run in progress"
```

---

## Key Differences Summary

### Context Loading
| Aspect | Cursor | Claude Code |
|--------|--------|-------------|
| Initial Load | Rules (automatic) | CLAUDE.md (automatic) |
| Specifications | Manual reference | Manual reference |
| Memory Bank | Manual or via rules | Manual reference |
| Search | Exact paths needed | Fuzzy search works |

### Working Style
| Aspect | Cursor | Claude Code |
|--------|--------|-------------|
| Approach | Guided, interactive | Autonomous, parallel |
| Confirmation | Asks frequently | Executes more freely |
| Speed | Sequential | Parallel with sub-agents |
| Integration | Code-focused | Full terminal access |

### Best Practices
1. **Cursor**: Ideal for developers who want more control and step-by-step guidance
2. **Claude Code**: Better for experienced developers who want faster, autonomous execution
3. **Both**: Require good specifications and context setup for best results

Remember: The quality of your output depends on the quality of your input specifications and context setup!
