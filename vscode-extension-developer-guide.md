# SpecKit VSCode Extension - Developer Guide

## Welcome, Contributors!

This guide helps you get started developing the SpecKit VSCode extension. Whether you're fixing a bug, adding a feature, or improving documentation, we appreciate your contribution!

---

## Table of Contents

1. [Getting Started](#getting-started)
2. [Development Environment](#development-environment)
3. [Project Structure](#project-structure)
4. [Architecture Overview](#architecture-overview)
5. [Development Workflow](#development-workflow)
6. [Testing](#testing)
7. [Debugging](#debugging)
8. [Contributing Guidelines](#contributing-guidelines)
9. [Common Tasks](#common-tasks)
10. [Troubleshooting](#troubleshooting)

---

## Getting Started

### Prerequisites

- **Node.js**: v18.x or later
- **npm**: v9.x or later
- **VSCode**: v1.85.0 or later
- **Git**: Latest version
- **TypeScript**: v5.2+ (installed via npm)

### Clone and Install

```bash
# Clone the repository
git clone https://github.com/github/spec-kit.git
cd spec-kit/vscode-extension

# Install dependencies
npm install

# Compile TypeScript
npm run compile
```

### First Run

1. Open the project in VSCode:
   ```bash
   code .
   ```

2. Press `F5` to launch the Extension Development Host

3. A new VSCode window opens with the extension loaded

4. Try the command: `Ctrl+Shift+P` → "SpecKit: Initialize Project"

---

## Development Environment

### Recommended VSCode Extensions

Install these extensions for the best development experience:

```json
{
  "recommendations": [
    "dbaeumer.vscode-eslint",
    "esbenp.prettier-vscode",
    "ms-vscode.vscode-typescript-next",
    "orta.vscode-jest",
    "firsttris.vscode-jest-runner"
  ]
}
```

### Editor Settings

Add to `.vscode/settings.json`:

```json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "typescript.tsdk": "node_modules/typescript/lib",
  "typescript.enablePromptUseWorkspaceTsdk": true,
  "jest.autoRun": "off"
}
```

### Tasks Configuration

We provide several tasks in `.vscode/tasks.json`:

- **Watch**: `Ctrl+Shift+B` - Compile TypeScript in watch mode
- **Test**: Run unit tests
- **Lint**: Run ESLint
- **Package**: Create .vsix package

---

## Project Structure

```
vscode-extension/
├── src/                          # Source code
│   ├── extension.ts              # Extension entry point
│   ├── core/                     # Core services
│   │   ├── ConfigurationManager.ts
│   │   ├── StateManager.ts
│   │   └── EventBus.ts
│   ├── workflow/                 # Workflow engine
│   │   ├── WorkflowEngine.ts
│   │   ├── WorkflowStateMachine.ts
│   │   └── PhaseManager.ts
│   ├── documents/                # Document management
│   │   ├── DocumentManager.ts
│   │   ├── TemplateEngine.ts
│   │   └── parsers/
│   ├── agents/                   # AI agent integration
│   │   ├── AIAgentOrchestrator.ts
│   │   ├── AgentRegistry.ts
│   │   └── adapters/
│   ├── validation/               # Validation engine
│   │   ├── ValidationEngine.ts
│   │   ├── validators/
│   │   └── rules/
│   ├── git/                      # Git integration
│   │   ├── GitManager.ts
│   │   └── BranchManager.ts
│   ├── ui/                       # UI components
│   │   ├── providers/
│   │   ├── webviews/
│   │   └── trees/
│   ├── models/                   # Data models
│   │   └── types.ts
│   └── utils/                    # Utilities
│       ├── logger.ts
│       └── helpers.ts
├── webview-ui/                   # React-based webviews
│   ├── src/
│   │   ├── Dashboard/
│   │   ├── WorkflowVisualizer/
│   │   ├── CommandBuilder/
│   │   └── QualityDashboard/
│   └── package.json
├── media/                        # Icons, images
├── syntaxes/                     # Language grammars
├── snippets/                     # Code snippets
├── test/                         # Tests
│   ├── unit/
│   ├── integration/
│   └── e2e/
├── .vscode/                      # VSCode config
│   ├── launch.json
│   ├── tasks.json
│   └── settings.json
├── package.json                  # Extension manifest
├── tsconfig.json                 # TypeScript config
├── webpack.config.js             # Webpack config
└── README.md
```

---

## Architecture Overview

### High-Level Components

```
┌─────────────────────────────────────────────────┐
│           VSCode Extension Host                  │
├─────────────────────────────────────────────────┤
│  Extension Core (extension.ts)                   │
│  ├── Configuration Manager                       │
│  ├── State Manager                               │
│  └── Event Bus                                   │
├─────────────────────────────────────────────────┤
│  Business Logic                                  │
│  ├── Workflow Engine                             │
│  ├── Document Manager                            │
│  ├── AI Agent Orchestrator                       │
│  ├── Validation Engine                           │
│  └── Git Manager                                 │
├─────────────────────────────────────────────────┤
│  UI Layer                                        │
│  ├── Tree Views (Feature Explorer)               │
│  ├── WebViews (Dashboard, Visualizer)           │
│  ├── Editors (CodeLens, Hover, Diagnostics)     │
│  └── Status Bar                                  │
└─────────────────────────────────────────────────┘
```

### Key Design Patterns

#### 1. Event-Driven Architecture

```typescript
// EventBus - Central event system
export class EventBus {
  private listeners = new Map<string, Set<Function>>();

  on(event: string, handler: Function): void {
    if (!this.listeners.has(event)) {
      this.listeners.set(event, new Set());
    }
    this.listeners.get(event)!.add(handler);
  }

  emit(event: string, data?: any): void {
    const handlers = this.listeners.get(event);
    if (handlers) {
      handlers.forEach(handler => handler(data));
    }
  }
}

// Usage
eventBus.on('feature:updated', feature => {
  console.log('Feature updated:', feature.name);
  featureExplorer.refresh(feature);
});

eventBus.emit('feature:updated', updatedFeature);
```

#### 2. Service Locator Pattern

```typescript
// ServiceLocator - Access to shared services
export class ServiceLocator {
  private static services = new Map<string, any>();

  static register<T>(name: string, service: T): void {
    this.services.set(name, service);
  }

  static get<T>(name: string): T {
    const service = this.services.get(name);
    if (!service) {
      throw new Error(`Service '${name}' not found`);
    }
    return service as T;
  }
}

// Usage
ServiceLocator.register('workflowEngine', workflowEngine);
const engine = ServiceLocator.get<WorkflowEngine>('workflowEngine');
```

#### 3. Strategy Pattern for AI Agents

```typescript
// AgentAdapter interface
interface AgentAdapter {
  detect(): Promise<boolean>;
  executeCommand(command: string): Promise<ExecutionResult>;
}

// Concrete adapters
class ClaudeAdapter implements AgentAdapter {
  async detect(): Promise<boolean> {
    // Check if Claude CLI is installed
  }

  async executeCommand(command: string): Promise<ExecutionResult> {
    // Execute command with Claude
  }
}

// Registry manages adapters
class AgentRegistry {
  private adapters = new Map<string, AgentAdapter>();

  register(id: string, adapter: AgentAdapter): void {
    this.adapters.set(id, adapter);
  }

  async getAvailableAgents(): Promise<string[]> {
    const available: string[] = [];
    for (const [id, adapter] of this.adapters) {
      if (await adapter.detect()) {
        available.push(id);
      }
    }
    return available;
  }
}
```

#### 4. Observer Pattern for File Watching

```typescript
// FileWatcher - Monitors file system changes
export class FileWatcher {
  private watcher: vscode.FileSystemWatcher;
  private observers: Set<FileObserver> = new Set();

  constructor(pattern: string) {
    this.watcher = vscode.workspace.createFileSystemWatcher(pattern);

    this.watcher.onDidCreate(uri => {
      this.notify('created', uri);
    });

    this.watcher.onDidChange(uri => {
      this.notify('changed', uri);
    });

    this.watcher.onDidDelete(uri => {
      this.notify('deleted', uri);
    });
  }

  subscribe(observer: FileObserver): void {
    this.observers.add(observer);
  }

  private notify(event: string, uri: vscode.Uri): void {
    this.observers.forEach(observer => {
      observer.onFileEvent(event, uri);
    });
  }
}
```

---

## Development Workflow

### 1. Create a Feature Branch

```bash
git checkout -b feature/my-new-feature
```

### 2. Make Changes

Edit TypeScript files in `src/`:

```typescript
// src/workflow/WorkflowEngine.ts
export class WorkflowEngine {
  // Your implementation
}
```

### 3. Compile and Test

```bash
# Compile TypeScript
npm run compile

# Run unit tests
npm run test:unit

# Run integration tests
npm run test:integration
```

### 4. Debug in Extension Host

1. Set breakpoints in your code
2. Press `F5` to launch Extension Development Host
3. Trigger your code path
4. Debugger stops at breakpoints

### 5. Lint and Format

```bash
# Run ESLint
npm run lint

# Fix auto-fixable issues
npm run lint -- --fix
```

### 6. Commit Changes

```bash
git add .
git commit -m "feat: add workflow phase validation"
```

Follow [Conventional Commits](https://www.conventionalcommits.org/):
- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation changes
- `refactor:` - Code refactoring
- `test:` - Test additions/changes
- `chore:` - Build process or auxiliary tool changes

### 7. Push and Create PR

```bash
git push origin feature/my-new-feature
```

Then create a Pull Request on GitHub.

---

## Testing

### Unit Tests (Jest)

Location: `test/unit/`

```typescript
// test/unit/WorkflowEngine.test.ts
import { WorkflowEngine } from '../../src/workflow/WorkflowEngine';
import { WorkflowPhase } from '../../src/models/types';

describe('WorkflowEngine', () => {
  let engine: WorkflowEngine;

  beforeEach(() => {
    engine = new WorkflowEngine(mockStateManager, mockEventBus);
  });

  test('should transition from specification to planning', async () => {
    const feature = createMockFeature(WorkflowPhase.Specification);

    const result = await engine.transition(feature, WorkflowPhase.Planning);

    expect(result.success).toBe(true);
    expect(feature.phase).toBe(WorkflowPhase.Planning);
  });

  test('should reject invalid transitions', async () => {
    const feature = createMockFeature(WorkflowPhase.Specification);

    const result = await engine.transition(feature, WorkflowPhase.Implementation);

    expect(result.success).toBe(false);
    expect(result.errors).toContainEqual(
      expect.objectContaining({ code: 'INVALID_TRANSITION' })
    );
  });
});
```

Run tests:

```bash
npm run test:unit
```

### Integration Tests (Mocha)

Location: `test/integration/`

```typescript
// test/integration/featureCreation.test.ts
import * as vscode from 'vscode';
import * as assert from 'assert';

suite('Feature Creation Integration Tests', () => {
  test('Should create feature with all artifacts', async () => {
    // Execute command
    await vscode.commands.executeCommand('speckit.createFeature', {
      name: 'Test Feature'
    });

    // Verify files created
    const specFile = vscode.Uri.file(
      path.join(workspace, '.specify/specs/001-test-feature/spec.md')
    );
    const exists = await fileExists(specFile);
    assert.strictEqual(exists, true);

    // Verify feature in state
    const features = await getFeatures();
    assert.strictEqual(features.length, 1);
    assert.strictEqual(features[0].name, 'test-feature');
  });
});
```

Run tests:

```bash
npm run test:integration
```

### End-to-End Tests

Location: `test/e2e/`

```typescript
// test/e2e/fullWorkflow.test.ts
suite('Full Workflow E2E Tests', () => {
  test('Complete workflow from init to implementation', async () => {
    // 1. Initialize project
    await vscode.commands.executeCommand('speckit.initProject');

    // 2. Create constitution
    await vscode.commands.executeCommand('speckit.createConstitution');

    // 3. Create feature
    await vscode.commands.executeCommand('speckit.createFeature');

    // 4. Generate plan
    await vscode.commands.executeCommand('speckit.generatePlan');

    // 5. Verify workflow state
    const state = await getWorkflowState();
    assert.strictEqual(state.phase, WorkflowPhase.Planning);
  });
});
```

---

## Debugging

### Debug Extension

**launch.json** is already configured:

```json
{
  "configurations": [
    {
      "name": "Run Extension",
      "type": "extensionHost",
      "request": "launch",
      "args": [
        "--extensionDevelopmentPath=${workspaceFolder}"
      ],
      "outFiles": ["${workspaceFolder}/dist/**/*.js"],
      "preLaunchTask": "npm: compile"
    }
  ]
}
```

**Steps:**
1. Set breakpoints in `.ts` files
2. Press `F5`
3. New window opens with extension
4. Trigger functionality
5. Debugger pauses at breakpoints

### Debug Tests

```json
{
  "name": "Extension Tests",
  "type": "extensionHost",
  "request": "launch",
  "args": [
    "--extensionDevelopmentPath=${workspaceFolder}",
    "--extensionTestsPath=${workspaceFolder}/out/test/suite/index"
  ],
  "outFiles": ["${workspaceFolder}/out/test/**/*.js"],
  "preLaunchTask": "npm: compile-tests"
}
```

### Debug Webviews

Webviews are HTML/React, so debug in DevTools:

1. In Extension Development Host, press `Ctrl+Shift+P`
2. Run "Developer: Open Webview Developer Tools"
3. Use Chrome DevTools to debug React components

### Logging

Use the included logger:

```typescript
import { Logger } from './utils/logger';

const logger = new Logger('WorkflowEngine');

logger.debug('Transitioning to planning phase');
logger.info('Feature created successfully');
logger.warn('Quality score below threshold');
logger.error('Failed to load configuration', error);
```

View logs:
- **Output Panel**: "SpecKit" output channel
- **Developer Tools**: `Help > Toggle Developer Tools`

---

## Contributing Guidelines

### Code Style

- Use TypeScript strict mode
- Follow ESLint rules
- Use meaningful variable names
- Add JSDoc comments for public APIs

```typescript
/**
 * Transitions a feature to a new workflow phase
 *
 * @param feature - The feature to transition
 * @param targetPhase - The target workflow phase
 * @returns Transition result with success status and any errors
 * @throws {Error} If feature is invalid
 */
public async transition(
  feature: Feature,
  targetPhase: WorkflowPhase
): Promise<TransitionResult> {
  // Implementation
}
```

### Commit Messages

Follow Conventional Commits:

```
feat(workflow): add phase transition validation

- Implement state machine for valid transitions
- Add prerequisite checking before transitions
- Emit events on phase changes

Closes #123
```

### Pull Request Process

1. **Create PR** with clear title and description
2. **Link issue** if applicable
3. **Add tests** for new functionality
4. **Update docs** if changing APIs
5. **Request review** from maintainers
6. **Address feedback** promptly
7. **Squash commits** before merge

---

## Common Tasks

### Adding a New Command

1. **Define command in package.json:**

```json
{
  "contributes": {
    "commands": [
      {
        "command": "speckit.myNewCommand",
        "title": "My New Command",
        "category": "SpecKit"
      }
    ]
  }
}
```

2. **Register command in extension.ts:**

```typescript
const disposable = vscode.commands.registerCommand(
  'speckit.myNewCommand',
  async () => {
    // Implementation
    vscode.window.showInformationMessage('Command executed!');
  }
);

context.subscriptions.push(disposable);
```

3. **Add tests:**

```typescript
test('myNewCommand should execute successfully', async () => {
  await vscode.commands.executeCommand('speckit.myNewCommand');
  // Assertions
});
```

### Adding a New Validator

1. **Create validator class:**

```typescript
// src/validation/validators/MyValidator.ts
export class MyValidator implements Validator {
  async validate(document: Document): Promise<ValidationResult> {
    const issues: QualityIssue[] = [];

    // Validation logic
    if (/* condition */) {
      issues.push({
        severity: IssueSeverity.Warning,
        message: 'Validation message',
        location: { /* ... */ }
      });
    }

    return {
      valid: issues.length === 0,
      issues
    };
  }
}
```

2. **Register validator:**

```typescript
// src/validation/ValidationEngine.ts
this.validators.push(new MyValidator());
```

### Adding a New AI Agent Adapter

1. **Create adapter:**

```typescript
// src/agents/adapters/MyAgentAdapter.ts
export class MyAgentAdapter implements AgentAdapter {
  id = 'my-agent';
  name = 'My Agent';

  async detect(): Promise<boolean> {
    // Check if agent is installed
    return checkForCLI('my-agent');
  }

  async executeCommand(command: string): Promise<ExecutionResult> {
    // Execute command using agent's CLI
  }
}
```

2. **Register adapter:**

```typescript
// src/agents/AgentRegistry.ts
this.register('my-agent', new MyAgentAdapter());
```

3. **Update configuration:**

```json
{
  "speckit.agent.type": {
    "enum": ["claude", "gemini", "my-agent", /* ... */]
  }
}
```

---

## Troubleshooting

### Extension Won't Activate

**Problem:** Extension doesn't load in development host

**Solutions:**
- Check `activationEvents` in package.json
- Verify TypeScript compiled successfully (`npm run compile`)
- Check for errors in Output > Extension Host
- Clear extension cache: `Ctrl+Shift+P` > "Developer: Reload Window"

### Tests Failing

**Problem:** Tests fail unexpectedly

**Solutions:**
- Run `npm run compile-tests` before testing
- Check test file paths are correct
- Verify mocks are properly configured
- Check for async issues (missing `await`)

### Webview Not Loading

**Problem:** Webview shows blank or errors

**Solutions:**
- Check webview bundle built: `cd webview-ui && npm run build`
- Verify CSP (Content Security Policy) settings
- Check webview DevTools for errors
- Ensure correct resource URIs used

### Breakpoints Not Hitting

**Problem:** Debugger doesn't stop at breakpoints

**Solutions:**
- Verify source maps generated (`npm run compile`)
- Check `outFiles` in launch.json points to compiled code
- Ensure breakpoint in correct file (not in `dist/`)
- Try "Reload Window" in Extension Development Host

---

## Resources

- **VSCode Extension API**: https://code.visualstudio.com/api
- **Extension Samples**: https://github.com/microsoft/vscode-extension-samples
- **SpecKit Docs**: https://github.github.io/spec-kit/
- **TypeScript Handbook**: https://www.typescriptlang.org/docs/

---

## Getting Help

- **GitHub Issues**: https://github.com/github/spec-kit/issues
- **Discussions**: https://github.com/github/spec-kit/discussions
- **Discord**: https://discord.gg/speckit

---

Happy coding! 🚀
