# SpecKit VSCode Extension - Technical Architecture

## Document Purpose

This document provides detailed technical architecture specifications for the SpecKit VSCode extension, including TypeScript interfaces, class structures, data models, and implementation patterns.

---

## Table of Contents

1. [Core Type Definitions](#core-type-definitions)
2. [Extension Architecture](#extension-architecture)
3. [Workflow Engine](#workflow-engine)
4. [Document Management System](#document-management-system)
5. [AI Agent Orchestration](#ai-agent-orchestration)
6. [Validation Engine](#validation-engine)
7. [Git Integration Layer](#git-integration-layer)
8. [UI Components](#ui-components)
9. [State Management](#state-management)
10. [Extension Points](#extension-points)

---

## Core Type Definitions

### Project Models

```typescript
/**
 * Core SpecKit project configuration
 */
export interface SpecKitProject {
  /** Project metadata */
  version: string;
  name: string;
  description?: string;
  created: Date;
  updated: Date;

  /** AI agent configuration */
  agent: AgentType;
  agentVersion?: string;
  scriptType: ScriptType;

  /** Project paths */
  paths: ProjectPaths;

  /** Features in the project */
  features: Map<string, Feature>;

  /** Project constitution */
  constitution?: Constitution;

  /** Project-wide settings */
  settings: ProjectSettings;
}

/**
 * Project directory structure paths
 */
export interface ProjectPaths {
  root: string;
  specs: string;
  templates: string;
  scripts: string;
  memory: string;
  commands: string;
}

/**
 * Supported AI agent types
 */
export enum AgentType {
  Claude = 'claude',
  Gemini = 'gemini',
  Copilot = 'copilot',
  Cursor = 'cursor-agent',
  Qwen = 'qwen',
  OpenCode = 'opencode',
  Windsurf = 'windsurf',
  KiloCode = 'kilocode',
  Auggie = 'auggie',
  Roo = 'roo',
  CodeBuddy = 'codebuddy',
  AmazonQ = 'q',
  Amp = 'amp',
  Shai = 'shai'
}

/**
 * Script type for shell operations
 */
export enum ScriptType {
  Bash = 'sh',
  PowerShell = 'ps'
}

/**
 * Feature representation
 */
export interface Feature {
  id: string;
  number: number;
  name: string;
  displayName: string;
  description?: string;

  /** Workflow state */
  phase: WorkflowPhase;
  status: FeatureStatus;
  progress: number; // 0-100

  /** Git information */
  branch?: string;
  baseBranch?: string;

  /** Artifacts */
  artifacts: FeatureArtifacts;

  /** Quality metrics */
  quality: QualityMetrics;

  /** Blockers and issues */
  blockers: Blocker[];

  /** Timestamps */
  created: Date;
  updated: Date;
  phaseStarted?: Date;
}

/**
 * Feature status enumeration
 */
export enum FeatureStatus {
  NotStarted = 'not_started',
  InProgress = 'in_progress',
  Blocked = 'blocked',
  Completed = 'completed',
  Archived = 'archived'
}

/**
 * Workflow phase enumeration
 */
export enum WorkflowPhase {
  Constitution = 'constitution',
  Specification = 'specification',
  Clarification = 'clarification',
  Planning = 'planning',
  Tasks = 'tasks',
  Analysis = 'analysis',
  Implementation = 'implementation',
  Completed = 'completed'
}

/**
 * Feature artifacts (documents and files)
 */
export interface FeatureArtifacts {
  specification?: Artifact;
  clarifications?: Artifact;
  plan?: Artifact;
  research?: Artifact;
  dataModel?: Artifact;
  contracts?: Artifact[];
  tasks?: Artifact;
  checklist?: Artifact;
  quickstart?: Artifact;
}

/**
 * Individual artifact representation
 */
export interface Artifact {
  path: string;
  type: ArtifactType;
  exists: boolean;
  status: ArtifactStatus;
  created?: Date;
  updated?: Date;
  size?: number;
  hash?: string; // For change detection
}

export enum ArtifactType {
  Specification = 'spec',
  Clarifications = 'clarifications',
  Plan = 'plan',
  Research = 'research',
  DataModel = 'data-model',
  Contract = 'contract',
  Tasks = 'tasks',
  Checklist = 'checklist',
  Quickstart = 'quickstart'
}

export enum ArtifactStatus {
  Missing = 'missing',
  Empty = 'empty',
  Draft = 'draft',
  Complete = 'complete',
  Validated = 'validated',
  Invalid = 'invalid'
}

/**
 * Quality metrics for a feature
 */
export interface QualityMetrics {
  overall: number; // 0-100
  breakdown: QualityBreakdown;
  trend: QualityTrend[];
  issues: QualityIssue[];
}

export interface QualityBreakdown {
  completeness: number;
  clarity: number;
  testability: number;
  constitutionalCompliance: number;
  crossArtifactConsistency: number;
}

export interface QualityTrend {
  date: Date;
  score: number;
  phase: WorkflowPhase;
}

export interface QualityIssue {
  id: string;
  severity: IssueSeverity;
  category: IssueCategory;
  message: string;
  location: Location;
  suggestion?: string;
  autoFixable: boolean;
}

export enum IssueSeverity {
  Error = 'error',
  Warning = 'warning',
  Info = 'info',
  Hint = 'hint'
}

export enum IssueCategory {
  Completeness = 'completeness',
  Clarity = 'clarity',
  Consistency = 'consistency',
  Constitutional = 'constitutional',
  Formatting = 'formatting',
  BestPractice = 'best-practice'
}

export interface Location {
  artifact: ArtifactType;
  path: string;
  line?: number;
  column?: number;
  range?: Range;
}

export interface Range {
  start: Position;
  end: Position;
}

export interface Position {
  line: number;
  character: number;
}

/**
 * Feature blocker representation
 */
export interface Blocker {
  id: string;
  type: BlockerType;
  message: string;
  severity: IssueSeverity;
  location?: Location;
  createdAt: Date;
  resolvedAt?: Date;
}

export enum BlockerType {
  MissingArtifact = 'missing-artifact',
  ValidationFailure = 'validation-failure',
  UnansweredClarification = 'unanswered-clarification',
  ConstitutionalViolation = 'constitutional-violation',
  IncompleteRequirement = 'incomplete-requirement',
  DependencyIssue = 'dependency-issue'
}

/**
 * Project constitution
 */
export interface Constitution {
  path: string;
  articles: Article[];
  principles: Principle[];
  validated: boolean;
  lastValidated?: Date;
}

export interface Article {
  number: number;
  title: string;
  content: string;
  sections: Section[];
  mandatory: boolean;
}

export interface Section {
  number: string; // e.g., "7.3"
  title: string;
  content: string;
  requirements: Requirement[];
}

export interface Requirement {
  id: string;
  description: string;
  type: RequirementType;
  enforcementLevel: EnforcementLevel;
}

export enum RequirementType {
  Must = 'must',
  Should = 'should',
  MustNot = 'must-not',
  ShouldNot = 'should-not',
  May = 'may'
}

export enum EnforcementLevel {
  Blocking = 'blocking',
  Warning = 'warning',
  Advisory = 'advisory'
}

export interface Principle {
  id: string;
  name: string;
  description: string;
  rationale?: string;
  examples?: string[];
}

/**
 * Project settings
 */
export interface ProjectSettings {
  workflow: WorkflowSettings;
  validation: ValidationSettings;
  git: GitSettings;
  ui: UISettings;
  analytics: AnalyticsSettings;
}

export interface WorkflowSettings {
  enforcement: EnforcementMode;
  qualityThresholds: QualityThresholds;
  autoProgress: boolean;
  showVisualization: boolean;
  promptBeforeTransitions: boolean;
}

export enum EnforcementMode {
  Strict = 'strict',
  Guided = 'guided',
  Flexible = 'flexible'
}

export interface QualityThresholds {
  minSpecificationScore: number;
  minPlanScore: number;
  minOverallScore: number;
  blockOnConstitutionalViolations: boolean;
}

export interface ValidationSettings {
  enabled: boolean;
  realTime: boolean;
  delay: number; // milliseconds
  maxDiagnostics: number;
  autoFix: boolean;
}

export interface GitSettings {
  autoCreateBranches: boolean;
  autoCommit: boolean;
  autoPush: boolean;
  branchPattern: string; // e.g., "{number}-{feature-name}"
  featureNumbering: NumberingSettings;
  commitMessageTemplate: string;
}

export interface NumberingSettings {
  startNumber: number;
  paddingDigits: number;
  prefix?: string;
}

export interface UISettings {
  showCodeLens: boolean;
  showHoverTooltips: boolean;
  showInlineDiagnostics: boolean;
  enableAutoComplete: boolean;
  theme: UITheme;
}

export enum UITheme {
  Auto = 'auto',
  Light = 'light',
  Dark = 'dark',
  HighContrast = 'high-contrast'
}

export interface AnalyticsSettings {
  enabled: boolean;
  trackQualityTrends: boolean;
  trackCommandUsage: boolean;
  sendAnonymousData: boolean;
  retentionDays: number;
}
```

---

## Extension Architecture

### Main Extension Class

```typescript
import * as vscode from 'vscode';

/**
 * Main extension class - entry point for the SpecKit extension
 */
export class SpecKitExtension implements vscode.Disposable {
  private context: vscode.ExtensionContext;
  private disposables: vscode.Disposable[] = [];

  // Core services
  private configManager: ConfigurationManager;
  private stateManager: StateManager;
  private eventBus: EventBus;

  // Feature managers
  private workflowEngine: WorkflowEngine;
  private documentManager: DocumentManager;
  private agentOrchestrator: AIAgentOrchestrator;
  private validationEngine: ValidationEngine;
  private gitManager: GitManager;

  // UI providers
  private featureExplorer: FeatureExplorerProvider;
  private workflowVisualizer: WorkflowVisualizerProvider;
  private dashboardProvider: DashboardProvider;
  private commandBuilder: CommandBuilderProvider;

  constructor(context: vscode.ExtensionContext) {
    this.context = context;
  }

  /**
   * Activate the extension
   */
  public async activate(): Promise<void> {
    console.log('Activating SpecKit extension...');

    try {
      // Initialize core services
      await this.initializeCoreServices();

      // Initialize feature managers
      await this.initializeFeatureManagers();

      // Initialize UI providers
      await this.initializeUIProviders();

      // Register commands
      this.registerCommands();

      // Register event listeners
      this.registerEventListeners();

      // Load project if in SpecKit workspace
      await this.loadProject();

      console.log('SpecKit extension activated successfully');
    } catch (error) {
      vscode.window.showErrorMessage(
        `Failed to activate SpecKit extension: ${error.message}`
      );
      throw error;
    }
  }

  /**
   * Initialize core services
   */
  private async initializeCoreServices(): Promise<void> {
    this.configManager = new ConfigurationManager(this.context);
    this.stateManager = new StateManager(this.context);
    this.eventBus = new EventBus();

    this.disposables.push(
      this.configManager,
      this.stateManager,
      this.eventBus
    );
  }

  /**
   * Initialize feature managers
   */
  private async initializeFeatureManagers(): Promise<void> {
    this.workflowEngine = new WorkflowEngine(
      this.stateManager,
      this.eventBus
    );

    this.documentManager = new DocumentManager(
      this.configManager,
      this.eventBus
    );

    this.validationEngine = new ValidationEngine(
      this.documentManager,
      this.configManager,
      this.eventBus
    );

    this.agentOrchestrator = new AIAgentOrchestrator(
      this.configManager,
      this.eventBus
    );

    this.gitManager = new GitManager(
      this.configManager,
      this.eventBus
    );

    this.disposables.push(
      this.workflowEngine,
      this.documentManager,
      this.validationEngine,
      this.agentOrchestrator,
      this.gitManager
    );
  }

  /**
   * Initialize UI providers
   */
  private async initializeUIProviders(): Promise<void> {
    // Feature Explorer tree view
    this.featureExplorer = new FeatureExplorerProvider(
      this.stateManager,
      this.eventBus
    );
    const featureTreeView = vscode.window.createTreeView('speckit.features', {
      treeDataProvider: this.featureExplorer,
      showCollapseAll: true
    });

    // Workflow Visualizer webview
    this.workflowVisualizer = new WorkflowVisualizerProvider(
      this.context,
      this.workflowEngine,
      this.eventBus
    );

    // Dashboard webview
    this.dashboardProvider = new DashboardProvider(
      this.context,
      this.stateManager,
      this.eventBus
    );

    // Command Builder webview
    this.commandBuilder = new CommandBuilderProvider(
      this.context,
      this.agentOrchestrator,
      this.eventBus
    );

    this.disposables.push(
      featureTreeView,
      this.featureExplorer,
      this.workflowVisualizer,
      this.dashboardProvider,
      this.commandBuilder
    );
  }

  /**
   * Register extension commands
   */
  private registerCommands(): void {
    const commands: { [command: string]: (...args: any[]) => any } = {
      // Project commands
      'speckit.initProject': () => this.initProject(),
      'speckit.openDashboard': () => this.openDashboard(),

      // Feature commands
      'speckit.createFeature': () => this.createFeature(),
      'speckit.openFeature': (feature: Feature) => this.openFeature(feature),
      'speckit.deleteFeature': (feature: Feature) => this.deleteFeature(feature),

      // Workflow commands
      'speckit.createConstitution': () => this.createConstitution(),
      'speckit.createSpecification': () => this.createSpecification(),
      'speckit.generatePlan': () => this.generatePlan(),
      'speckit.breakdownTasks': () => this.breakdownTasks(),
      'speckit.runAnalysis': () => this.runAnalysis(),
      'speckit.implement': () => this.implement(),

      // View commands
      'speckit.showWorkflow': (feature: Feature) => this.showWorkflow(feature),
      'speckit.showQualityDashboard': (feature: Feature) => this.showQualityDashboard(feature),

      // AI Agent commands
      'speckit.selectAgent': () => this.selectAgent(),
      'speckit.buildCommand': () => this.buildCommand(),

      // Git commands
      'speckit.createBranch': (feature: Feature) => this.createBranch(feature),
      'speckit.createPR': (feature: Feature) => this.createPR(feature),

      // Utility commands
      'speckit.refresh': () => this.refresh(),
      'speckit.openSettings': () => this.openSettings()
    };

    for (const [command, handler] of Object.entries(commands)) {
      const disposable = vscode.commands.registerCommand(command, handler);
      this.disposables.push(disposable);
    }
  }

  /**
   * Register event listeners
   */
  private registerEventListeners(): void {
    // File system watcher
    const watcher = vscode.workspace.createFileSystemWatcher(
      '**/.specify/specs/**/*'
    );

    watcher.onDidCreate(uri => this.onFileCreated(uri));
    watcher.onDidChange(uri => this.onFileChanged(uri));
    watcher.onDidDelete(uri => this.onFileDeleted(uri));

    this.disposables.push(watcher);

    // Configuration changes
    vscode.workspace.onDidChangeConfiguration(e => {
      if (e.affectsConfiguration('speckit')) {
        this.onConfigurationChanged();
      }
    });

    // Event bus listeners
    this.eventBus.on('feature:updated', feature => this.onFeatureUpdated(feature));
    this.eventBus.on('workflow:phaseChanged', data => this.onPhaseChanged(data));
    this.eventBus.on('validation:completed', results => this.onValidationCompleted(results));
  }

  /**
   * Load project if in SpecKit workspace
   */
  private async loadProject(): Promise<void> {
    const workspaceRoot = vscode.workspace.workspaceFolders?.[0]?.uri.fsPath;
    if (!workspaceRoot) {
      return;
    }

    const isSpecKitProject = await this.configManager.isSpecKitProject(workspaceRoot);
    if (isSpecKitProject) {
      await this.configManager.loadProject(workspaceRoot);
      this.stateManager.setProjectLoaded(true);
      this.featureExplorer.refresh();
    }
  }

  // Command implementations
  private async initProject(): Promise<void> {
    // Implementation in next section
  }

  private async openDashboard(): Promise<void> {
    await this.dashboardProvider.show();
  }

  private async createFeature(): Promise<void> {
    // Implementation in workflow section
  }

  private async openFeature(feature: Feature): Promise<void> {
    if (feature.artifacts.specification) {
      const doc = await vscode.workspace.openTextDocument(
        vscode.Uri.file(feature.artifacts.specification.path)
      );
      await vscode.window.showTextDocument(doc);
    }
  }

  private async deleteFeature(feature: Feature): Promise<void> {
    // Implementation in feature management section
  }

  // Event handlers
  private async onFileCreated(uri: vscode.Uri): Promise<void> {
    await this.stateManager.refreshFeatures();
    this.featureExplorer.refresh();
  }

  private async onFileChanged(uri: vscode.Uri): Promise<void> {
    // Trigger revalidation
    await this.validationEngine.validateFile(uri.fsPath);
  }

  private async onFileDeleted(uri: vscode.Uri): Promise<void> {
    await this.stateManager.refreshFeatures();
    this.featureExplorer.refresh();
  }

  private async onConfigurationChanged(): Promise<void> {
    await this.configManager.reloadConfiguration();
    this.featureExplorer.refresh();
  }

  private async onFeatureUpdated(feature: Feature): Promise<void> {
    this.featureExplorer.refresh(feature);
  }

  private async onPhaseChanged(data: { feature: Feature; from: WorkflowPhase; to: WorkflowPhase }): Promise<void> {
    vscode.window.showInformationMessage(
      `Feature ${data.feature.name} transitioned from ${data.from} to ${data.to}`
    );
    this.featureExplorer.refresh(data.feature);
  }

  private async onValidationCompleted(results: ValidationResult): Promise<void> {
    // Update diagnostics, quality scores, etc.
  }

  /**
   * Dispose of resources
   */
  public dispose(): void {
    for (const disposable of this.disposables) {
      disposable.dispose();
    }
  }
}

/**
 * Extension activation function (called by VSCode)
 */
export async function activate(context: vscode.ExtensionContext): Promise<void> {
  const extension = new SpecKitExtension(context);
  await extension.activate();
  context.subscriptions.push(extension);
}

/**
 * Extension deactivation function (called by VSCode)
 */
export function deactivate(): void {
  console.log('SpecKit extension deactivated');
}
```

---

## Workflow Engine

```typescript
/**
 * Workflow engine manages feature workflow state and transitions
 */
export class WorkflowEngine implements vscode.Disposable {
  private stateManager: StateManager;
  private eventBus: EventBus;
  private stateMachine: WorkflowStateMachine;

  constructor(stateManager: StateManager, eventBus: EventBus) {
    this.stateManager = stateManager;
    this.eventBus = eventBus;
    this.stateMachine = new WorkflowStateMachine();
  }

  /**
   * Get current workflow phase for a feature
   */
  public getCurrentPhase(feature: Feature): WorkflowPhase {
    return feature.phase;
  }

  /**
   * Transition to a new workflow phase
   */
  public async transition(
    feature: Feature,
    targetPhase: WorkflowPhase
  ): Promise<TransitionResult> {
    // Validate transition is allowed
    const validation = this.stateMachine.validateTransition(
      feature.phase,
      targetPhase
    );

    if (!validation.allowed) {
      return {
        success: false,
        errors: validation.errors
      };
    }

    // Check prerequisites
    const prerequisites = await this.checkPrerequisites(feature, targetPhase);
    if (!prerequisites.satisfied) {
      return {
        success: false,
        errors: prerequisites.missing.map(p => ({
          code: 'PREREQUISITE_MISSING',
          message: `Prerequisite not met: ${p}`
        }))
      };
    }

    // Perform transition
    const previousPhase = feature.phase;
    feature.phase = targetPhase;
    feature.phaseStarted = new Date();
    feature.updated = new Date();

    // Update feature in state
    await this.stateManager.updateFeature(feature);

    // Emit event
    this.eventBus.emit('workflow:phaseChanged', {
      feature,
      from: previousPhase,
      to: targetPhase
    });

    return {
      success: true,
      data: { feature, previousPhase, newPhase: targetPhase }
    };
  }

  /**
   * Get next recommended actions for current phase
   */
  public getNextActions(feature: Feature): Action[] {
    const actions: Action[] = [];

    switch (feature.phase) {
      case WorkflowPhase.Constitution:
        actions.push({
          id: 'create-constitution',
          label: 'Create Constitution',
          description: 'Define project principles and guidelines',
          command: 'speckit.createConstitution',
          priority: ActionPriority.High
        });
        break;

      case WorkflowPhase.Specification:
        actions.push({
          id: 'complete-spec',
          label: 'Complete Specification',
          description: 'Add user stories and acceptance criteria',
          command: 'speckit.editSpecification',
          priority: ActionPriority.High
        });

        if (feature.quality.breakdown.clarity < 80) {
          actions.push({
            id: 'run-clarification',
            label: 'Run Clarification Workflow',
            description: 'Address ambiguities in specification',
            command: 'speckit.runClarification',
            priority: ActionPriority.Medium
          });
        }
        break;

      case WorkflowPhase.Planning:
        actions.push({
          id: 'generate-plan',
          label: 'Generate Implementation Plan',
          description: 'Create technical design and architecture',
          command: 'speckit.generatePlan',
          priority: ActionPriority.High
        });
        break;

      case WorkflowPhase.Tasks:
        actions.push({
          id: 'breakdown-tasks',
          label: 'Break Down Tasks',
          description: 'Generate actionable task list from plan',
          command: 'speckit.breakdownTasks',
          priority: ActionPriority.High
        });
        break;

      case WorkflowPhase.Analysis:
        actions.push({
          id: 'run-analysis',
          label: 'Run Consistency Analysis',
          description: 'Validate alignment across artifacts',
          command: 'speckit.runAnalysis',
          priority: ActionPriority.Medium
        });
        break;

      case WorkflowPhase.Implementation:
        actions.push({
          id: 'implement',
          label: 'Execute Implementation',
          description: 'Build feature according to plan',
          command: 'speckit.implement',
          priority: ActionPriority.High
        });
        break;
    }

    return actions;
  }

  /**
   * Check prerequisites for phase transition
   */
  private async checkPrerequisites(
    feature: Feature,
    targetPhase: WorkflowPhase
  ): Promise<PrerequisiteCheck> {
    const missing: string[] = [];

    switch (targetPhase) {
      case WorkflowPhase.Specification:
        if (!await this.hasConstitution()) {
          missing.push('Project constitution required');
        }
        break;

      case WorkflowPhase.Planning:
        if (!feature.artifacts.specification?.exists) {
          missing.push('Specification document required');
        }
        if (feature.quality.breakdown.completeness < 75) {
          missing.push('Specification quality below threshold (75%)');
        }
        break;

      case WorkflowPhase.Tasks:
        if (!feature.artifacts.plan?.exists) {
          missing.push('Implementation plan required');
        }
        break;

      case WorkflowPhase.Implementation:
        if (!feature.artifacts.tasks?.exists) {
          missing.push('Task breakdown required');
        }
        break;
    }

    return {
      satisfied: missing.length === 0,
      missing
    };
  }

  private async hasConstitution(): Promise<boolean> {
    const project = this.stateManager.getProject();
    return project?.constitution?.validated ?? false;
  }

  public dispose(): void {
    // Cleanup
  }
}

/**
 * Workflow state machine - defines allowed transitions
 */
class WorkflowStateMachine {
  private transitions: Map<WorkflowPhase, WorkflowPhase[]>;

  constructor() {
    this.transitions = new Map([
      [WorkflowPhase.Constitution, [WorkflowPhase.Specification]],
      [WorkflowPhase.Specification, [WorkflowPhase.Clarification, WorkflowPhase.Planning]],
      [WorkflowPhase.Clarification, [WorkflowPhase.Planning]],
      [WorkflowPhase.Planning, [WorkflowPhase.Tasks, WorkflowPhase.Analysis]],
      [WorkflowPhase.Tasks, [WorkflowPhase.Analysis, WorkflowPhase.Implementation]],
      [WorkflowPhase.Analysis, [WorkflowPhase.Implementation]],
      [WorkflowPhase.Implementation, [WorkflowPhase.Completed]]
    ]);
  }

  /**
   * Validate if transition is allowed
   */
  public validateTransition(
    from: WorkflowPhase,
    to: WorkflowPhase
  ): TransitionValidation {
    const allowedTargets = this.transitions.get(from) ?? [];

    if (!allowedTargets.includes(to)) {
      return {
        allowed: false,
        errors: [{
          code: 'INVALID_TRANSITION',
          message: `Cannot transition from ${from} to ${to}. Allowed transitions: ${allowedTargets.join(', ')}`
        }]
      };
    }

    return {
      allowed: true,
      errors: []
    };
  }
}

// Supporting types
export interface TransitionResult {
  success: boolean;
  errors?: TransitionError[];
  data?: {
    feature: Feature;
    previousPhase: WorkflowPhase;
    newPhase: WorkflowPhase;
  };
}

export interface TransitionError {
  code: string;
  message: string;
}

export interface TransitionValidation {
  allowed: boolean;
  errors: TransitionError[];
}

export interface PrerequisiteCheck {
  satisfied: boolean;
  missing: string[];
}

export interface Action {
  id: string;
  label: string;
  description: string;
  command: string;
  arguments?: any[];
  priority: ActionPriority;
  enabled?: boolean;
}

export enum ActionPriority {
  Low = 'low',
  Medium = 'medium',
  High = 'high',
  Critical = 'critical'
}
```

This architecture document provides the foundation for implementing the SpecKit VSCode extension. It includes:

1. **Comprehensive type definitions** for all core entities
2. **Main extension class** with activation and lifecycle management
3. **Workflow engine** for managing feature workflow state
4. **State machine** for validating phase transitions
5. **Event-driven architecture** using an event bus
6. **Extensibility points** for customization

The next sections would cover:
- Document Management System
- AI Agent Orchestration
- Validation Engine
- Git Integration Layer
- UI Components
- State Management
- Extension Points

Would you like me to continue building out the remaining sections?
