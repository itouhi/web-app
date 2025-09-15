# Tasks: [FEATURE NAME]

**Input**: Design documents from `/specs/[###-feature-name]/`
**Prerequisites**: plan.md (required), research.md, data-model.md, contracts/

## Execution Flow (main)
```
1. Load plan.md from feature directory
   → If not found: ERROR "No implementation plan found"
   → Extract: tech stack, libraries, structure
2. Load optional design documents:
   → data-model.md: Extract entities → model tasks
   → contracts/: Each file → contract test task
   → research.md: Extract decisions → setup tasks
3. Generate tasks by category:
   → Setup: project init, dependencies, linting
   → Tests: contract tests, integration tests
   → Core: models, services, CLI commands
   → Integration: DB, middleware, logging
   → Polish: unit tests, performance, docs
4. Apply task rules:
   → Different files = mark [P] for parallel
   → Same file = sequential (no [P])
   → Tests before implementation (TDD)
5. Number tasks sequentially (T001, T002...)
6. Generate dependency graph
7. Create parallel execution examples
8. Validate task completeness:
   → All contracts have tests?
   → All entities have models?
   → All endpoints implemented?
9. Return: SUCCESS (tasks ready for execution)
```

## Format: `[ID] [P?] Description`
- **[P]**: Can run in parallel (different files, no dependencies)
- Include exact file paths in descriptions

## Path Conventions - Full-Stack Structure
- **Frontend**: `frontend/src/`, `frontend/components/`, `frontend/pages/`
- **Backend Node.js**: `backend/node/src/`, `backend/node/routes/`
- **Backend Python**: `backend/python/src/`, `backend/python/api/`
- **Shared**: `shared/types/`, `shared/schemas/`, `shared/utils/`
- **Tests**: `frontend/tests/`, `backend/tests/`, `e2e/tests/`
- **Configs**: `configs/`, `docker/`, `.github/workflows/`
- **Docs**: `docs/api/`, `docs/deployment/`, `docs/architecture/`

## Phase 3.1: Full-Stack Setup
- [ ] T001 Create full-stack project structure (frontend/, backend/, shared/)
- [ ] T002 [P] Initialize frontend project with TypeScript + framework
- [ ] T003 [P] Initialize backend Node.js project with TypeScript
- [ ] T004 [P] Initialize backend Python project with FastAPI/Flask
- [ ] T005 [P] Configure shared type definitions and schemas
- [ ] T006 [P] Set up Docker containers for development environment
- [ ] T007 [P] Configure linting (ESLint, Black, Flake8) and formatting (Prettier, Black)
- [ ] T008 Configure VS Code workspace settings for multi-language development
- [ ] T009 Set up GitHub Actions for CI/CD pipeline

## Phase 3.2: Tests First (TDD) ⚠️ MUST COMPLETE BEFORE 3.3
**CRITICAL: These tests MUST be written and MUST FAIL before ANY implementation**
- [ ] T010 [P] Frontend component tests (React Testing Library)
- [ ] T011 [P] Backend API contract tests (OpenAPI validation)
- [ ] T012 [P] Database integration tests (actual DB connection)
- [ ] T013 [P] Authentication flow tests (JWT, session management)
- [ ] T014 [P] Cross-service integration tests (Node.js ↔ Python)
- [ ] T015 [P] E2E user journey tests (Playwright)

## Phase 3.3: Core Implementation (ONLY after tests are failing)
### Frontend Development
- [ ] T016 [P] UI components implementation (TypeScript + React)
- [ ] T017 [P] State management setup (Redux/Zustand)
- [ ] T018 [P] API client with TypeScript types
- [ ] T019 [P] Form validation and error handling
- [ ] T020 [P] Responsive design implementation

### Backend Node.js Development  
- [ ] T021 [P] Express.js API routes setup
- [ ] T022 [P] Authentication middleware
- [ ] T023 [P] Request validation and sanitization
- [ ] T024 [P] Database models (Prisma/TypeORM)

### Backend Python Development
- [ ] T025 [P] FastAPI endpoints implementation
- [ ] T026 [P] Data processing logic
- [ ] T027 [P] Database operations (SQLAlchemy)
- [ ] T028 [P] Background task processing

### Cross-Language Integration
- [ ] T029 Shared API contracts and schemas
- [ ] T030 Inter-service communication setup
- [ ] T031 Data consistency validation

## Phase 3.4: Full-Stack Integration
- [ ] T032 Frontend ↔ Backend API integration
- [ ] T033 Authentication flow end-to-end
- [ ] T034 Error handling across all layers
- [ ] T035 Logging and monitoring setup
- [ ] T036 Database migration and seeding
- [ ] T037 Docker containerization and orchestration

## Phase 3.5: Quality & Performance
- [ ] T038 [P] Unit test coverage (frontend components)
- [ ] T039 [P] Unit test coverage (backend services)  
- [ ] T040 [P] Performance optimization and testing
- [ ] T041 [P] Security audit and penetration testing
- [ ] T042 [P] Accessibility compliance (WCAG 2.1)
- [ ] T043 [P] Browser compatibility testing
- [ ] T044 [P] API documentation generation
- [ ] T045 Code quality analysis and refactoring

## Dependencies - Full-Stack Context
- **Phase 3.2** (Tests) before **Phase 3.3** (Implementation)
- **Frontend tests** (T010) before **UI components** (T016)
- **Backend tests** (T011-T014) before **API implementation** (T021-T028)
- **Integration tests** (T014) before **Cross-service setup** (T029-T031)
- **Core implementation** before **Integration** (T032-T037)
- **Integration** before **Quality & Performance** (T038-T045)

## Parallel Execution Examples
```bash
# Phase 3.2: All test development in parallel
$ npm run test:frontend & pytest backend/tests/ & npm run test:e2e

# Phase 3.3: Language-specific development
$ npm run dev:frontend & npm run dev:backend & python -m uvicorn backend.python.main:app

# Phase 3.5: Quality assurance
$ npm run lint & python -m black . & npm run test:coverage
```

## Notes
- [P] tasks = different files, no dependencies
- Verify tests fail before implementing
- Commit after each task
- Avoid: vague tasks, same file conflicts

## Task Generation Rules
*Applied during main() execution*

1. **From Contracts**:
   - Each contract file → contract test task [P]
   - Each endpoint → implementation task
   
2. **From Data Model**:
   - Each entity → model creation task [P]
   - Relationships → service layer tasks
   
3. **From User Stories**:
   - Each story → integration test [P]
   - Quickstart scenarios → validation tasks

4. **Ordering**:
   - Setup → Tests → Models → Services → Endpoints → Polish
   - Dependencies block parallel execution

## Validation Checklist
*GATE: Checked by main() before returning*

- [ ] All contracts have corresponding tests
- [ ] All entities have model tasks
- [ ] All tests come before implementation
- [ ] Parallel tasks truly independent
- [ ] Each task specifies exact file path
- [ ] No task modifies same file as another [P] task