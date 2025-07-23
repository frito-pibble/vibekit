# No-Code AI Platform Architecture Document

**Document Status:** 📝 **DRAFT - UNDER ANALYSIS**  
**Document Version:** 3.0  
**Date:** July 17, 2024  
**Created by:** Architect Winston  
**Based on:** PRD v1.0 and Technical Architecture Analysis

---

## Introduction

This document outlines the overall project architecture for the No-Code AI Platform, including backend systems, shared services, and non-UI specific concerns. Its primary goal is to serve as the guiding architectural blueprint for AI-driven development, ensuring consistency and adherence to chosen patterns and technologies.

**Relationship to Frontend Architecture:**
The project includes a significant user interface component. A separate Frontend Architecture Document will detail the frontend-specific design and MUST be used in conjunction with this document. Core technology stack choices documented herein (see "Tech Stack") are definitive for the entire project, including any frontend components.

**Architecture Distinction:**
This document covers TWO distinct architectural approaches:

1. **Platform Architecture** - Traditional microservices approach for the no-code platform itself
2. **Generated Solution Architecture** - Vertical Slice Architecture (VSA) for applications created by the platform

### Foundation Strategy: V0-Clone Adaptation

**Analysis:** After comprehensive evaluation of available options, we will use the V0-Clone template from VibeKit as our foundation:

**Selected Foundation:**

- **Frontend:** V0-Clone Next.js 15 template with complete UI system
- **Backend:** Existing Convex + Inngest + VibeKit integration
- **Agent System:** VibeKit SDK with BMAD methodology overlay

**Rationale:**

- **80% of infrastructure already built** (authentication, real-time updates, AI integration)
- **Perfect architectural alignment** with chat-driven development approach
- **Production-ready components** (shadcn/ui, TypeScript, modern stack)
- **Proven real-time capabilities** essential for collaborative workflows
- **Significant time savings** (6-8 weeks vs 16-20 weeks from scratch)

**V0-Clone Foundation Benefits:**

- ✅ Next.js 15 + TypeScript production-ready stack
- ✅ Convex real-time state management
- ✅ Inngest background job processing
- ✅ VibeKit SDK integration for AI code generation
- ✅ Complete authentication system (NextAuth.js)
- ✅ GitHub OAuth and repository management
- ✅ Modern UI components (Tailwind + shadcn/ui)
- ✅ Chat interface and session management
- ✅ Template system for extensibility

### Change Log

| Version   | Date          | Author  | Changes                                                                                        |
| --------- | ------------- | ------- | ---------------------------------------------------------------------------------------------- |
| 1.0       | December 2024 | Winston | Initial architecture design based on PRD requirements                                          |
| 1.0-DRAFT | December 2024 | Winston | Marked as draft pending additional tool research and evaluation                                |
| 2.0       | December 2024 | Winston | Updated with V0-Clone foundation and VibeKit integration strategy                              |
| 3.0       | July 17, 2024 | Winston | Added Vertical Slice Architecture (VSA) for generated solutions                                |
| 3.1       | July 22, 2025 | Winston | Enhanced Memory Pickle MCP with semantic search and learning capabilities                      |
| 3.2       | July 22, 2025 | Winston | Added Claude Code Router integration for multi-model LLM routing and BMAD agent specialization |

---

## System Overview

### High-Level Architecture

The No-Code AI Platform employs a **dual architectural approach**:

**1. Platform Architecture (Traditional Microservices)**
The no-code platform itself uses microservices designed around the BMAD framework's agent system. The platform transforms user visions into production-ready applications through a structured 5-phase process orchestrated by specialized AI agents.

**2. Generated Solution Architecture (Vertical Slice Architecture)**
Applications created by the platform use Vertical Slice Architecture (VSA) to ensure feature isolation, conflict prevention, and maintainable code generation for non-technical users.

**Core Architectural Principles:**

1. **Agent-Centric Design:** Each BMAD agent operates as an independent service
2. **Document-Driven Workflows:** Structured handoffs through standardized templates
3. **VSA-Aware Generation:** Generated solutions use vertical slices for feature isolation
4. **Progressive Complexity:** Simple to start, scales with user needs
5. **User Experience First:** Architecture optimized for non-technical users
6. **Production Ready:** Built for scale from day one

### System Context Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                    No-Code AI Platform                          │
├─────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │   Web UI    │  │ Agent APIs  │  │ Generated   │              │
│  │ (Next.js)   │  │(Microsvcs)  │  │ Apps        │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
├─────────────────────────────────────────────────────────────────┤
│  External: LLM Providers, Cloud Services, User Domains          │
└─────────────────────────────────────────────────────────────────┘
```

---

## Technology Stack

### Core Technology Decisions

**Backend Framework:** Node.js with TypeScript + AI Fastify Template

- **Primary:** Fastify with TypeScript for high-performance APIs
- **AI Integration:** AI Fastify Template for enterprise-grade backend generation
- **Quality Assurance:** Mutation testing (85% threshold) + comprehensive validation
- **Rationale:** Excellent LLM integration libraries, strong ecosystem, AI-optimized patterns
- **Version:** Node.js 20+ LTS, TypeScript 5.0+ with @tsconfig/strictest preset

**Frontend Framework:** Next.js 14+ with React 18+

- **Rationale:** Full-stack capabilities, excellent developer experience, production-ready
- **Styling:** Tailwind CSS for rapid UI development
- **Components:** Radix UI primitives for accessibility

**Database Strategy:**

- **Primary:** PostgreSQL 15+ with JSONB for document storage
- **Rationale:** ACID compliance, excellent JSON support, mature ecosystem
- **ORM:** Prisma for type-safe database access

**AI/LLM Integration:**

- **Primary Library:** Vercel AI SDK for multi-provider support
- **Model Routing:** Claude Code Router for intelligent LLM selection and cost optimization
- **Supported Providers:** OpenAI, Anthropic, Google AI, DeepSeek, Ollama, user BYOLLM
- **Rationale:** Provider agnostic, excellent streaming support, intelligent task-based routing

**Container Orchestration:** Kubernetes

- **Rationale:** Industry standard, excellent scaling, cloud agnostic
- **Development:** Docker Compose for local development

**Cloud Provider:** AWS (Primary)

- **Compute:** EKS for Kubernetes orchestration
- **Storage:** S3 for file storage, RDS for PostgreSQL
- **CDN:** CloudFront for global content delivery

### Development Tools

**Package Management:** pnpm

- **Rationale:** Faster installs, disk space efficiency, strict dependency management

**Code Quality:**

- **Linting:** ESLint with TypeScript rules
- **Formatting:** Prettier
- **Testing:** Vitest for unit tests, Playwright for E2E

**CI/CD:** GitHub Actions

- **Deployment:** Automated deployment to AWS EKS
- **Quality Gates:** Tests, linting, security scans

---

## System Architecture

### Platform Architecture (Traditional Microservices)

#### V0-Clone Foundation Architecture

The no-code platform itself builds upon the proven V0-Clone architecture, extending it with BMAD methodology, Memory Pickle MCP integration, and business-focused workflows:

```
┌─────────────────────────────────────────────────────────────────┐
│                    Next.js 15 Frontend                          │
│      (V0-Clone UI + BMAD Workflow + Multi-Project Management)   │
└─────────────────────┬───────────────────────────────────────────┘
                      │
    ┌─────────────────┼─────────────────┬─────────────────┐
    │                 │                 │                 │
┌───▼────┐    ┌──────▼──────┐    ┌─────▼─────┐    ┌─────▼─────┐
│Convex  │    │   Inngest   │    │ VibeKit   │    │Memory     │
│Real-time│    │Background   │    │ AI Agents │    │Pickle MCP │
│State   │    │ Jobs        │    │(Execution)│    │(Context)  │
└────────┘    └─────────────┘    └───────────┘    └───────────┘
```

#### BMAD Integration Layer with Memory Pickle MCP

The BMAD methodology is implemented as an orchestration layer on top of the V0-Clone foundation, enhanced with Memory Pickle MCP for context management and multi-project support:

```
┌─────────────────────────────────────────────────────────────────┐
│                    BMAD Orchestration Layer                     │
│  (Phase Management, Agent Coordination, Multi-Project Context)  │
└─────────────────────┬───────────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────────┐
│                Memory Pickle MCP Integration                    │
│   (Project Context, Session Management, Agent Handoffs)        │
└─────────────────────┬───────────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────────┐
│                    V0-Clone Foundation                          │
│  (UI Components, Real-time, Auth, Sessions, Templates)          │
└─────────────────────────────────────────────────────────────────┘
```

#### Enhanced Memory Pickle MCP Architecture with Semantic Search

**Dual-Layer Learning Architecture:**

The Enhanced Memory Pickle MCP implements a dual-layer architecture separating user-specific session data from platform-wide learning intelligence:

1. **User Layer** - Personal project management and session memory
2. **Platform Layer** - Cross-user learning, patterns, and intelligence

```typescript
interface EnhancedMemoryPickle extends MemoryPickleCore {
  // ===== USER LAYER: Personal Session Management =====
  // Existing Memory Pickle tools (13 tools) - User-specific
  recall_state(): Promise<ProjectState>;
  create_project(params: ProjectParams): Promise<Project>;
  create_task(params: TaskParams): Promise<Task>;
  remember_this(params: MemoryParams): Promise<Memory>;
  recall_context(params: ContextQuery): Promise<Memory[]>;

  // User-specific semantic search within personal projects
  semantic_search_personal(
    params: PersonalSearchParams
  ): Promise<SemanticResult[]>;

  // ===== PLATFORM LAYER: Cross-User Learning Intelligence =====
  // Platform-wide learning from ALL users (anonymized)
  learn_from_mistake(
    params: AnonymizedMistakeParams
  ): Promise<PlatformLearningEntry>;
  recall_similar_issues(
    params: PlatformIssueQuery
  ): Promise<PlatformSimilarIssue[]>;
  store_bug_fix(params: AnonymizedBugFixParams): Promise<PlatformBugFixEntry>;

  // Cross-user pattern recognition and insights
  get_platform_insights(projectType: string): Promise<PlatformInsights>;
  get_tech_stack_lessons(stack: string[]): Promise<PlatformTechStackLessons>;
  predict_potential_issues(
    context: ProjectContext
  ): Promise<PlatformPotentialIssue[]>;

  // Platform-wide semantic search across all anonymized learnings
  semantic_search_platform(
    params: PlatformSearchParams
  ): Promise<PlatformSemanticResult[]>;
}

// ===== USER LAYER INTERFACES =====
interface PersonalSearchParams {
  query: string;
  project_id?: string;
  importance?: ("critical" | "high" | "medium" | "low")[];
  limit?: number;
  similarity_threshold?: number;
  context_type?: "personal_note" | "project_decision" | "task_context";
}

// ===== PLATFORM LAYER INTERFACES =====
interface PlatformSearchParams {
  query: string;
  tech_stack?: string[];
  project_type?: string;
  phase?: BMADPhase;
  importance?: ("critical" | "high" | "medium" | "low")[];
  limit?: number;
  similarity_threshold?: number;
  context_type?: "bug_fix" | "pattern" | "mistake" | "solution";

  // NEW: Temporal filtering
  max_age_days?: number; // Only return memories newer than X days
  min_relevance_date?: Date; // Only return memories after this date
  exclude_deprecated?: boolean; // Exclude memories marked as deprecated
  tech_stack_version_aware?: boolean; // Consider tech stack version compatibility
}

interface AnonymizedMistakeParams {
  phase: BMADPhase;
  error_description: string;
  solution_applied: string;
  tech_stack: string[];
  project_type: string;
  severity: "critical" | "high" | "medium" | "low";
  prevention_strategy?: string;
  // NO user_id or project_id - completely anonymized
  anonymized_context: {
    project_size: "small" | "medium" | "large";
    team_size: "solo" | "small" | "medium" | "large";
    timeline: "days" | "weeks" | "months";
  };
}

interface AnonymizedBugFixParams {
  bug_description: string;
  root_cause: string;
  solution_steps: string[];
  tech_stack: string[];
  files_affected: string[]; // Anonymized file patterns
  testing_approach: string;
  prevention_measures: string[];
  // NO user_id or project_id - completely anonymized
  anonymized_context: {
    project_complexity: "simple" | "moderate" | "complex";
    bug_severity: "critical" | "high" | "medium" | "low";
    resolution_time: "minutes" | "hours" | "days";
  };
}

interface PlatformIssueQuery {
  phase?: BMADPhase;
  tech_stack: string[];
  project_type: string;
  severity?: ("critical" | "high" | "medium" | "low")[];
  limit?: number;
}

// Platform-level learning results
interface PlatformLearningEntry {
  id: string;
  phase: BMADPhase;
  pattern_type: "mistake" | "solution" | "best_practice";
  tech_stack: string[];
  project_type: string;
  confidence_score: number; // Based on frequency and success rate
  anonymized_examples: AnonymizedExample[];
  prevention_strategies: string[];

  // NEW: Temporal Management
  created_at: Date;
  updated_at: Date;
  last_validated_at?: Date; // When this learning was last confirmed as still relevant
  usage_count: number; // How often this learning has been applied
  success_rate: number; // Success rate when this learning is applied
  recent_success_rate: number; // Success rate in last 30 days

  // Memory aging and relevance
  relevance_score: number; // Calculated based on recency, usage, and success
  is_deprecated: boolean; // Manually marked as outdated
  deprecation_reason?: string;
  superseded_by?: string; // ID of newer learning that replaces this one

  // Tech stack version awareness
  tech_stack_versions?: Record<string, string>; // e.g., {"react": "18.x", "node": "20.x"}
  compatible_versions?: Record<string, string[]>; // Compatible version ranges

  // Temporal context
  temporal_context: {
    era: "legacy" | "current" | "emerging"; // Technology era classification
    trend_direction: "declining" | "stable" | "growing"; // Usage trend
    estimated_shelf_life_months?: number; // How long this learning stays relevant
  };
}

interface PlatformSimilarIssue {
  issue_pattern: string;
  common_causes: string[];
  proven_solutions: string[];
  tech_stack: string[];
  project_types: string[];
  occurrence_frequency: number;
  average_resolution_time: string;
  prevention_strategies: string[];
  confidence_score: number;
}
```

**VibeKit Memory Manager (Enhanced Wrapper Layer):**

```typescript
interface VibeKitMemoryManager {
  userId: string;
  userDatabase: UserDatabase;
  embeddingService: EmbeddingService;
  vectorStore: VectorStore;

  // User session management
  getUserSession(): Promise<MemoryPickleSession>;
  createProject(params: ProjectCreationParams): Promise<UserProject>;
  getUserProjects(): Promise<UserProject[]>;
  switchProject(projectId: string): Promise<void>;

  // Enhanced learning capabilities
  getUserInsights(): Promise<UserLearningContext>;
  getProjectTypeInsights(type: string): Promise<ProjectTypeInsights>;
  getTechStackInsights(stack: string[]): Promise<TechStackInsights>;

  // NEW: Semantic learning features
  learnFromUserSession(session: CompletedSession): Promise<void>;
  predictIssuesForProject(context: ProjectContext): Promise<PredictedIssue[]>;
  getSimilarSuccessfulProjects(
    context: ProjectContext
  ): Promise<SuccessPattern[]>;
  getRecommendedApproaches(
    phase: BMADPhase,
    context: ProjectContext
  ): Promise<Recommendation[]>;

  // Session persistence with learning
  saveUserSession(): Promise<void>;
  restoreUserSession(): Promise<void>;
  exportLearnings(): Promise<LearningExport>;
}
```

**Platform-Level Learning Architecture:**

```
┌─────────────────────────────────────────────────────────────────┐
│                    PLATFORM LEARNING LAYER                     │
│     (Cross-User Intelligence, Anonymized Patterns & Fixes)     │
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │   Semantic  │  │   Pattern   │  │   Bug Fix   │             │
│  │   Search    │  │ Recognition │  │  Database   │             │
│  │   Engine    │  │   Engine    │  │             │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
└─────────────────────┬───────────────────────────────────────────┘
                      │ Anonymized Learning Data
                      │ (No User IDs, Project IDs)
┌─────────────────────▼───────────────────────────────────────────┐
│                VibeKit Memory Manager (Wrapper)                 │
│         (User Context, Session Management, Privacy)            │
└─────────────────────┬───────────────────────────────────────────┘
                      │ User-Specific Data Only
    ┌─────────────────┼─────────────────┬─────────────────┐
    │                 │                 │                 │
┌───▼────┐    ┌──────▼──────┐    ┌─────▼─────┐    ┌─────▼─────┐
│User A  │    │   User B    │    │  User C   │    │PostgreSQL │
│Personal│    │   Personal  │    │  Personal │    │User Data  │
│Session │    │   Session   │    │  Session  │    │(Isolated) │
└────────┘    └─────────────┘    └───────────┘    └───────────┘
```

**Cross-User Learning Flow:**

```
User A encounters bug → Anonymized learning stored in Platform Layer
                     ↓
User B starts similar project → Platform suggests prevention strategy
                              ↓
User C gets proactive warning → Bug prevented before it occurs
```

**Privacy & Learning Strategy:**

✅ **Complete User Isolation** - Personal projects and data remain private
✅ **Anonymized Learning** - Only patterns and solutions shared, no user data
✅ **Cross-User Intelligence** - User B learns from User A's mistakes
✅ **Platform-Wide Improvement** - Every user benefits from collective knowledge
✅ **Privacy Preserved** - No way to trace learnings back to original users

**Temporal Memory Management Architecture:**

```typescript
// Enhanced Platform Learning Service with Temporal Management
class PlatformLearningService {
  constructor(
    private memoryAging: MemoryAgingService,
    private versionTracker: TechStackVersionTracker,
    private relevanceCalculator: RelevanceCalculator
  ) {}

  async storeLearningFromUser(userId: string, learning: UserLearning) {
    // 1. Extract anonymized pattern
    const anonymizedLearning = this.anonymizeLearning(learning);

    // 2. Add temporal context
    const temporalContext = await this.generateTemporalContext(learning);

    // 3. Store in platform layer with temporal metadata
    const storedLearning = await this.platformStore.store({
      pattern: anonymizedLearning.pattern,
      solution: anonymizedLearning.solution,
      tech_stack: learning.techStack,
      project_type: learning.projectType,

      // Temporal metadata
      created_at: new Date(),
      updated_at: new Date(),
      tech_stack_versions: await this.versionTracker.getCurrentVersions(
        learning.techStack
      ),
      temporal_context: temporalContext,
      estimated_shelf_life_months: this.calculateShelfLife(
        learning.techStack,
        learning.projectType
      ),

      // Initial relevance scores
      relevance_score: 1.0, // New learnings start with max relevance
      confidence_score: this.calculateInitialConfidence(learning),
      usage_count: 0,
      success_rate: 1.0, // Assume success until proven otherwise
      recent_success_rate: 1.0,

      // NO userId, projectId, or personal data
    });

    // 4. Update pattern recognition
    await this.updatePatternRecognition(anonymizedLearning);

    return storedLearning;
  }

  // Enhanced search with temporal filtering
  async getPlatformInsights(
    context: ProjectContext
  ): Promise<PlatformInsights> {
    // Apply temporal filters to ensure fresh, relevant data
    const temporalFilters = {
      max_age_days: 365, // Default: only consider learnings from last year
      exclude_deprecated: true,
      tech_stack_version_aware: true,
      min_relevance_score: 0.3, // Only return reasonably relevant learnings
    };

    // Search platform-wide learnings with temporal awareness
    const relevantLearnings = await this.platformStore.search({
      tech_stack: context.techStack,
      project_type: context.projectType,
      temporal_filters: temporalFilters,
      // Returns only fresh, relevant anonymized patterns
    });

    // Filter out stale or incompatible learnings
    const freshLearnings = await this.filterByFreshness(
      relevantLearnings,
      context
    );

    return {
      preventionStrategies: freshLearnings.preventionStrategies,
      commonPitfalls: freshLearnings.commonPitfalls,
      bestPractices: freshLearnings.bestPractices,
      temporalReliability: this.calculateTemporalReliability(freshLearnings),
      // NO reference to original users
    };
  }

  // Memory aging and maintenance
  async performMemoryMaintenance(): Promise<MaintenanceReport> {
    const report = {
      deprecated_count: 0,
      updated_count: 0,
      validated_count: 0,
      purged_count: 0,
    };

    // 1. Age all memories and update relevance scores
    const allLearnings = await this.platformStore.getAllLearnings();

    for (const learning of allLearnings) {
      const updatedLearning = await this.memoryAging.ageLearning(learning);

      // Check if learning should be deprecated
      if (this.shouldDeprecate(updatedLearning)) {
        await this.deprecateLearning(
          updatedLearning.id,
          "Outdated technology stack"
        );
        report.deprecated_count++;
      }

      // Update relevance scores
      if (updatedLearning.relevance_score !== learning.relevance_score) {
        await this.platformStore.updateRelevanceScore(
          learning.id,
          updatedLearning.relevance_score
        );
        report.updated_count++;
      }
    }

    // 2. Validate high-usage learnings
    const highUsageLearnings = allLearnings.filter((l) => l.usage_count > 10);
    for (const learning of highUsageLearnings) {
      const validationResult = await this.validateLearning(learning);
      if (validationResult.needsUpdate) {
        await this.updateLearning(learning.id, validationResult.updates);
        report.validated_count++;
      }
    }

    // 3. Purge completely obsolete learnings
    const obsoleteLearnings = allLearnings.filter(
      (l) =>
        l.relevance_score < 0.1 &&
        l.is_deprecated &&
        this.daysSince(l.updated_at) > 180
    );

    for (const learning of obsoleteLearnings) {
      await this.platformStore.purgeLearning(learning.id);
      report.purged_count++;
    }

    return report;
  }

  private async generateTemporalContext(
    learning: UserLearning
  ): Promise<TemporalContext> {
    const techStackEra = await this.versionTracker.classifyTechStackEra(
      learning.techStack
    );
    const trendDirection = await this.versionTracker.getTrendDirection(
      learning.techStack
    );

    return {
      era: techStackEra,
      trend_direction: trendDirection,
      estimated_shelf_life_months: this.calculateShelfLife(
        learning.techStack,
        learning.projectType
      ),
    };
  }

  private calculateShelfLife(techStack: string[], projectType: string): number {
    // Different technologies have different shelf lives
    const shelfLifeMap = {
      react: 24, // React patterns stay relevant for ~2 years
      vue: 18, // Vue patterns for ~1.5 years
      angular: 12, // Angular changes more frequently
      node: 36, // Node.js patterns are more stable
      python: 48, // Python patterns very stable
      javascript: 60, // Core JS patterns very stable
    };

    const minShelfLife = Math.min(
      ...techStack.map(
        (tech) => shelfLifeMap[tech.toLowerCase()] || 12 // Default 1 year
      )
    );

    // Adjust based on project type
    const projectTypeMultiplier = {
      "e-commerce": 0.8, // Fast-changing domain
      blog: 1.2, // Stable domain
      dashboard: 1.0, // Standard
      api: 1.5, // More stable
    };

    return Math.round(
      minShelfLife * (projectTypeMultiplier[projectType] || 1.0)
    );
  }
}

// Memory Aging Service
class MemoryAgingService {
  async ageLearning(
    learning: PlatformLearningEntry
  ): Promise<PlatformLearningEntry> {
    const ageInDays = this.daysSince(learning.created_at);
    const lastUpdateAgeInDays = this.daysSince(learning.updated_at);

    // Calculate age-based relevance decay
    const ageDecayFactor = this.calculateAgeDecay(
      ageInDays,
      learning.estimated_shelf_life_months
    );

    // Calculate usage-based relevance boost
    const usageBoost = this.calculateUsageBoost(
      learning.usage_count,
      learning.recent_success_rate
    );

    // Calculate tech stack relevance (are the technologies still current?)
    const techStackRelevance = await this.calculateTechStackRelevance(
      learning.tech_stack_versions
    );

    // Combined relevance score
    const newRelevanceScore = Math.max(
      0,
      Math.min(
        1,
        learning.relevance_score *
          ageDecayFactor *
          usageBoost *
          techStackRelevance
      )
    );

    return {
      ...learning,
      relevance_score: newRelevanceScore,
      updated_at: new Date(),
    };
  }

  private calculateAgeDecay(
    ageInDays: number,
    shelfLifeMonths: number
  ): number {
    const shelfLifeDays = shelfLifeMonths * 30;

    if (ageInDays <= shelfLifeDays * 0.5) {
      return 1.0; // Full relevance for first half of shelf life
    } else if (ageInDays <= shelfLifeDays) {
      // Linear decay in second half of shelf life
      return (
        1.0 - ((ageInDays - shelfLifeDays * 0.5) / (shelfLifeDays * 0.5)) * 0.5
      );
    } else {
      // Exponential decay after shelf life
      const excessDays = ageInDays - shelfLifeDays;
      return 0.5 * Math.exp(-excessDays / (shelfLifeDays * 0.5));
    }
  }

  private calculateUsageBoost(
    usageCount: number,
    recentSuccessRate: number
  ): number {
    // Frequently used and successful learnings get relevance boost
    const usageBoost = Math.min(1.2, 1 + (usageCount / 100) * 0.2);
    const successBoost = 0.8 + recentSuccessRate * 0.4; // 0.8 to 1.2 range

    return usageBoost * successBoost;
  }

  private async calculateTechStackRelevance(
    techStackVersions: Record<string, string>
  ): Promise<number> {
    // Check if the tech stack versions are still current
    let totalRelevance = 0;
    let techCount = 0;

    for (const [tech, version] of Object.entries(techStackVersions)) {
      const currentVersion = await this.versionTracker.getCurrentVersion(tech);
      const versionRelevance = this.compareVersions(version, currentVersion);
      totalRelevance += versionRelevance;
      techCount++;
    }

    return techCount > 0 ? totalRelevance / techCount : 1.0;
  }

  private daysSince(date: Date): number {
    return Math.floor((Date.now() - date.getTime()) / (1000 * 60 * 60 * 24));
  }
}

// Enhanced search with temporal awareness
interface TemporalSearchOptions {
  max_age_days?: number;
  min_relevance_score?: number;
  exclude_deprecated?: boolean;
  tech_stack_version_aware?: boolean;
  prefer_recent?: boolean; // Boost recent learnings in results
}

// Temporal validation and maintenance
interface MaintenanceReport {
  deprecated_count: number;
  updated_count: number;
  validated_count: number;
  purged_count: number;
  temporal_reliability_score: number;
}
```

## Claude Code Router Integration for Multi-Model LLM Management

### Overview

The Claude Code Router provides intelligent LLM routing and model specialization across all three development phases of the BMAD platform. This enables cost optimization, performance specialization, and unified CLI experience for developers.

### Architecture Integration

```
┌─────────────────────────────────────────────────────────────────┐
│                    BMAD Development Phases                      │
│  (Phase 1: Setup, Phase 2: Development, Phase 3: Production)   │
└─────────────────────┬───────────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────────┐
│                Claude Code Router Layer                         │
│        (Intelligent Model Routing & Cost Optimization)         │
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │   Agent     │  │    Task     │  │    Cost     │             │
│  │Specialization│  │   Routing   │  │Optimization │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
└─────────────────────┬───────────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────────┐
│                Multi-Provider LLM Layer                         │
│  OpenRouter | DeepSeek | Ollama | Gemini | Anthropic | OpenAI  │
└─────────────────────────────────────────────────────────────────┘
```

### Phase-Based Implementation Strategy

#### **Phase 1: Basic Setup (30 minutes)**

**Goal:** Replace multiple CLI tools with unified Claude Code Router interface

**Configuration:**

```json
{
  "APIKEY": "your-secret-key",
  "LOG": true,
  "Providers": [
    {
      "name": "openrouter",
      "api_base_url": "https://openrouter.ai/api/v1/chat/completions",
      "api_key": "sk-xxx",
      "models": [
        "anthropic/claude-3.5-sonnet",
        "google/gemini-2.5-pro-preview",
        "anthropic/claude-3.7-sonnet:thinking"
      ],
      "transformer": { "use": ["openrouter"] }
    },
    {
      "name": "deepseek",
      "api_base_url": "https://api.deepseek.com/chat/completions",
      "api_key": "sk-xxx",
      "models": ["deepseek-chat", "deepseek-reasoner"],
      "transformer": {
        "use": ["deepseek"],
        "deepseek-chat": { "use": ["tooluse"] }
      }
    },
    {
      "name": "ollama",
      "api_base_url": "http://localhost:11434/v1/chat/completions",
      "api_key": "ollama",
      "models": ["qwen2.5-coder:latest"]
    }
  ],
  "Router": {
    "default": "deepseek,deepseek-chat",
    "background": "ollama,qwen2.5-coder:latest",
    "think": "deepseek,deepseek-reasoner",
    "longContext": "openrouter,google/gemini-2.5-pro-preview"
  }
}
```

**Benefits:**

- ✅ Single CLI command (`ccr code`) instead of multiple terminals
- ✅ Dynamic model switching with `/model provider,model`
- ✅ Cost optimization with cheaper models for background tasks
- ✅ Immediate workflow efficiency improvement

#### **Phase 2: Advanced Task-Based Routing (1 hour)**

**Goal:** Implement intelligent routing based on BMAD workflow phases and task types

**Enhanced Configuration:**

```json
{
  "Router": {
    "default": "deepseek,deepseek-chat",
    "background": "ollama,qwen2.5-coder:latest",
    "think": "openrouter,anthropic/claude-3.7-sonnet:thinking",
    "longContext": "openrouter,google/gemini-2.5-pro-preview",
    "webSearch": "openrouter,google/gemini-2.5-flash:online",

    // BMAD-specific routing
    "architecture": "openrouter,anthropic/claude-3.5-sonnet",
    "development": "deepseek,deepseek-chat",
    "testing": "ollama,qwen2.5-coder:latest",
    "documentation": "openrouter,google/gemini-2.5-flash"
  }
}
```

**Task-Based Intelligence:**

- **Architecture Phase:** Premium models for complex system design
- **Development Phase:** Balanced cost/performance for code generation
- **Testing Phase:** Local models for test generation and validation
- **Documentation:** Fast, cost-effective models for documentation

#### **Phase 3: Custom BMAD Agent Specialization (TODO)**

**Goal:** Route different BMAD agents to specialized LLMs based on their strengths

**Custom Router Implementation:**

```javascript
// ~/.claude-code-router/bmad-agent-router.js
module.exports = async function router(req, config) {
  const userMessage = req.body.messages.find((m) => m.role === "user")?.content;
  const systemMessage = req.body.messages.find(
    (m) => m.role === "system"
  )?.content;

  // Detect BMAD agent type from system message or context
  const agentType = detectBMADAgent(systemMessage, userMessage);

  switch (agentType) {
    case "architect":
      // Use Claude 3.5 Sonnet for architectural decisions
      return "openrouter,anthropic/claude-3.5-sonnet";

    case "dev":
      // Use DeepSeek for code generation (cost-effective, good at coding)
      return "deepseek,deepseek-chat";

    case "qa":
      // Use local Ollama for test generation (cost-effective)
      return "ollama,qwen2.5-coder:latest";

    case "pm":
      // Use Gemini for project management (good at structured thinking)
      return "openrouter,google/gemini-2.5-pro";

    case "reasoning":
      // Use DeepSeek R1 for complex reasoning tasks
      return "deepseek,deepseek-reasoner";

    default:
      // Fallback to default router
      return null;
  }
};

function detectBMADAgent(systemMessage, userMessage) {
  // Agent detection logic based on system prompts and context
  if (
    systemMessage?.includes("architect") ||
    systemMessage?.includes("system design")
  ) {
    return "architect";
  }
  if (systemMessage?.includes("dev") || userMessage?.includes("implement")) {
    return "dev";
  }
  if (systemMessage?.includes("qa") || userMessage?.includes("test")) {
    return "qa";
  }
  if (systemMessage?.includes("pm") || userMessage?.includes("project")) {
    return "pm";
  }
  if (userMessage?.includes("analyze") || userMessage?.includes("reason")) {
    return "reasoning";
  }
  return "default";
}
```

### BMAD Agent Specialization Matrix

| BMAD Agent           | Specialized LLM   | Rationale                                       | Cost Impact            |
| -------------------- | ----------------- | ----------------------------------------------- | ---------------------- |
| **Architect Agent**  | Claude 3.5 Sonnet | Superior architectural reasoning, system design | High cost, high value  |
| **Dev Agent**        | DeepSeek Chat     | Excellent code generation, cost-effective       | Low cost, high volume  |
| **QA Agent**         | Ollama (Local)    | Test generation, validation, zero API cost      | Zero cost              |
| **PM Agent**         | Gemini 2.5 Pro    | Structured thinking, project planning           | Medium cost            |
| **Reasoning Tasks**  | DeepSeek R1       | Complex problem solving, step-by-step analysis  | Medium cost            |
| **Background Tasks** | Ollama (Local)    | File processing, simple transformations         | Zero cost              |
| **Long Context**     | Gemini 2.5 Pro    | Large codebase analysis, documentation          | High cost, specialized |

### Cost Optimization Strategy

#### **Intelligent Cost Management:**

```typescript
interface CostOptimizationConfig {
  // Route expensive operations to premium models
  high_value_tasks: {
    models: ["anthropic/claude-3.5-sonnet", "google/gemini-2.5-pro"];
    triggers: ["architecture", "complex_reasoning", "critical_decisions"];
  };

  // Route routine operations to cost-effective models
  routine_tasks: {
    models: ["deepseek-chat", "ollama/qwen2.5-coder"];
    triggers: ["code_generation", "testing", "documentation"];
  };

  // Route background operations to free local models
  background_tasks: {
    models: ["ollama/qwen2.5-coder"];
    triggers: ["file_processing", "simple_transformations"];
  };
}
```

#### **Expected Cost Savings:**

- **80% cost reduction** on routine development tasks
- **Free local processing** for background operations
- **Premium model usage** only for high-value architectural decisions
- **Dynamic scaling** based on project complexity and budget

### Integration with Enhanced Memory Pickle

#### **Learning-Informed Model Selection:**

```typescript
class IntelligentModelRouter {
  constructor(
    private memoryPickle: EnhancedMemoryPickle,
    private claudeRouter: ClaudeCodeRouter
  ) {}

  async selectOptimalModel(
    task: BMADTask,
    context: ProjectContext
  ): Promise<ModelSelection> {
    // Get historical performance data for similar tasks
    const historicalPerformance =
      await this.memoryPickle.semantic_search_platform({
        query: `${task.type} ${context.techStack.join(" ")} model performance`,
        context_type: "pattern",
        limit: 10,
      });

    // Analyze which models performed best for similar tasks
    const modelPerformanceAnalysis = this.analyzeModelPerformance(
      historicalPerformance
    );

    // Select optimal model based on:
    // 1. Historical performance for similar tasks
    // 2. Current cost constraints
    // 3. Task complexity requirements
    const optimalModel = this.selectModel({
      taskComplexity: task.complexity,
      historicalPerformance: modelPerformanceAnalysis,
      costConstraints: context.budget,
      qualityRequirements: task.qualityThreshold,
    });

    return {
      provider: optimalModel.provider,
      model: optimalModel.model,
      rationale: optimalModel.reasoning,
      expectedCost: optimalModel.estimatedCost,
      confidenceScore: optimalModel.confidence,
    };
  }
}
```

### Development Workflow Enhancement

#### **Before Claude Code Router:**

```bash
# Multiple terminals and CLIs
Terminal 1: claude code
Terminal 2: gemini cli
Terminal 3: opencode
# Context switching between different interfaces
# Manual model selection
# Inconsistent authentication
```

#### **After Claude Code Router:**

```bash
# Single unified interface
Terminal 1: ccr code

# Dynamic model switching within same session
/model openrouter,anthropic/claude-3.5-sonnet  # For architecture
/model deepseek,deepseek-chat                  # For development
/model ollama,qwen2.5-coder:latest            # For testing

# Automatic routing based on task type
# Consistent interface across all models
# Centralized authentication and configuration
```

### Implementation Roadmap

#### **Phase 1: Basic Setup** ✅ **Ready to Implement**

- [ ] Install Claude Code Router
- [ ] Configure basic multi-provider setup
- [ ] Test unified CLI interface
- [ ] Validate model switching functionality

#### **Phase 2: Advanced Routing** ⏳ **Next Sprint**

- [ ] Implement task-based routing rules
- [ ] Configure cost optimization strategies
- [ ] Add BMAD workflow-specific routes
- [ ] Test performance and cost metrics

#### **Phase 3: BMAD Agent Specialization** 📋 **TODO - Future Enhancement**

- [ ] Develop custom router logic for BMAD agents
- [ ] Implement agent detection algorithms
- [ ] Create specialization matrix configuration
- [ ] Integrate with Enhanced Memory Pickle for learning-informed routing
- [ ] Add performance monitoring and optimization
- [ ] Implement cost tracking and budget controls

### Benefits for BMAD Platform

#### **Developer Experience:**

✅ **Unified Interface** - Single CLI for all models and providers
✅ **Intelligent Routing** - Automatic model selection based on task type
✅ **Cost Optimization** - Significant reduction in LLM costs
✅ **Performance Specialization** - Right model for the right task

#### **Platform Intelligence:**

✅ **Agent Specialization** - Each BMAD agent uses optimal LLM
✅ **Learning Integration** - Historical performance informs model selection
✅ **Adaptive Routing** - System learns and improves over time
✅ **Budget Management** - Automatic cost control and optimization

#### **Operational Benefits:**

✅ **Reduced Complexity** - Single configuration for all providers
✅ **Centralized Management** - Unified authentication and monitoring
✅ **Scalable Architecture** - Easy to add new providers and models
✅ **Future-Proof Design** - Adapts to new models and providers

## Tech Stack Management & Validation System

### Overview

The BMAD platform implements intelligent tech stack management with default configurations, user customization capabilities, and comprehensive validation during the architecture phase to ensure all requirements can be supported.

### Tech Stack Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    Tech Stack Management Layer                  │
│  (Defaults, User Preferences, Validation, Compatibility)       │
└─────────────────────┬───────────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────────┐
│                Platform Default Stack                           │
│     (Proven, Production-Ready, No-Code Optimized)              │
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │  Frontend   │  │   Backend   │  │Infrastructure│             │
│  │   Stack     │  │    Stack    │  │    Stack    │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
└─────────────────────┬───────────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────────┐
│                User Override Layer                              │
│        (Custom Preferences, Project-Specific Choices)          │
└─────────────────────┬───────────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────────┐
│              Architecture Validation Engine                     │
│    (Requirement Analysis, Compatibility Checks, Warnings)      │
└─────────────────────────────────────────────────────────────────┘
```

### Default Tech Stack Configuration

#### **Platform Default Stack (Production-Ready)**

```typescript
interface PlatformDefaultStack {
  frontend: {
    framework: "Next.js 15";
    language: "TypeScript 5.0+";
    styling: "Tailwind CSS + shadcn/ui";
    state_management: "Convex (real-time)";
    authentication: "NextAuth.js";
    deployment: "Vercel";
  };

  backend: {
    runtime: "Node.js 20+ LTS";
    framework: "Fastify + TypeScript";
    database: "PostgreSQL 15+ with JSONB";
    orm: "Prisma";
    background_jobs: "Inngest";
    api_style: "REST + GraphQL (optional)";
  };

  infrastructure: {
    hosting: "AWS EKS";
    database_hosting: "AWS RDS PostgreSQL";
    file_storage: "AWS S3";
    cdn: "CloudFront";
    monitoring: "Sentry + DataDog";
    ci_cd: "GitHub Actions";
  };

  ai_integration: {
    primary_library: "Vercel AI SDK";
    model_routing: "Claude Code Router";
    memory_system: "Enhanced Memory Pickle MCP";
    supported_providers: ["OpenAI", "Anthropic", "DeepSeek", "Ollama"];
  };

  development: {
    package_manager: "pnpm";
    code_quality: ["ESLint", "Prettier", "TypeScript strict"];
    testing: ["Vitest", "Playwright"];
    containerization: "Docker + Docker Compose";
  };
}
```

#### **Rationale for Default Choices:**

**Frontend Stack:**

- **Next.js 15**: Full-stack capabilities, excellent developer experience, production-ready
- **TypeScript**: Type safety, better developer experience, reduced runtime errors
- **Tailwind + shadcn/ui**: Rapid UI development, consistent design system
- **Convex**: Real-time state management, perfect for collaborative no-code platform

**Backend Stack:**

- **Node.js + Fastify**: High performance, excellent LLM integration libraries
- **PostgreSQL + JSONB**: ACID compliance, excellent JSON support, mature ecosystem
- **Prisma**: Type-safe database access, excellent developer experience
- **Inngest**: Reliable background job processing, great for AI workflows

**Infrastructure:**

- **AWS**: Industry standard, excellent scaling, comprehensive services
- **Kubernetes**: Container orchestration, cloud agnostic, production-ready
- **GitHub Actions**: Integrated CI/CD, excellent ecosystem

### User Tech Stack Override System

#### **Override Hierarchy:**

```typescript
interface TechStackResolution {
  // Priority order (highest to lowest)
  1: "Project-specific user selection";
  2: "User global preferences";
  3: "Platform defaults";
}

interface UserTechStackPreferences {
  user_id: string;
  global_preferences: {
    frontend_framework?: "Next.js" | "React + Vite" | "Vue.js" | "Svelte";
    backend_framework?: "Fastify" | "Express" | "Hono" | "Elysia";
    database?: "PostgreSQL" | "MySQL" | "SQLite" | "MongoDB";
    hosting_preference?: "AWS" | "Vercel" | "Railway" | "Fly.io";
    styling_approach?: "Tailwind" | "CSS Modules" | "Styled Components";
  };

  project_overrides: {
    [project_id: string]: {
      frontend?: Partial<FrontendStack>;
      backend?: Partial<BackendStack>;
      infrastructure?: Partial<InfrastructureStack>;
      rationale?: string; // Why this override was chosen
    };
  };

  created_at: Date;
  updated_at: Date;
}
```

#### **User Preference Management:**

```typescript
class TechStackManager {
  async getUserPreferences(user_id: string): Promise<UserTechStackPreferences> {
    return await this.database.getUserTechStackPreferences(user_id);
  }

  async updateGlobalPreferences(
    user_id: string,
    preferences: Partial<GlobalTechStackPreferences>
  ): Promise<void> {
    await this.database.updateUserGlobalPreferences(user_id, preferences);

    // Log preference change for learning
    await this.memoryPickle.remember_this({
      content: `User updated global tech stack preferences: ${JSON.stringify(
        preferences
      )}`,
      importance: "medium",
      tags: ["tech_stack", "user_preferences"],
    });
  }

  async setProjectOverride(
    user_id: string,
    project_id: string,
    overrides: ProjectTechStackOverride,
    rationale: string
  ): Promise<void> {
    await this.database.setProjectTechStackOverride(
      user_id,
      project_id,
      overrides,
      rationale
    );

    // Store learning for future recommendations
    await this.memoryPickle.learn_from_mistake({
      phase: "architecture",
      error_description: `Default stack insufficient for project requirements`,
      solution_applied: `Override: ${JSON.stringify(overrides)}`,
      tech_stack: Object.values(overrides).flat(),
      project_type: await this.getProjectType(project_id),
      severity: "medium",
      prevention_strategy: `Consider ${rationale} for similar projects`,
    });
  }

  async resolveProjectTechStack(
    user_id: string,
    project_id: string
  ): Promise<ResolvedTechStack> {
    const userPreferences = await this.getUserPreferences(user_id);
    const projectOverrides = userPreferences.project_overrides[project_id];
    const globalPreferences = userPreferences.global_preferences;
    const platformDefaults = this.getPlatformDefaults();

    // Merge in priority order
    return this.mergeTechStacks([
      projectOverrides,
      globalPreferences,
      platformDefaults,
    ]);
  }
}
```

### Architecture Phase Validation Engine

#### **Requirement-to-Tech-Stack Validation:**

```typescript
class TechStackValidator {
  async validateTechStackForRequirements(
    requirements: ProjectRequirements,
    proposedStack: ResolvedTechStack
  ): Promise<ValidationResult> {
    const validationChecks = [
      await this.validateScalabilityRequirements(requirements, proposedStack),
      await this.validatePerformanceRequirements(requirements, proposedStack),
      await this.validateSecurityRequirements(requirements, proposedStack),
      await this.validateIntegrationRequirements(requirements, proposedStack),
      await this.validateDeploymentRequirements(requirements, proposedStack),
      await this.validateBudgetConstraints(requirements, proposedStack),
      await this.validateTeamExpertise(requirements, proposedStack),
    ];

    return this.consolidateValidationResults(validationChecks);
  }

  private async validateScalabilityRequirements(
    requirements: ProjectRequirements,
    stack: ResolvedTechStack
  ): Promise<ValidationCheck> {
    const scalabilityNeeds = requirements.scalability;

    // Check if database can handle expected load
    if (
      scalabilityNeeds.expected_users > 100000 &&
      stack.backend.database === "SQLite"
    ) {
      return {
        type: "scalability",
        severity: "critical",
        issue: "SQLite cannot handle 100K+ users efficiently",
        recommendation: "Switch to PostgreSQL or MySQL for better scalability",
        auto_fix_available: true,
        suggested_override: { backend: { database: "PostgreSQL" } },
      };
    }

    // Check if hosting can handle traffic
    if (
      scalabilityNeeds.expected_requests_per_second > 1000 &&
      stack.infrastructure.hosting === "Vercel Hobby"
    ) {
      return {
        type: "scalability",
        severity: "high",
        issue:
          "Vercel Hobby plan has request limits for high-traffic applications",
        recommendation:
          "Upgrade to Vercel Pro or consider AWS/Railway for high-traffic needs",
        auto_fix_available: false,
        estimated_cost_impact: "$20-100/month",
      };
    }

    return { type: "scalability", status: "passed" };
  }

  private async validatePerformanceRequirements(
    requirements: ProjectRequirements,
    stack: ResolvedTechStack
  ): Promise<ValidationCheck> {
    // Check if real-time features need appropriate stack
    if (
      requirements.features.includes("real_time_collaboration") &&
      !stack.frontend.state_management.includes("real-time")
    ) {
      return {
        type: "performance",
        severity: "high",
        issue: "Real-time collaboration requires real-time state management",
        recommendation: "Add Convex or Socket.io for real-time capabilities",
        auto_fix_available: true,
        suggested_override: {
          frontend: { state_management: "Convex (real-time)" },
          backend: { additional_services: ["WebSocket support"] },
        },
      };
    }

    return { type: "performance", status: "passed" };
  }

  private async validateSecurityRequirements(
    requirements: ProjectRequirements,
    stack: ResolvedTechStack
  ): Promise<ValidationCheck> {
    // Check authentication requirements
    if (
      requirements.security.authentication_required &&
      !stack.frontend.authentication
    ) {
      return {
        type: "security",
        severity: "critical",
        issue: "Authentication required but no auth system configured",
        recommendation: "Add NextAuth.js or similar authentication system",
        auto_fix_available: true,
        suggested_override: {
          frontend: { authentication: "NextAuth.js" },
        },
      };
    }

    // Check compliance requirements
    if (
      requirements.security.compliance?.includes("GDPR") &&
      stack.infrastructure.hosting === "US-only"
    ) {
      return {
        type: "security",
        severity: "high",
        issue: "GDPR compliance may require EU data residency",
        recommendation:
          "Consider EU hosting options or multi-region deployment",
        auto_fix_available: false,
        requires_manual_review: true,
      };
    }

    return { type: "security", status: "passed" };
  }

  private async validateIntegrationRequirements(
    requirements: ProjectRequirements,
    stack: ResolvedTechStack
  ): Promise<ValidationCheck> {
    // Check third-party integrations
    for (const integration of requirements.integrations || []) {
      const compatibility = await this.checkIntegrationCompatibility(
        integration,
        stack
      );

      if (!compatibility.supported) {
        return {
          type: "integration",
          severity: "high",
          issue: `${integration.name} integration not supported with current stack`,
          recommendation: compatibility.recommendation,
          auto_fix_available: compatibility.auto_fix_available,
          suggested_override: compatibility.suggested_override,
        };
      }
    }

    return { type: "integration", status: "passed" };
  }
}
```

#### **Enhanced Architect Agent with Tech Stack Validation:**

```typescript
class EnhancedArchitectAgentWithTechStack extends EnhancedBMADAgent {
  constructor(
    memoryPickle: EnhancedMemoryPickle,
    vibeKitSDK: VibeKitSDK,
    private techStackManager: TechStackManager,
    private techStackValidator: TechStackValidator
  ) {
    super(memoryPickle, vibeKitSDK, "architect");
  }

  async executePhaseWithLearning(
    phase: BMADPhase,
    context: PhaseContext,
    learnings: LearningContext
  ): Promise<ArchitectureResult> {
    // 1. Resolve tech stack for this project
    const resolvedTechStack =
      await this.techStackManager.resolveProjectTechStack(
        context.userId,
        context.projectId
      );

    // 2. Validate tech stack against requirements
    const validationResult =
      await this.techStackValidator.validateTechStackForRequirements(
        context.requirements,
        resolvedTechStack
      );

    // 3. Handle validation issues
    if (!validationResult.passed) {
      const criticalIssues = validationResult.issues.filter(
        (i) => i.severity === "critical"
      );

      if (criticalIssues.length > 0) {
        // Auto-fix critical issues if possible
        const autoFixableIssues = criticalIssues.filter(
          (i) => i.auto_fix_available
        );

        if (autoFixableIssues.length > 0) {
          await this.applyTechStackFixes(
            context.userId,
            context.projectId,
            autoFixableIssues
          );

          // Re-resolve stack after fixes
          resolvedTechStack =
            await this.techStackManager.resolveProjectTechStack(
              context.userId,
              context.projectId
            );
        }

        // Report remaining critical issues
        const remainingCritical = criticalIssues.filter(
          (i) => !i.auto_fix_available
        );
        if (remainingCritical.length > 0) {
          throw new TechStackValidationError(
            "Critical tech stack issues require manual resolution",
            remainingCritical
          );
        }
      }
    }

    // 4. Generate architecture with validated tech stack
    const architecture = await this.generateArchitecture(context, {
      techStack: resolvedTechStack,
      validationResult,
      successfulPatterns: learnings.similarExperiences,
      knownPitfalls: learnings.knownIssues,
      recommendations: learnings.recommendations,
    });

    // 5. Store tech stack decision for learning
    await this.memoryPickle.remember_this({
      content: `Tech stack selected for ${
        context.projectType
      }: ${JSON.stringify(resolvedTechStack)}`,
      importance: "high",
      project_id: context.projectId,
      tags: ["tech_stack", "architecture", context.projectType],
    });

    return {
      architecture,
      techStack: resolvedTechStack,
      validationResult,
      rationale: this.generateTechStackRationale(
        resolvedTechStack,
        validationResult
      ),
      riskMitigation: this.generateRiskMitigation(validationResult.issues),
    };
  }

  private async applyTechStackFixes(
    userId: string,
    projectId: string,
    fixes: ValidationIssue[]
  ): Promise<void> {
    for (const fix of fixes) {
      if (fix.suggested_override) {
        await this.techStackManager.setProjectOverride(
          userId,
          projectId,
          fix.suggested_override,
          `Auto-fix: ${fix.recommendation}`
        );
      }
    }
  }
}
```

### User Interface for Tech Stack Management

#### **Tech Stack Selection UI:**

```typescript
interface TechStackSelectionUI {
  // During project creation
  showTechStackOptions(
    defaultStack: PlatformDefaultStack,
    userPreferences: UserTechStackPreferences
  ): Promise<UserTechStackSelection>;

  // During architecture phase
  showValidationResults(
    validationResult: ValidationResult
  ): Promise<UserValidationResponse>;

  // Global preferences management
  showGlobalPreferencesEditor(
    currentPreferences: UserTechStackPreferences
  ): Promise<UpdatedPreferences>;
}

// Example validation UI flow
const validationUI = {
  criticalIssues: [
    {
      type: "scalability",
      message: "⚠️ SQLite cannot handle your expected 100K+ users",
      options: [
        { label: "Auto-fix: Switch to PostgreSQL", action: "auto_fix" },
        { label: "Keep SQLite (not recommended)", action: "ignore" },
        { label: "Let me choose different database", action: "manual_select" },
      ],
    },
  ],
  warnings: [
    {
      type: "cost",
      message: "💰 Your hosting choice may cost $100+/month at scale",
      options: [
        { label: "Continue with current choice", action: "accept" },
        { label: "Show cost-effective alternatives", action: "alternatives" },
      ],
    },
  ],
};
```

### Implementation Strategy

#### **Phase 1: Default Stack Implementation** ✅ **Ready to Implement**

- [ ] Define platform default tech stack configuration
- [ ] Implement tech stack resolution logic
- [ ] Create user preference storage system
- [ ] Add basic override capabilities

#### **Phase 2: Validation Engine** ⏳ **Next Sprint**

- [ ] Build requirement-to-tech-stack validation system
- [ ] Implement scalability, performance, and security checks
- [ ] Add integration compatibility validation
- [ ] Create auto-fix capabilities for common issues

#### **Phase 3: Advanced Features** 📋 **Future Enhancement**

- [ ] Machine learning for tech stack recommendations
- [ ] Cost optimization suggestions
- [ ] Team expertise matching
- [ ] Historical performance analysis for stack choices

### Benefits

#### **For Users:**

✅ **Zero Configuration** - Works out of the box with proven defaults
✅ **Flexible Customization** - Override any part of the stack
✅ **Validation Safety** - Catch incompatibilities before development
✅ **Learning System** - Platform learns from successful stack choices

#### **For Platform:**

✅ **Consistent Quality** - Proven, production-ready defaults
✅ **Reduced Support** - Fewer tech stack-related issues
✅ **Better Outcomes** - Validated stacks lead to successful projects
✅ **Data-Driven Improvement** - Learn which stacks work best for different project types

---

### Generated Solution Architecture (Vertical Slice Architecture)

#### VSA Principles for Generated Applications

When the no-code platform generates applications for users, it employs **Vertical Slice Architecture (VSA)** to ensure:

- **Feature Isolation:** Each business function operates independently
- **Conflict Prevention:** Adding/modifying features won't break existing functionality
- **Maintainable Code:** Clear boundaries and responsibilities
- **User Confidence:** Predictable behavior for non-technical users

#### VSA Structure for Generated Apps

```

Generated Application Structure:
├── features/ // VSA Feature Slices
│ ├── authentication/ // Complete auth vertical
│ │ ├── api/auth-routes.ts
│ │ ├── components/LoginForm.tsx
│ │ ├── services/auth.service.ts
│ │ ├── database/user.model.ts
│ │ └── tests/auth.test.ts
│ ├── user-profile/ // Profile management vertical
│ │ ├── api/profile-routes.ts
│ │ ├── components/ProfileForm.tsx
│ │ ├── services/profile.service.ts
│ │ ├── database/profile.model.ts
│ │ └── tests/profile.test.ts
│ ├── product-catalog/ // Product management vertical
│ │ ├── api/products-routes.ts
│ │ ├── components/ProductList.tsx
│ │ ├── services/product.service.ts
│ │ ├── database/product.model.ts
│ │ └── tests/product.test.ts
│ └── shopping-cart/ // Cart functionality vertical
│ ├── api/cart-routes.ts
│ ├── components/CartWidget.tsx
│ ├── services/cart.service.ts
│ ├── database/cart.model.ts
│ └── tests/cart.test.ts
├── shared/ // Shared utilities within app
│ ├── types/ // Common TypeScript interfaces
│ ├── utils/ // Utility functions
│ ├── database/ // Database connection
│ ├── auth/ // Auth middleware
│ └── ui/ // Design system components
└── app/ // Next.js app router
├── api/ // API route aggregation
├── (auth)/ // Auth-related pages
├── (dashboard)/ // Dashboard pages
└── layout.tsx // Root layout

```

#### VSA Generation Strategy

**Requirements Analysis → Business Functions → VSA Features**

1. **Feature Identification:** BMAD agents analyze requirements and identify business functions
2. **VSA Mapping:** Each business function becomes a complete vertical slice
3. **Dependency Management:** Clear contracts between features via shared utilities
4. **Integration Points:** Event-driven communication between verticals

**Example Generation Flow:**

```

User Request: "E-commerce app with user accounts and product management"

↓ BMAD Analysis ↓

Generated VSA Features:

- features/authentication/ (login, register, password reset)
- features/user-profile/ (profile management, settings)
- features/product-catalog/ (CRUD, search, filtering)
- features/storefront/ (product display, cart integration)
- features/checkout/ (payment processing, orders)

```

#### VSA-Aware BMAD Agents

The following BMAD agents are enhanced with VSA methodology for generated solutions:

**1. Architect Agent (VSA-Enhanced)**

- Designs VSA structure based on business requirements
- Defines feature boundaries and integration points
- Creates VSA-compliant architecture documents

**2. Dev Agent (VSA-Enhanced)**

- Generates code following VSA patterns
- Ensures feature isolation in generated code
- Implements clean integration contracts

**3. QA Agent (VSA-Enhanced)**

- Tests each VSA feature independently
- Validates feature isolation and integration points
- Ensures no cross-feature contamination

**4. PM Agent (VSA-Enhanced)**

- Maps requirements to VSA features
- Manages feature scope and boundaries
- Prevents cross-feature requirement creep

#### VSA Benefits for Non-Technical Users

✅ **Zero Conflict Guarantee** - Approved features stay approved
✅ **Incremental Development** - Add features without breaking existing ones
✅ **Clear Boundaries** - Users understand feature scope and impact
✅ **Safe Regeneration** - Modify one feature without affecting others
✅ **Predictable Behavior** - Consistent, reliable application structure

### Enhanced BMAD Agents with Semantic Learning

The BMAD agents are enhanced with semantic search and learning capabilities through the Enhanced Memory Pickle MCP integration. Each agent can now learn from past experiences, avoid repeated mistakes, and leverage successful patterns from previous projects.

#### **Enhanced Agent Architecture**

```typescript
// Base Enhanced BMAD Agent with Semantic Learning
abstract class EnhancedBMADAgent {
  constructor(
    protected memoryPickle: EnhancedMemoryPickle,
    protected vibeKitSDK: VibeKitSDK,
    protected agentType: BMADAgentType
  ) {}

  async executePhase(
    phase: BMADPhase,
    context: PhaseContext
  ): Promise<PhaseResult> {
    // 1. Recall similar past experiences
    const similarExperiences = await this.memoryPickle.semantic_search({
      query: `${phase} ${context.projectType} ${context.techStack.join(" ")}`,
      importance: ["critical", "high"],
      limit: 5,
      context_type: "pattern",
    });

    // 2. Check for known issues and solutions
    const knownIssues = await this.memoryPickle.recall_similar_issues({
      phase,
      techStack: context.techStack,
      projectType: context.projectType,
    });

    // 3. Get recommended approaches based on past successes
    const recommendations = await this.memoryPickle.get_project_insights(
      context.projectType
    );

    // 4. Execute phase with enhanced context
    const result = await this.executePhaseWithLearning(phase, context, {
      similarExperiences,
      knownIssues,
      recommendations,
    });

    // 5. Store learnings for future use
    await this.storeLearnings(phase, context, result);

    return result;
  }

  protected abstract executePhaseWithLearning(
    phase: BMADPhase,
    context: PhaseContext,
    learnings: LearningContext
  ): Promise<PhaseResult>;

  private async storeLearnings(
    phase: BMADPhase,
    context: PhaseContext,
    result: PhaseResult
  ): Promise<void> {
    // Store successful patterns
    if (result.success) {
      await this.memoryPickle.remember_this({
        content: `Successful ${phase} approach: ${result.approach}`,
        importance: "high",
        project_id: context.projectId,
        tags: [phase, context.projectType, ...context.techStack],
      });
    }

    // Store mistakes and solutions
    if (result.issues.length > 0) {
      for (const issue of result.issues) {
        await this.memoryPickle.learn_from_mistake({
          phase,
          error_description: issue.description,
          solution_applied: issue.solution,
          tech_stack: context.techStack,
          project_type: context.projectType,
          severity: issue.severity,
          prevention_strategy: issue.prevention,
        });
      }
    }

    // Store bug fixes
    if (result.bugFixes.length > 0) {
      for (const bugFix of result.bugFixes) {
        await this.memoryPickle.store_bug_fix({
          bug_description: bugFix.description,
          root_cause: bugFix.rootCause,
          solution_steps: bugFix.solutionSteps,
          tech_stack: context.techStack,
          files_affected: bugFix.filesAffected,
          testing_approach: bugFix.testingApproach,
          prevention_measures: bugFix.preventionMeasures,
        });
      }
    }
  }
}
```

#### **1. Enhanced Architect Agent**

```typescript
class EnhancedArchitectAgent extends EnhancedBMADAgent {
  async executePhaseWithLearning(
    phase: BMADPhase,
    context: PhaseContext,
    learnings: LearningContext
  ): Promise<ArchitectureResult> {
    // Leverage past architectural decisions
    const architecturalPatterns = await this.memoryPickle.semantic_search({
      query: `architecture patterns ${context.projectType} scalability performance`,
      context_type: "pattern",
      limit: 10,
    });

    // Check for common architectural pitfalls
    const commonPitfalls = await this.memoryPickle.recall_similar_issues({
      phase: "architecture",
      techStack: context.techStack,
      projectType: context.projectType,
    });

    // Generate architecture with learned insights
    const architecture = await this.generateArchitecture(context, {
      successfulPatterns: architecturalPatterns,
      knownPitfalls: commonPitfalls,
      recommendations: learnings.recommendations,
    });

    return {
      architecture,
      rationale: this.generateRationale(architecturalPatterns, commonPitfalls),
      riskMitigation: this.generateRiskMitigation(commonPitfalls),
    };
  }
}
```

#### **2. Enhanced Dev Agent**

```typescript
class EnhancedDevAgent extends EnhancedBMADAgent {
  async executePhaseWithLearning(
    phase: BMADPhase,
    context: PhaseContext,
    learnings: LearningContext
  ): Promise<DevelopmentResult> {
    // Learn from past coding patterns and mistakes
    const codingPatterns = await this.memoryPickle.semantic_search({
      query: `coding patterns ${context.techStack.join(" ")} best practices`,
      context_type: "pattern",
      limit: 15,
    });

    // Get bug fixes for similar tech stacks
    const relevantBugFixes = await this.memoryPickle.semantic_search({
      query: `bug fixes ${context.techStack.join(" ")} common issues`,
      context_type: "bug_fix",
      limit: 10,
    });

    // Predict potential issues before coding
    const potentialIssues = await this.memoryPickle.predict_potential_issues({
      projectType: context.projectType,
      techStack: context.techStack,
      features: context.features,
    });

    // Generate VSA-compliant code with learned insights
    const generatedCode = await this.generateVSACode(context, {
      successfulPatterns: codingPatterns,
      knownBugFixes: relevantBugFixes,
      potentialIssues,
      preventiveMeasures: this.generatePreventiveMeasures(potentialIssues),
    });

    return {
      code: generatedCode,
      qualityMetrics: await this.assessCodeQuality(generatedCode),
      preventedIssues: potentialIssues.length,
      appliedPatterns: codingPatterns.length,
    };
  }
}
```

#### **3. Enhanced QA Agent**

```typescript
class EnhancedQAAgent extends EnhancedBMADAgent {
  async executePhaseWithLearning(
    phase: BMADPhase,
    context: PhaseContext,
    learnings: LearningContext
  ): Promise<QAResult> {
    // Learn from past testing strategies and missed bugs
    const testingStrategies = await this.memoryPickle.semantic_search({
      query: `testing strategies ${
        context.projectType
      } ${context.techStack.join(" ")}`,
      context_type: "pattern",
      limit: 10,
    });

    // Get common bugs for this tech stack
    const commonBugs = await this.memoryPickle.semantic_search({
      query: `common bugs ${context.techStack.join(" ")} testing`,
      context_type: "bug_fix",
      limit: 15,
    });

    // Generate comprehensive test suite based on learnings
    const testSuite = await this.generateEnhancedTestSuite(context, {
      provenStrategies: testingStrategies,
      knownBugPatterns: commonBugs,
      riskAreas: learnings.knownIssues,
    });

    // Execute tests with Web-Eval-Agent integration
    const testResults = await this.executeTestsWithWebEval(testSuite, context);

    return {
      testSuite,
      results: testResults,
      coverageMetrics: await this.calculateCoverage(testResults),
      preventedBugs: commonBugs.filter((bug) =>
        testSuite.tests.some((test) => test.targets.includes(bug.pattern))
      ).length,
    };
  }
}
```

#### **4. Enhanced PM Agent**

```typescript
class EnhancedPMAgent extends EnhancedBMADAgent {
  async executePhaseWithLearning(
    phase: BMADPhase,
    context: PhaseContext,
    learnings: LearningContext
  ): Promise<ProjectManagementResult> {
    // Learn from past project management decisions
    const pmPatterns = await this.memoryPickle.semantic_search({
      query: `project management ${context.projectType} scope timeline`,
      context_type: "pattern",
      limit: 8,
    });

    // Get common project pitfalls
    const projectPitfalls = await this.memoryPickle.recall_similar_issues({
      phase: "project_management",
      projectType: context.projectType,
    });

    // Generate enhanced project plan
    const projectPlan = await this.generateProjectPlan(context, {
      successfulApproaches: pmPatterns,
      knownPitfalls: projectPitfalls,
      riskMitigation: this.generateRiskMitigation(projectPitfalls),
    });

    return {
      plan: projectPlan,
      riskAssessment: this.assessProjectRisks(projectPitfalls),
      successProbability: this.calculateSuccessProbability(
        pmPatterns,
        projectPitfalls
      ),
    };
  }
}
```

#### **Cross-Agent Learning Benefits**

**1. Mistake Prevention:**

- Agents learn from past errors across all projects
- Common pitfalls are automatically avoided
- Solutions are reused and refined

**2. Pattern Recognition:**

- Successful approaches are identified and replicated
- Best practices emerge from real project data
- Architecture patterns evolve based on outcomes

**3. Predictive Capabilities:**

- Potential issues are identified before they occur
- Risk assessment improves with each project
- Resource estimation becomes more accurate

**4. Continuous Improvement:**

- Agent performance improves over time
- Knowledge compounds across projects
- User satisfaction increases with better outcomes

**5. Cross-Project Intelligence:**

- Learnings from one project benefit all future projects
- Anonymous pattern sharing across users
- Platform-wide intelligence accumulation

---

## Enhanced BMAD Workflow with Self-Hosted ACI Integration

### Overview

The integration of self-hosted ACI.dev transforms the BMAD workflow from code generation to complete production deployment. Each BMAD phase is enhanced with 600+ tool integrations, enabling non-technical users to go from vision to live product seamlessly.

### Phase-by-Phase ACI Enhancement

#### **Phase 1: Vision & Style Definition (Enhanced)**

**Traditional BMAD:**

- User selects visual style
- AI generates mockups
- Style preferences captured

**ACI-Enhanced BMAD:**

- User selects visual style
- AI generates mockups
- **ACI Integration:** Automatic domain availability checking via Cloudflare
- **ACI Integration:** GitHub repository creation for project tracking
- **ACI Integration:** Slack/Discord workspace setup for project notifications
- Style preferences and infrastructure foundation established

**ACI Tools Used:**

```typescript
const phase1Tools = [
  "CLOUDFLARE__CHECK_DOMAIN_AVAILABILITY",
  "GITHUB__CREATE_REPOSITORY",
  "SLACK__CREATE_CHANNEL",
  "NOTION__CREATE_PROJECT_PAGE",
];
```

#### **Phase 2: Collaborative Requirement Gathering (Enhanced)**

**Traditional BMAD:**

- AI-driven requirement elicitation
- PRD generation
- User story creation

**ACI-Enhanced BMAD:**

- AI-driven requirement elicitation
- PRD generation with automatic documentation
- **ACI Integration:** Notion/Google Docs automatic PRD publishing
- **ACI Integration:** Asana/Linear project management setup
- **ACI Integration:** Stakeholder notification via email/Slack
- **ACI Integration:** Requirement validation via survey tools

**ACI Tools Used:**

```typescript
const phase2Tools = [
  "NOTION__CREATE_PAGE",
  "GOOGLE_DOCS__CREATE_DOCUMENT",
  "ASANA__CREATE_PROJECT",
  "RESEND__SEND_EMAIL",
  "SLACK__SEND_MESSAGE",
];
```

#### **Phase 3: Interactive Prototyping & Logic Validation (Enhanced)**

**Traditional BMAD:**

- Functional prototype generation
- User testing and validation
- Iterative refinement

**ACI-Enhanced BMAD:**

- Functional prototype generation
- **ACI Integration:** Automatic Vercel preview deployment
- **ACI Integration:** User feedback collection via Typeform/Airtable
- **ACI Integration:** Analytics setup with PostHog/Google Analytics
- **ACI Integration:** A/B testing configuration
- **ACI Integration:** Stakeholder sharing via email/Slack with live links

**ACI Tools Used:**

```typescript
const phase3Tools = [
  "VERCEL__DEPLOY_PROJECT",
  "TYPEFORM__CREATE_FORM",
  "AIRTABLE__CREATE_BASE",
  "POSTHOG__CREATE_PROJECT",
  "RESEND__SEND_EMAIL",
];
```

#### **Phase 4: Architectural Blueprinting (Enhanced)**

**Traditional BMAD:**

- Technical architecture generation
- Infrastructure planning
- Documentation creation

**ACI-Enhanced BMAD:**

- Technical architecture generation
- **ACI Integration:** Database provisioning (Supabase/PlanetScale)
- **ACI Integration:** CDN and edge configuration (Cloudflare)
- **ACI Integration:** Monitoring setup (Sentry/DataDog)
- **ACI Integration:** Security scanning and configuration
- **ACI Integration:** Cost estimation and budget alerts
- **ACI Integration:** Architecture documentation in Notion/Confluence

**ACI Tools Used:**

```typescript
const phase4Tools = [
  "SUPABASE__CREATE_PROJECT",
  "PLANETSCALE__CREATE_DATABASE",
  "CLOUDFLARE__CONFIGURE_CDN",
  "SENTRY__CREATE_PROJECT",
  "NOTION__CREATE_ARCHITECTURE_DOC",
];
```

#### **Phase 5: AI-Driven Development & Deployment (Fully Enhanced)**

**Traditional BMAD:**

- Code generation
- Testing
- Basic deployment

**ACI-Enhanced BMAD:**

- VSA-compliant code generation
- **ACI Integration:** Production deployment (Vercel/Railway/Fly.io)
- **ACI Integration:** Database schema migration and seeding
- **ACI Integration:** Environment variable management
- **ACI Integration:** Custom domain configuration with SSL
- **ACI Integration:** Email service setup (Resend/SendGrid)
- **ACI Integration:** Payment processing (Stripe) if applicable
- **ACI Integration:** Analytics and monitoring activation
- **ACI Integration:** SEO optimization and sitemap generation
- **ACI Integration:** Social media integration setup
- **ACI Integration:** Backup and disaster recovery configuration

**ACI Tools Used:**

```typescript
const phase5Tools = [
  // Core Deployment
  "VERCEL__DEPLOY_PROJECT",
  "RAILWAY__DEPLOY_APPLICATION",
  "FLY_IO__DEPLOY_APP",

  // Database & Backend
  "SUPABASE__MIGRATE_SCHEMA",
  "PLANETSCALE__DEPLOY_SCHEMA",
  "NEON__CREATE_DATABASE",

  // Domain & SSL
  "CLOUDFLARE__CONFIGURE_DOMAIN",
  "CLOUDFLARE__SETUP_SSL",

  // Communication
  "RESEND__CONFIGURE_DOMAIN",
  "SENDGRID__SETUP_TEMPLATES",

  // Payments & Business
  "STRIPE__CREATE_PRODUCTS",
  "PADDLE__SETUP_CHECKOUT",

  // Monitoring & Analytics
  "SENTRY__CONFIGURE_MONITORING",
  "POSTHOG__SETUP_ANALYTICS",
  "GOOGLE_ANALYTICS__CREATE_PROPERTY",

  // SEO & Marketing
  "GOOGLE_SEARCH_CONSOLE__VERIFY_SITE",
  "FACEBOOK_PIXEL__SETUP_TRACKING",
];
```

### Enhanced BMAD Workflow with Web-Eval-Agent Integration

#### **Phase 5: AI-Driven Development + Automated QA (Fully Enhanced)**

**Traditional BMAD Phase 5:**

- Code generation
- Basic testing
- Simple deployment

**Web-Eval-Agent Enhanced Phase 5:**

- VSA-compliant code generation
- **Web-Eval-Agent Integration:** Automated end-to-end testing
- **Web-Eval-Agent Integration:** UX evaluation and issue detection
- **Web-Eval-Agent Integration:** Console error and network analysis
- **Web-Eval-Agent Integration:** Automated bug reproduction and fix recommendations
- **Web-Eval-Agent Integration:** Performance and accessibility testing
- Production deployment with validated quality assurance

**Web-Eval-Agent Tools Used:**

```typescript
const webEvalTools = [
  "web_eval_agent", // Autonomous UX evaluator
  "setup_browser_state", // Interactive browser setup
];

const testScenarios = [
  "Test all user flows and identify UX issues",
  "Verify form submissions and error handling",
  "Check responsive design on mobile devices",
  "Test authentication and authorization flows",
  "Validate API integrations and data flow",
  "Check accessibility compliance",
  "Test performance under load",
];
```

### Complete Deployment Pipeline

#### **From Code to Tested Live Product in Minutes:**

```typescript
// Enhanced BMAD Dev Agent with ACI Integration
class EnhancedBMADDevAgent {
  constructor(
    private aciMCPClient: ACIMCPClient,
    private memoryPickle: MemoryPickleMCP,
    private superClaude: SuperClaudeValidator
  ) {}

  async executePhase5(project: Project): Promise<LiveApplication> {
    // 1. Generate VSA-compliant code
    const generatedCode = await this.generateVSACode(project);

    // 2. Quality validation with SuperClaude
    const qualityCheck = await this.superClaude.validate(generatedCode);
    if (!qualityCheck.approved) {
      throw new Error("Code quality below threshold");
    }

    // 3. Deploy to production via ACI
    const deployment = await this.deployToProduction(generatedCode, project);

    // 4. Setup infrastructure via ACI
    const infrastructure = await this.setupInfrastructure(project);

    // 5. Configure monitoring and analytics
    const monitoring = await this.setupMonitoring(project);

    // 6. Final validation and go-live
    return this.goLive(deployment, infrastructure, monitoring);
  }

  private async deployToProduction(code: GeneratedCode, project: Project) {
    // Deploy to Vercel with custom domain
    const deployment = await this.aciMCPClient.callTool(
      "VERCEL__DEPLOY_PROJECT",
      {
        projectPath: code.path,
        customDomain: project.domain,
        environmentVars: project.envVars,
      }
    );

    // Configure Cloudflare CDN and SSL
    await this.aciMCPClient.callTool("CLOUDFLARE__CONFIGURE_DOMAIN", {
      domain: project.domain,
      targetUrl: deployment.url,
      enableSSL: true,
      enableCDN: true,
    });

    return deployment;
  }

  private async setupInfrastructure(project: Project) {
    // Database setup
    const database = await this.aciMCPClient.callTool(
      "SUPABASE__CREATE_PROJECT",
      {
        name: project.name,
        schema: project.databaseSchema,
        region: project.region,
      }
    );

    // Email service setup
    const emailService = await this.aciMCPClient.callTool(
      "RESEND__CONFIGURE_DOMAIN",
      {
        domain: project.domain,
        templates: project.emailTemplates,
      }
    );

    // Payment processing (if e-commerce)
    let paymentSetup = null;
    if (project.hasPayments) {
      paymentSetup = await this.aciMCPClient.callTool(
        "STRIPE__CREATE_PRODUCTS",
        {
          products: project.products,
          webhookUrl: `${project.domain}/api/webhooks/stripe`,
        }
      );
    }

    return { database, emailService, paymentSetup };
  }

  private async setupMonitoring(project: Project) {
    // Error tracking
    const errorTracking = await this.aciMCPClient.callTool(
      "SENTRY__CREATE_PROJECT",
      {
        name: project.name,
        platform: "nextjs",
        alertRules: project.alertRules,
      }
    );

    // Analytics
    const analytics = await this.aciMCPClient.callTool(
      "POSTHOG__CREATE_PROJECT",
      {
        name: project.name,
        domain: project.domain,
        events: project.trackingEvents,
      }
    );

    // Uptime monitoring
    const uptime = await this.aciMCPClient.callTool("PINGDOM__CREATE_CHECK", {
      url: project.domain,
      interval: 5,
      alertContacts: project.alertContacts,
    });

    return { errorTracking, analytics, uptime };
  }

  // 7. Automated Testing with Web-Eval-Agent (NEW)
  private async runAutomatedTesting(deployment: Deployment, project: Project) {
    const webEvalClient = this.webEvalAgentMCP;

    // 1. Setup browser state for authentication if needed
    if (project.requiresAuthentication) {
      await webEvalClient.callTool("setup_browser_state", {
        url: `${deployment.url}/login`,
      });
    }

    // 2. Generate test scenarios based on project requirements
    const testScenarios = this.generateTestScenarios(project);

    const testResults = [];

    // 3. Execute each test scenario using web_eval_agent
    for (const scenario of testScenarios) {
      const result = await webEvalClient.callTool("web_eval_agent", {
        url: deployment.url,
        task: scenario,
        headless_browser: true,
      });

      testResults.push({
        scenario,
        result,
        passed: !result.hasIssues,
        issues: result.detectedIssues || [],
        consoleErrors:
          result.consoleLogs?.filter((log) => log.level === "error") || [],
        networkFailures:
          result.networkRequests?.filter((req) => req.status >= 400) || [],
        performanceMetrics: result.performanceMetrics || {},
      });
    }

    return {
      overallPassed: testResults.every((r) => r.passed),
      testResults,
      summary: this.generateTestSummary(testResults),
      authenticationSetup: project.requiresAuthentication,
    };
  }

  // 8. Automated Issue Resolution (NEW)
  private async resolveDetectedIssues(
    testResults: TestResults,
    generatedCode: GeneratedCode
  ) {
    const criticalIssues = testResults.testResults
      .flatMap((r) => r.issues)
      .filter(
        (issue) => issue.severity === "critical" || issue.severity === "high"
      );

    if (criticalIssues.length === 0) {
      return { codeUpdated: false, generatedCode };
    }

    // Generate fixes for critical issues
    const fixes = await this.generateAutomatedFixes(
      criticalIssues,
      generatedCode
    );

    // Apply fixes to code
    const updatedCode = await this.applyFixes(generatedCode, fixes);

    return {
      codeUpdated: true,
      generatedCode: updatedCode,
      appliedFixes: fixes,
    };
  }

  // Enhanced Phase 5 with Web-Eval-Agent Integration
  async executeEnhancedPhase5(
    project: Project
  ): Promise<TestedLiveApplication> {
    // 1. Generate VSA-compliant code
    const generatedCode = await this.generateVSACode(project);

    // 2. Quality validation with SuperClaude
    const qualityCheck = await this.superClaude.validate(generatedCode);
    if (!qualityCheck.approved) {
      throw new Error("Code quality below threshold");
    }

    // 3. Deploy to production via ACI
    let deployment = await this.deployToProduction(generatedCode, project);

    // 4. Setup infrastructure via ACI
    const infrastructure = await this.setupInfrastructure(project);

    // 5. Configure monitoring and analytics
    const monitoring = await this.setupMonitoring(project);

    // 6. Automated testing with Web-Eval-Agent (NEW)
    const testResults = await this.runAutomatedTesting(deployment, project);

    // 7. Automated issue resolution (NEW)
    if (!testResults.overallPassed) {
      const fixResults = await this.resolveDetectedIssues(
        testResults,
        generatedCode
      );

      if (fixResults.codeUpdated) {
        // Re-deploy with fixes
        deployment = await this.deployToProduction(
          fixResults.generatedCode,
          project
        );

        // Re-test to verify fixes
        const retestResults = await this.runAutomatedTesting(
          deployment,
          project
        );

        return {
          deployment,
          infrastructure,
          monitoring,
          testResults: retestResults,
          fixesApplied: fixResults.appliedFixes,
          qualityAssured: retestResults.overallPassed,
        };
      }
    }

    // 8. Final validation and go-live
    return {
      deployment,
      infrastructure,
      monitoring,
      testResults,
      fixesApplied: [],
      qualityAssured: testResults.overallPassed,
    };
  }
}
```

### User Experience Transformation

#### **Before ACI Integration:**

```
User Journey: Vision → Code → Manual Deployment (Weeks/Months)
├── Phase 1-4: BMAD workflow (Days)
├── Phase 5: Code generation (Hours)
└── Manual deployment: (Weeks)
    ├── Find hosting provider
    ├── Configure domains
    ├── Setup databases
    ├── Configure monitoring
    ├── Handle SSL certificates
    └── Debug deployment issues
```

#### **After ACI Integration:**

```
User Journey: Vision → Live Product (Hours)
├── Phase 1-4: Enhanced BMAD workflow (Hours)
└── Phase 5: Automated deployment (Minutes)
    ├── Code generation ✅
    ├── Production deployment ✅
    ├── Database provisioning ✅
    ├── Domain configuration ✅
    ├── SSL certificates ✅
    ├── Monitoring setup ✅
    └── Analytics activation ✅
```

### Business Impact

#### **Value Proposition Enhancement:**

- **Time to Market:** Weeks → Hours
- **Technical Complexity:** High → Zero
- **Infrastructure Management:** Manual → Automated
- **Monitoring & Analytics:** Optional → Built-in
- **Scalability:** Unknown → Production-ready
- **Cost Predictability:** Variable → Fixed

#### **Competitive Advantage:**

- **Complete Solution:** Only platform that goes from vision to live product
- **Production-Ready:** Not just prototypes, but scalable applications
- **Zero Technical Debt:** Professional architecture from day one
- **Enterprise-Grade:** Monitoring, security, and compliance built-in

---

## Platform Component Architecture

#### 1. Frontend Layer (V0-Clone Extended)

**Foundation:** Next.js 15 + TypeScript from V0-Clone
**Extensions:** BMAD workflow UI components + Memory Pickle MCP integration
**Key Features:**

- **Chat Interface:** Adapted for guided BMAD conversations with context preservation
- **Phase Navigation:** 5-phase workflow progression with handoff summaries
- **Multi-Project Dashboard:** Project switching and management interface
- **Template Gallery:** Business application templates with intelligent suggestions
- **Preview System:** Interactive prototype validation with session recovery
- **Progress Tracking:** Real-time workflow status with Memory Pickle state integration
- **Learning Dashboard:** Cross-project insights and recommendations

#### 2. Real-time State Management (Convex)

**Foundation:** Convex from V0-Clone
**Extensions:** BMAD workflow state schemas
**Key Features:**

- **Session Persistence:** Multi-phase project state
- **Real-time Collaboration:** Live updates across team members
- **Document Versioning:** Template and output version control
- **User Workspace:** Project organization and management

#### 3. Background Processing (Inngest)

**Foundation:** Inngest from V0-Clone
**Extensions:** BMAD workflow orchestration
**Key Features:**

- **Phase Orchestration:** Automated workflow progression
- **Agent Coordination:** BMAD agent task distribution
- **Long-running Tasks:** Code generation and deployment
- **Error Recovery:** Workflow resilience and retry logic

#### 4. AI Execution Layer (VibeKit Enhanced)

**Foundation:** VibeKit SDK from V0-Clone
**Extensions:** BMAD agent specialization with user isolation
**Key Features:**

- **Multi-Agent Support:** Claude, Codex, Gemini integration
- **Isolated User Sandboxes:** Complete user/project isolation via E2B, Daytona, Northflank
- **Multi-Tier Sandbox Support:** E2B (free tier), Northflank (premium), Daytona (enterprise)
- **GitHub Integration:** Repository management and PR creation per user
- **Streaming Responses:** Real-time AI output with session persistence
- **Resource Management:** Automatic pause/resume for cost optimization
- **VSA-Aware Generation:** Vertical Slice Architecture compliant code generation

#### 5. BMAD Orchestration Layer (New)

**Technology:** Custom TypeScript services + AI Fastify Template integration
**Integration:** Built on top of V0-Clone foundation with specialized backend agent
**Key Features:**

- **Workflow Management:** 5-phase BMAD progression
- **Agent Specialization:** PM, Architect, Dev (enhanced), QA, UX roles
- **Backend Code Generation:** AI Fastify Template-based backend agent
- **Business Logic:** Non-technical user experience
- **Quality Gates:** Phase validation and approval with enterprise-grade testing

#### 5a. BMAD Backend Agent (AI Fastify Template + ACI Integration)

**Technology:** AI Fastify Template + VibeKit + Memory Pickle MCP + Self-hosted ACI
**Purpose:** Specialized agent for generating and deploying production-ready backend APIs
**Key Features:**

- **Enterprise-Grade Code Generation:** Fastify + TypeScript with strict quality gates
- **VSA-Compliant Architecture:** Generates vertical slice backend features
- **Comprehensive Testing:** Mutation testing (85% threshold) + property-based testing
- **Security-First:** Zod validation, GitLeaks scanning, dependency auditing
- **AI-Optimized Patterns:** Prevents common AI development pitfalls
- **Zero-Failure Guarantee:** 4-layer validation system ensures quality
- **Production Deployment:** Automated deployment via ACI integrations (Vercel, Railway, Fly.io)
- **Database Provisioning:** Automatic Supabase/PlanetScale database setup and schema migration
- **Monitoring Setup:** Integrated Sentry error tracking and performance monitoring

#### 6. Memory Pickle MCP Integration Layer (New)

**Technology:** Memory Pickle MCP Server
**Integration:** MCP protocol integration with BMAD agents
**Key Features:**

- **Multi-Project Context Management:** Isolated project sessions with cross-project learning
- **Agent Memory System:** Persistent context across agent interactions
- **Session Recovery:** Resume complex projects across multiple sessions
- **Intelligent Handoffs:** Automated phase transitions with comprehensive summaries
- **Learning System:** Multi-level insights (Project → User → Type → Technology → Platform)
- **Template Intelligence:** Smart project initialization based on type and user history

#### 7. Self-Hosted ACI Integration Layer (New)

**Technology:** Self-hosted ACI.dev platform with unified MCP server
**Purpose:** 600+ tool integrations for complete DevOps automation and deployment
**Integration:** MCP protocol integration with BMAD agents for production-ready deployments
**Key Features:**

- **600+ Pre-built Integrations:** GitHub, Vercel, Supabase, Cloudflare, Sentry, Slack, and more
- **Multi-tenant Authentication:** OAuth flows and secrets management handled automatically
- **Production Deployment Pipeline:** Complete CI/CD automation from code to live product
- **Infrastructure as Code:** Self-hosted on AWS with provided CDK deployment stack
- **Cost Control:** No per-API-call charges, fixed infrastructure costs
- **Data Privacy:** Complete control over user data and integration credentials
- **Custom Domain Management:** Automated DNS and SSL certificate provisioning
- **Monitoring & Analytics:** Integrated error tracking, performance monitoring, and user analytics

**Self-Hosting Architecture:**

```
┌─────────────────────────────────────────────────────────────────┐
│                    Self-Hosted ACI Platform                     │
├─────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │   FastAPI   │  │ PostgreSQL  │  │   600+      │              │
│  │   Backend   │  │  Database   │  │ Integrations│              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
├─────────────────────────────────────────────────────────────────┤
│  MCP Server Endpoint → BMAD Agents                              │
└─────────────────────────────────────────────────────────────────┘
```

#### 8. SuperClaude Quality Validation Layer (New)

**Technology:** SuperClaude Framework integration
**Purpose:** Quality assurance and sanity checking for BMAD agent outputs
**Integration:** Validation layer that runs after each BMAD agent phase
**Key Features:**

- **Multi-Perspective Validation:** 11 specialized personas for comprehensive review
- **Quality Gate Enforcement:** Automated validation with configurable thresholds
- **Error Detection:** Catch issues BMAD agents might miss through alternative analysis
- **Confidence Scoring:** Quantitative quality metrics for each phase output
- **Recommendation Engine:** Improvement suggestions based on validation results
- **Cross-Agent Consistency:** Ensure coherent outputs across BMAD phases

---

## Implementation Roadmap & Deployment Strategy

### Phase 1: Foundation Setup (Weeks 1-4)

#### **Core Infrastructure Deployment**

```bash
# 1. Deploy Self-Hosted ACI Platform
cd aci-platform/backend/deployment
cdk deploy --all

# 2. Configure Essential Integrations
docker compose exec runner python -m aci.cli upsert-app \
  --app-file ./apps/vercel/app.json \
  --secrets-file ./apps/vercel/.app.secrets.json

# 3. Setup MCP Server Endpoint
# Configure ACI MCP server for BMAD agent access
```

#### **V0-Clone Foundation Enhancement**

- Deploy enhanced V0-Clone with BMAD workflow UI
- Integrate Memory Pickle MCP for session management
- Configure Convex schemas for multi-project support
- Setup Inngest workflows for BMAD orchestration

#### **Essential ACI Integrations**

```typescript
const phase1Integrations = [
  "VERCEL__DEPLOY_PROJECT", // Core deployment
  "GITHUB__CREATE_REPOSITORY", // Version control
  "SUPABASE__CREATE_PROJECT", // Database
  "CLOUDFLARE__CONFIGURE_DOMAIN", // DNS/SSL
  "SENTRY__CREATE_PROJECT", // Error tracking
];
```

### Phase 2: BMAD Agent Enhancement (Weeks 5-8)

#### **Enhanced Dev Agent with ACI**

```typescript
// Integration of AI Fastify Template + ACI deployment
class EnhancedBMADDevAgent extends BMADDevAgent {
  constructor(
    private aciMCPClient: ACIMCPClient,
    private fastifyTemplate: AIFastifyTemplate
  ) {
    super();
  }

  async generateAndDeploy(project: Project): Promise<LiveApplication> {
    // 1. Generate VSA-compliant code
    const code = await this.fastifyTemplate.generateVSACode(project);

    // 2. Deploy via ACI integrations
    const deployment = await this.deployViaACI(code, project);

    return deployment;
  }
}
```

#### **Quality Validation Integration**

- SuperClaude validation layer implementation
- Quality gate enforcement at each BMAD phase
- Automated retry and improvement workflows

#### **Extended ACI Integrations**

```typescript
const phase2Integrations = [
  "NOTION__CREATE_PAGE", // Documentation
  "SLACK__SEND_MESSAGE", // Notifications
  "RESEND__SEND_EMAIL", // Communications
  "POSTHOG__CREATE_PROJECT", // Analytics
  "STRIPE__CREATE_PRODUCTS", // Payments (if applicable)
];
```

### Phase 3: Production Optimization (Weeks 9-12)

#### **Advanced Features**

- Multi-tenant user isolation and scaling
- Advanced VSA pattern generation
- Custom domain automation
- Enterprise security features

#### **Performance & Monitoring**

- Real-time deployment monitoring
- Cost optimization and resource management
- Advanced analytics and user insights
- Automated backup and disaster recovery

#### **Full Integration Suite**

```typescript
const phase3Integrations = [
  // Advanced deployment options
  "RAILWAY__DEPLOY_APPLICATION",
  "FLY_IO__DEPLOY_APP",

  // Business integrations
  "GOOGLE_ANALYTICS__CREATE_PROPERTY",
  "FACEBOOK_PIXEL__SETUP_TRACKING",
  "CALENDLY__CREATE_EVENT",

  // Enterprise features
  "DATADOG__SETUP_MONITORING",
  "AWS_S3__CONFIGURE_STORAGE",
  "SENDGRID__SETUP_TEMPLATES",
];
```

### Deployment Architecture

#### **Production Infrastructure**

```yaml
# AWS Infrastructure (via ACI CDK)
ACI Platform:
  - ECS Fargate: ACI backend services
  - RDS PostgreSQL: ACI database + integrations
  - ElastiCache: Session and cache management
  - Application Load Balancer: Traffic distribution
  - CloudWatch: Monitoring and logging

VibeKit Platform:
  - Vercel: Next.js frontend deployment
  - Convex: Real-time state management
  - Inngest: Background job processing
  - AWS EKS: BMAD agent orchestration
  - S3: File storage and backups
```

#### **Security & Compliance**

```typescript
// Multi-tenant security model
interface SecurityModel {
  userIsolation: {
    sandboxes: "E2B | Northflank | Daytona";
    databases: "Per-user schema isolation";
    sessions: "Encrypted session management";
  };

  dataProtection: {
    encryption: "AES-256 at rest and in transit";
    secrets: "AWS Secrets Manager integration";
    oauth: "Secure credential management via ACI";
  };

  compliance: {
    gdpr: "User data control and deletion";
    soc2: "Audit logging and access controls";
    enterprise: "SSO and advanced permissions";
  };
}
```

### Success Metrics & Monitoring

#### **Technical Metrics**

- **Deployment Success Rate:** >95% successful deployments
- **Time to Live Product:** <2 hours from vision to production
- **System Uptime:** 99.9% availability SLA
- **ACI Integration Health:** Real-time monitoring of all 600+ tools

#### **Business Metrics**

- **User Conversion:** Vision → Live Product completion rate
- **Time to Value:** Hours instead of weeks/months
- **Customer Satisfaction:** Net Promoter Score >50
- **Revenue Impact:** $100K+ MRR within 12 months

#### **Quality Metrics**

- **Code Quality:** 85%+ mutation testing coverage
- **Security Score:** Zero critical vulnerabilities
- **Performance:** <2s page load times for generated apps
- **SuperClaude Validation:** 90%+ quality gate pass rate

---

## Conclusion

The enhanced VibeKit architecture with self-hosted ACI integration represents a paradigm shift in no-code development platforms. By combining:

- **V0-Clone Foundation:** Production-ready Next.js platform
- **BMAD Methodology:** Structured 5-phase development process
- **Self-Hosted ACI:** 600+ tool integrations for complete automation
- **VSA Architecture:** Maintainable, scalable generated applications
- **Quality Validation:** SuperClaude multi-perspective validation

We create the first platform that truly delivers on the promise of transforming business visions into production-ready applications without technical expertise.

**Key Differentiators:**

1. **Complete Solution:** Vision to live product in hours, not weeks
2. **Production-Ready:** Enterprise-grade applications from day one
3. **Self-Hosted Control:** Complete data privacy and cost predictability
4. **Zero Technical Debt:** Professional architecture and best practices
5. **Scalable Foundation:** Built to handle enterprise-scale deployments

This architecture positions VibeKit as the definitive no-code AI platform for the next generation of digital entrepreneurs and businesses.f-hosted on AWS with provided CDK deployment stack

- **Cost Control:** No per-API-call charges, fixed infrastructure costs
- **Data Privacy:** Complete control over user data and integration credentials
- **Custom Domain Management:** Automated DNS and SSL certificate provisioning
- **Monitoring & Analytics:** Integrated error tracking, performance monitoring, and user analytics

**Self-Hosting Architecture:**

```
┌─────────────────────────────────────────────────────────────────┐
│                    Self-Hosted ACI Platform                     │
├─────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │   FastAPI   │  │ PostgreSQL  │  │   600+      │              │
│  │   Backend   │  │  Database   │  │ Integrations│              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
├─────────────────────────────────────────────────────────────────┤
│  MCP Server Endpoint → BMAD Agents                              │
└─────────────────────────────────────────────────────────────────┘
```

#### 8. SuperClaude Quality Validation Layer (New)

**Technology:** SuperClaude Framework integration
**Purpose:** Quality assurance and sanity checking for BMAD agent outputs
**Integration:** Validation layer that runs after each BMAD agent phase
**Key Features:**

- **Multi-Perspective Validation:** 11 specialized personas for comprehensive review
- **Quality Gate Enforcement:** Automated validation with configurable thresholds
- **Error Detection:** Catch issues BMAD agents might miss through alternative analysis
- **Confidence Scoring:** Quantitative quality metrics for each phase output
- **Recommendation Engine:** Improvement suggestions based on validation results
- **Cross-Agent Consistency:** Ensure coherent outputs across BMAD phases

---

## Data Architecture

### Database Design Strategy

**Primary Database:** PostgreSQL with hybrid approach

- **Structured Data:** Traditional relational tables for users, projects, billing
- **Document Storage:** JSONB columns for flexible document storage
- **Benefits:** ACID compliance with NoSQL flexibility

### Data Models

#### Core Entities

**Users Table:**

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  name VARCHAR(255) NOT NULL,
  subscription_tier VARCHAR(50) DEFAULT 'free',
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

**Projects Table:**

```sql
CREATE TABLE projects (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id),
  name VARCHAR(255) NOT NULL,
  description TEXT,
  project_type VARCHAR(50) DEFAULT 'custom', -- 'ecommerce', 'saas', 'marketplace', 'blog', 'portfolio'
  status VARCHAR(50) DEFAULT 'draft', -- BMAD-aligned statuses
  workflow_state JSONB DEFAULT '{}',
  tech_stack JSONB DEFAULT '[]', -- Technologies used for learning
  template_id VARCHAR(100), -- Reference to project template used
  mcp_project_id VARCHAR(100), -- Memory Pickle project ID
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- BMAD Project Status Values:
-- 'draft', 'vision', 'requirements', 'prototyping', 'architecture', 'development', 'completed', 'paused', 'archived'
```

**Documents Table:**

```sql
CREATE TABLE documents (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id UUID REFERENCES projects(id),
  type VARCHAR(100) NOT NULL, -- 'prd', 'architecture', 'story', etc.
  title VARCHAR(255) NOT NULL,
  content JSONB NOT NULL,
  version INTEGER DEFAULT 1,
  created_by VARCHAR(100), -- agent type
  created_at TIMESTAMP DEFAULT NOW()
);
```

**Generated Applications Table:**

```sql
CREATE TABLE generated_applications (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id UUID REFERENCES projects(id),
  deployment_url VARCHAR(500),
  custom_domain VARCHAR(255),
  status VARCHAR(50) DEFAULT 'building',
  build_logs JSONB DEFAULT '[]',
  created_at TIMESTAMP DEFAULT NOW()
);
```

**User Sandbox Management Tables:**

```sql
-- User sandbox instances for complete isolation
CREATE TABLE user_sandboxes (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id),
  project_id UUID REFERENCES projects(id),
  sandbox_id VARCHAR(255) NOT NULL, -- VibeKit sandbox identifier
  sandbox_type VARCHAR(50) NOT NULL, -- 'e2b', 'northflank', 'daytona'
  status VARCHAR(50) DEFAULT 'active', -- 'active', 'paused', 'terminated'
  resources JSONB DEFAULT '{}', -- CPU, memory, storage allocation
  environment_vars JSONB DEFAULT '{}', -- Project-specific environment variables
  last_activity TIMESTAMP DEFAULT NOW(),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),

  -- Ensure unique sandbox per project
  UNIQUE(project_id, sandbox_type),
  -- Index for efficient user queries
  INDEX idx_user_sandboxes_user_id (user_id),
  INDEX idx_user_sandboxes_status (status)
);

-- Sandbox usage tracking for billing and optimization
CREATE TABLE sandbox_usage (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  sandbox_id UUID REFERENCES user_sandboxes(id),
  session_start TIMESTAMP NOT NULL,
  session_end TIMESTAMP,
  cpu_hours DECIMAL(10,4) DEFAULT 0,
  memory_gb_hours DECIMAL(10,4) DEFAULT 0,
  storage_gb_hours DECIMAL(10,4) DEFAULT 0,
  operations_count INTEGER DEFAULT 0,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Sandbox tier configurations
CREATE TABLE sandbox_tiers (
  id VARCHAR(50) PRIMARY KEY, -- 'free', 'premium', 'enterprise'
  name VARCHAR(100) NOT NULL,
  sandbox_type VARCHAR(50) NOT NULL, -- 'e2b', 'northflank', 'daytona'
  max_cpu_cores INTEGER NOT NULL,
  max_memory_gb INTEGER NOT NULL,
  max_storage_gb INTEGER NOT NULL,
  max_concurrent_sandboxes INTEGER NOT NULL,
  auto_pause_minutes INTEGER DEFAULT 30, -- Auto-pause after inactivity
  price_per_hour DECIMAL(10,4) DEFAULT 0,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Insert default sandbox tiers
INSERT INTO sandbox_tiers VALUES
('free', 'Free Tier', 'e2b', 2, 2, 5, 1, 15, 0.00),
('premium', 'Premium Tier', 'northflank', 4, 8, 20, 3, 60, 0.10),
('enterprise', 'Enterprise Tier', 'daytona', 8, 16, 50, 10, 120, 0.25);
```

**AI Fastify Template Integration Tables:**

```sql
-- Backend code generation tracking
CREATE TABLE backend_generations (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id UUID REFERENCES projects(id),
  feature_name VARCHAR(255) NOT NULL,
  generation_type VARCHAR(50) NOT NULL, -- 'vsa_feature', 'api_endpoint', 'service_layer'
  template_version VARCHAR(50) NOT NULL,
  quality_score DECIMAL(3,2) NOT NULL, -- Overall quality score (0.0-1.0)
  mutation_score DECIMAL(3,2) NOT NULL, -- Mutation testing score (0.0-1.0)
  security_score DECIMAL(3,2) NOT NULL, -- Security validation score (0.0-1.0)
  architecture_compliance BOOLEAN DEFAULT false,
  generated_files JSONB DEFAULT '[]', -- List of generated file paths
  quality_report JSONB DEFAULT '{}', -- Detailed quality metrics
  generation_time_ms INTEGER NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

-- AI Fastify Template patterns and learnings
CREATE TABLE fastify_patterns (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  pattern_type VARCHAR(100) NOT NULL, -- 'route', 'service', 'validation', 'test'
  pattern_name VARCHAR(255) NOT NULL,
  pattern_code TEXT NOT NULL, -- Template code pattern
  usage_count INTEGER DEFAULT 0,
  success_rate DECIMAL(3,2) DEFAULT 0.0,
  quality_metrics JSONB DEFAULT '{}',
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),

  UNIQUE(pattern_type, pattern_name)
);

-- Quality gate results tracking
CREATE TABLE quality_gate_results (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  backend_generation_id UUID REFERENCES backend_generations(id),
  gate_type VARCHAR(50) NOT NULL, -- 'lint', 'type_check', 'test', 'mutation', 'security'
  gate_status VARCHAR(20) NOT NULL, -- 'passed', 'failed', 'warning'
  execution_time_ms INTEGER NOT NULL,
  details JSONB DEFAULT '{}', -- Detailed results and metrics
  created_at TIMESTAMP DEFAULT NOW()
);

-- Insert default AI Fastify Template patterns
INSERT INTO fastify_patterns (pattern_type, pattern_name, pattern_code) VALUES
('route', 'crud_endpoint', 'fastify.register(async function (fastify) { /* CRUD template */ })'),
('service', 'business_logic', 'export class ServiceImplementation { /* Service template */ }'),
('validation', 'zod_schema', 'const Schema = z.object({ /* Validation template */ })'),
('test', 'comprehensive_test', 'describe("Feature", () => { /* Test template */ })');
```

**Self-Hosted ACI Integration Tables:**

```sql
-- ACI deployment tracking and management
CREATE TABLE aci_deployments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id UUID REFERENCES projects(id),
  deployment_type VARCHAR(50) NOT NULL, -- 'vercel', 'railway', 'fly_io', 'netlify'
  deployment_id VARCHAR(255) NOT NULL, -- External deployment identifier
  deployment_url VARCHAR(500) NOT NULL,
  custom_domain VARCHAR(255),
  status VARCHAR(50) DEFAULT 'deploying', -- 'deploying', 'active', 'failed', 'paused'

  -- ACI integration details
  aci_app_config_id VARCHAR(255), -- ACI app configuration reference
  aci_linked_account_id VARCHAR(255), -- ACI linked account reference

  -- Deployment configuration
  environment_vars JSONB DEFAULT '{}',
  build_settings JSONB DEFAULT '{}',

  -- Monitoring and logs
  last_deployment_at TIMESTAMP,
  deployment_logs JSONB DEFAULT '[]',
  error_logs JSONB DEFAULT '[]',

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- ACI service integrations tracking
CREATE TABLE aci_service_integrations (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id UUID REFERENCES projects(id),
  service_type VARCHAR(50) NOT NULL, -- 'database', 'monitoring', 'analytics', 'email', 'storage'
  service_name VARCHAR(100) NOT NULL, -- 'supabase', 'sentry', 'posthog', 'resend', 'cloudflare'

  -- ACI integration details
  aci_function_name VARCHAR(255) NOT NULL, -- ACI function used
  aci_linked_account_id VARCHAR(255), -- ACI linked account reference

  -- Service configuration
  service_config JSONB DEFAULT '{}',
  credentials_encrypted BOOLEAN DEFAULT true,

  -- Integration status
  status VARCHAR(50) DEFAULT 'configuring', -- 'configuring', 'active', 'failed', 'disabled'
  last_sync_at TIMESTAMP,
  sync_logs JSONB DEFAULT '[]',

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),

  UNIQUE(project_id, service_type, service_name)
);

-- ACI MCP server configuration and health
CREATE TABLE aci_mcp_server_config (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  server_endpoint VARCHAR(500) NOT NULL,
  server_status VARCHAR(50) DEFAULT 'active', -- 'active', 'maintenance', 'down'

  -- Authentication and security
  api_key_encrypted TEXT NOT NULL,
  rate_limit_per_minute INTEGER DEFAULT 1000,

  -- Available integrations
  available_integrations JSONB DEFAULT '[]', -- List of available ACI integrations
  enabled_integrations JSONB DEFAULT '[]', -- List of enabled integrations

  -- Health monitoring
  last_health_check TIMESTAMP DEFAULT NOW(),
  health_status JSONB DEFAULT '{}',
  uptime_percentage DECIMAL(5,2) DEFAULT 99.9,

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Insert default ACI MCP server configuration
INSERT INTO aci_mcp_server_config (server_endpoint, api_key_encrypted, available_integrations, enabled_integrations) VALUES
('http://localhost:8000/mcp', 'encrypted_api_key_here',
 '["VERCEL__DEPLOY_PROJECT", "SUPABASE__CREATE_PROJECT", "GITHUB__CREATE_REPOSITORY", "SENTRY__CREATE_PROJECT", "CLOUDFLARE__CONFIGURE_DOMAIN"]',
 '["VERCEL__DEPLOY_PROJECT", "SUPABASE__CREATE_PROJECT", "GITHUB__CREATE_REPOSITORY"]');
```

**Web-Eval-Agent QA/Debugging Tables:**

```sql
-- Web-Eval-Agent test execution tracking
CREATE TABLE web_eval_test_executions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id UUID REFERENCES projects(id),
  deployment_url VARCHAR(500) NOT NULL,
  test_task TEXT NOT NULL,
  execution_status VARCHAR(50) DEFAULT 'running', -- 'running', 'completed', 'failed', 'cancelled'

  -- Test configuration
  headless_browser BOOLEAN DEFAULT true,
  browser_type VARCHAR(50) DEFAULT 'chromium',
  test_timeout_seconds INTEGER DEFAULT 300,

  -- Test results
  test_passed BOOLEAN,
  ux_score DECIMAL(3,2), -- Overall UX score (0.0-1.0)
  performance_score DECIMAL(3,2), -- Performance score (0.0-1.0)
  accessibility_score DECIMAL(3,2), -- Accessibility score (0.0-1.0)

  -- Execution metrics
  execution_time_ms INTEGER,
  steps_completed INTEGER DEFAULT 0,
  total_steps INTEGER DEFAULT 0,

  -- Results data
  console_logs JSONB DEFAULT '[]',
  network_requests JSONB DEFAULT '[]',
  screenshots JSONB DEFAULT '[]',
  error_details JSONB DEFAULT '{}',

  created_at TIMESTAMP DEFAULT NOW(),
  completed_at TIMESTAMP,

  INDEX idx_web_eval_project_id (project_id),
  INDEX idx_web_eval_status (execution_status),
  INDEX idx_web_eval_created_at (created_at)
);

-- Detected issues and bugs from Web-Eval-Agent
CREATE TABLE web_eval_detected_issues (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  test_execution_id UUID REFERENCES web_eval_test_executions(id),
  project_id UUID REFERENCES projects(id),

  -- Issue classification
  issue_type VARCHAR(100) NOT NULL, -- 'console_error', 'network_failure', 'ux_issue', 'performance', 'accessibility'
  severity VARCHAR(20) NOT NULL, -- 'critical', 'high', 'medium', 'low'
  category VARCHAR(100), -- 'javascript_error', 'broken_link', 'slow_response', 'missing_alt_text', etc.

  -- Issue details
  title VARCHAR(255) NOT NULL,
  description TEXT NOT NULL,
  reproduction_steps JSONB DEFAULT '[]',

  -- Location information
  page_url VARCHAR(500),
  element_selector VARCHAR(500),
  line_number INTEGER,
  column_number INTEGER,

  -- Evidence
  screenshot_url VARCHAR(500),
  console_log_entry JSONB,
  network_request_data JSONB,

  -- Resolution tracking
  status VARCHAR(50) DEFAULT 'open', -- 'open', 'in_progress', 'resolved', 'ignored'
  resolution_notes TEXT,
  fixed_in_deployment_id UUID,

  created_at TIMESTAMP DEFAULT NOW(),
  resolved_at TIMESTAMP,

  INDEX idx_web_eval_issues_project_id (project_id),
  INDEX idx_web_eval_issues_severity (severity),
  INDEX idx_web_eval_issues_status (status),
  INDEX idx_web_eval_issues_type (issue_type)
);

-- Web-Eval-Agent fix recommendations
CREATE TABLE web_eval_fix_recommendations (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  detected_issue_id UUID REFERENCES web_eval_detected_issues(id),
  project_id UUID REFERENCES projects(id),

  -- Recommendation details
  recommendation_type VARCHAR(100) NOT NULL, -- 'code_fix', 'configuration_change', 'dependency_update'
  priority VARCHAR(20) NOT NULL, -- 'high', 'medium', 'low'

  -- Fix information
  title VARCHAR(255) NOT NULL,
  description TEXT NOT NULL,
  implementation_steps JSONB DEFAULT '[]',

  -- Code changes (if applicable)
  affected_files JSONB DEFAULT '[]',
  code_changes JSONB DEFAULT '{}', -- File path -> proposed changes

  -- Validation
  confidence_score DECIMAL(3,2) NOT NULL, -- AI confidence in recommendation (0.0-1.0)
  estimated_effort VARCHAR(50), -- 'low', 'medium', 'high'

  -- Implementation tracking
  status VARCHAR(50) DEFAULT 'pending', -- 'pending', 'approved', 'implemented', 'rejected'
  implementation_notes TEXT,
  implemented_by VARCHAR(100), -- 'ai_agent', 'human_developer'

  created_at TIMESTAMP DEFAULT NOW(),
  implemented_at TIMESTAMP,

  INDEX idx_web_eval_recommendations_issue_id (detected_issue_id),
  INDEX idx_web_eval_recommendations_priority (priority),
  INDEX idx_web_eval_recommendations_status (status)
);

-- Web-Eval-Agent configuration and health monitoring
CREATE TABLE web_eval_agent_config (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id UUID REFERENCES projects(id),

  -- Agent configuration
  default_test_timeout INTEGER DEFAULT 300,
  default_browser_type VARCHAR(50) DEFAULT 'chromium',
  headless_mode BOOLEAN DEFAULT true,

  -- Test scenarios and templates
  default_test_scenarios JSONB DEFAULT '[]',
  custom_test_templates JSONB DEFAULT '{}',

  -- Integration settings
  mcp_server_endpoint VARCHAR(500),
  operative_api_key_encrypted TEXT,

  -- Quality thresholds
  min_ux_score DECIMAL(3,2) DEFAULT 0.8,
  min_performance_score DECIMAL(3,2) DEFAULT 0.7,
  min_accessibility_score DECIMAL(3,2) DEFAULT 0.8,

  -- Health monitoring
  last_health_check TIMESTAMP DEFAULT NOW(),
  health_status VARCHAR(50) DEFAULT 'healthy', -- 'healthy', 'degraded', 'unhealthy'
  health_details JSONB DEFAULT '{}',

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),

  UNIQUE(project_id)
);

-- Insert default Web-Eval-Agent configuration
INSERT INTO web_eval_agent_config (project_id, default_test_scenarios) VALUES
(NULL, '["Test main user flows and report UX issues", "Verify all forms work correctly", "Check responsive design on mobile", "Test error handling and edge cases"]');
```

**SuperClaude Quality Validation Tables:**

```sql
-- SuperClaude validation results tracking
CREATE TABLE superclaude_validations (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id UUID REFERENCES projects(id),
  bmad_agent_type VARCHAR(50) NOT NULL, -- 'pm', 'architect', 'dev', 'qa', 'ux'
  bmad_phase VARCHAR(50) NOT NULL, -- 'vision', 'requirements', 'prototyping', 'architecture', 'development'
  validation_timestamp TIMESTAMP DEFAULT NOW(),

  -- Quality scores (0.0-1.0)
  overall_score DECIMAL(3,2) NOT NULL,
  confidence_score DECIMAL(3,2) NOT NULL,

  -- Detailed validation breakdown
  completeness_score DECIMAL(3,2) NOT NULL,
  accuracy_score DECIMAL(3,2) NOT NULL,
  consistency_score DECIMAL(3,2) NOT NULL,
  feasibility_score DECIMAL(3,2) NOT NULL,
  security_score DECIMAL(3,2) NOT NULL,
  performance_score DECIMAL(3,2) NOT NULL,

  -- SuperClaude command used
  superclaude_command VARCHAR(100) NOT NULL, -- '/sc:analyze', '/sc:troubleshoot', etc.
  command_flags JSONB DEFAULT '[]', -- Flags used in validation

  -- Validation results
  approved BOOLEAN DEFAULT false,
  approval_threshold DECIMAL(3,2) DEFAULT 0.85,
  requires_revision BOOLEAN DEFAULT false,

  -- Recommendations and issues
  recommendations JSONB DEFAULT '[]',
  critical_issues JSONB DEFAULT '[]',

  -- Processing metrics
  validation_time_ms INTEGER NOT NULL,
  token_usage INTEGER DEFAULT 0,

  created_at TIMESTAMP DEFAULT NOW()
);ndations JSONB DEFAULT '[]',
  critical_issues JSONB DEFAULT '[]',

  -- Processing metrics
  validation_time_ms INTEGER NOT NULL,
  token_usage INTEGER DEFAULT 0,

  created_at TIMESTAMP DEFAULT NOW()
);

-- SuperClaude persona analysis results
CREATE TABLE superclaude_persona_analysis (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  validation_id UUID REFERENCES superclaude_validations(id),
  persona_name VARCHAR(50) NOT NULL, -- 'architect', 'frontend', 'backend', 'analyzer', 'security', etc.
  persona_type VARCHAR(20) NOT NULL, -- 'primary', 'secondary'
  confidence_score DECIMAL(3,2) NOT NULL,
  analysis_text TEXT NOT NULL,
  recommendations JSONB DEFAULT '[]',
  created_at TIMESTAMP DEFAULT NOW()
);

-- Quality gate enforcement tracking
CREATE TABLE quality_gate_enforcement (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id UUID REFERENCES projects(id),
  bmad_phase VARCHAR(50) NOT NULL,
  validation_id UUID REFERENCES superclaude_validations(id),

  -- Gate status
  gate_status VARCHAR(20) NOT NULL, -- 'passed', 'failed', 'retry', 'escalated'
  retry_count INTEGER DEFAULT 0,
  max_retries INTEGER DEFAULT 2,

  -- Escalation handling
  escalated_to_human BOOLEAN DEFAULT false,
  escalation_reason TEXT,
  human_override BOOLEAN DEFAULT false,
  human_override_reason TEXT,

  -- Timing
  gate_execution_time_ms INTEGER NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  resolved_at TIMESTAMP
);

-- SuperClaude validation configuration
CREATE TABLE superclaude_validation_config (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id UUID REFERENCES projects(id),
  bmad_agent_type VARCHAR(50) NOT NULL,

  -- Quality thresholds
  overall_threshold DECIMAL(3,2) DEFAULT 0.85,
  completeness_threshold DECIMAL(3,2) DEFAULT 0.90,
  accuracy_threshold DECIMAL(3,2) DEFAULT 0.85,
  consistency_threshold DECIMAL(3,2) DEFAULT 0.80,
  feasibility_threshold DECIMAL(3,2) DEFAULT 0.85,
  security_threshold DECIMAL(3,2) DEFAULT 0.90,
  performance_threshold DECIMAL(3,2) DEFAULT 0.75,

  -- Validation behavior
  auto_retry_enabled BOOLEAN DEFAULT true,
  max_retries INTEGER DEFAULT 2,
  escalate_to_human BOOLEAN DEFAULT true,
  block_progression BOOLEAN DEFAULT true,

  -- Persona requirements
  require_multiple_personas BOOLEAN DEFAULT true,
  minimum_persona_confidence DECIMAL(3,2) DEFAULT 0.70,
  cross_persona_consistency DECIMAL(3,2) DEFAULT 0.80,

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),

  UNIQUE(project_id, bmad_agent_type)
);

-- Insert default SuperClaude validation configurations
INSERT INTO superclaude_validation_config (project_id, bmad_agent_type) VALUES
(NULL, 'pm'), -- Global default for PM agent
(NULL, 'architect'), -- Global default for Architect agent
(NULL, 'dev'), -- Global default for Dev agent
(NULL, 'qa'), -- Global default for QA agent
(NULL, 'ux'); -- Global default for UX agent
```

### Document Storage Strategy

**Template System:**

- **Storage:** File system with Git-based versioning
- **Format:** YAML templates with Markdown output
- **Categories:** PRD, Architecture, User Stories, Test Plans

**Generated Documents:**

- **Storage:** JSONB in PostgreSQL for searchability
- **Export:** On-demand generation to PDF, Word, Markdown
- **Versioning:** Full version history with diff tracking

### Memory Pickle MCP Data Models

**Project Templates Table:**

```sql
CREATE TABLE project_templates (
  id VARCHAR(100) PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  description TEXT,
  project_type VARCHAR(50) NOT NULL, -- 'ecommerce', 'saas', 'marketplace', etc.
  initial_tasks JSONB DEFAULT '[]',
  initial_memories JSONB DEFAULT '[]',
  tech_stack_suggestions JSONB DEFAULT '[]',
  bmad_phase_configs JSONB DEFAULT '{}',
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

**User Learning Context Table:**

```sql
CREATE TABLE user_learning_context (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id),
  context_type VARCHAR(50) NOT NULL, -- 'user_preference', 'project_type', 'tech_stack', 'platform'
  context_key VARCHAR(255) NOT NULL, -- e.g., 'react', 'ecommerce', 'user_123'
  insights JSONB NOT NULL,
  confidence_score DECIMAL(3,2) DEFAULT 0.5,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(user_id, context_type, context_key)
);
```

**MCP Session State Table:**

```sql
CREATE TABLE mcp_sessions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) UNIQUE, -- One session per user
  current_project_id UUID REFERENCES projects(id),
  session_data JSONB DEFAULT '{}',
  last_activity TIMESTAMP DEFAULT NOW(),
  created_at TIMESTAMP DEFAULT NOW()
);
```

**User Session Management Tables:**

```sql
-- Enhanced projects table with user isolation
CREATE TABLE projects (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id), -- USER ISOLATION
  name VARCHAR(255) NOT NULL,
  description TEXT,
  project_type VARCHAR(50) DEFAULT 'custom',
  status VARCHAR(50) DEFAULT 'draft',
  tech_stack JSONB DEFAULT '[]',
  mcp_project_id VARCHAR(100), -- Link to Memory Pickle project
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),

  -- Ensure user can only access their projects
  CONSTRAINT user_project_access CHECK (user_id IS NOT NULL)
);

-- Cross-user learning (anonymized)
CREATE TABLE project_insights (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_type VARCHAR(50) NOT NULL,
  tech_stack JSONB NOT NULL,
  success_patterns JSONB DEFAULT '[]',
  common_challenges JSONB DEFAULT '[]',
  best_practices JSONB DEFAULT '[]',
  confidence_score DECIMAL(3,2) DEFAULT 0.5,
  sample_size INTEGER DEFAULT 1,
  updated_at TIMESTAMP DEFAULT NOW()
);
```

---

## Agent System Architecture

### BMAD Framework Integration

The platform implements the proven BMAD methodology through specialized microservices, each embodying a specific agent role with defined responsibilities and capabilities.

#### Agent Service Pattern with Memory Pickle MCP Integration

Each agent service follows a consistent architectural pattern enhanced with Memory Pickle MCP for context management and SuperClaude quality validation:

```typescript
interface EnhancedAgentService {
  // Core agent operations
  processRequest(input: AgentInput): Promise<AgentOutput>;
  generateDocument(template: string, context: any): Promise<Document>;
  validateOutput(output: any): Promise<ValidationResult>;

  // Memory Pickle MCP integration
  initializeProject(
    name: string,
    description: string,
    type: string
  ): Promise<string>;
  recallProjectState(projectId?: string): Promise<ProjectContext>;
  rememberDecision(
    content: string,
    importance: "critical" | "high" | "medium" | "low"
  ): Promise<void>;
  createTask(
    title: string,
    description: string,
    priority: string
  ): Promise<string>;
  updateTaskProgress(
    taskId: string,
    progress: number,
    notes: string
  ): Promise<void>;

  // SuperClaude quality validation integration
  validateWithSuperClaude(
    output: AgentOutput,
    validationType: SuperClaudeValidationType
  ): Promise<SuperClaudeValidationResult>;
  getQualityScore(output: AgentOutput): Promise<QualityScore>;
  generateImprovementRecommendations(
    output: AgentOutput,
    validationResult: SuperClaudeValidationResult
  ): Promise<ImprovementRecommendation[]>;

  // Enhanced workflow integration
  getNextAgent(currentState: WorkflowState): Promise<string>;
  handoffToAgent(targetAgent: string, context: any): Promise<HandoffSummary>;
  generatePhaseHandoff(format: "detailed" | "brief"): Promise<string>;

  // Template management with learning
  loadTemplate(templateId: string): Promise<Template>;
  customizeTemplate(
    template: Template,
    preferences: any,
    learnings?: UserLearnings
  ): Promise<Template>;

  // Cross-project learning
  getUserInsights(): Promise<UserLearningContext>;
  getProjectTypeInsights(projectType: string): Promise<ProjectTypeInsights>;
  getTechStackInsights(techStack: string[]): Promise<TechStackInsights>;
}
```

#### SuperClaude Quality Validation Integration

**Enhanced BMAD Workflow with Quality Validation:**

```typescript
interface SuperClaudeQualityValidator {
  // Core validation operations
  validateAgentOutput(
    agentType: BMADAgentType,
    output: AgentOutput,
    validationCriteria: ValidationCriteria
  ): Promise<SuperClaudeValidationResult>;

  // Specialized validation by agent type
  validatePMOutput(pmOutput: PMAgentOutput): Promise<PMValidationResult>;
  validateArchitectureDesign(archOutput: ArchitectOutput): Promise<ArchitectureValidationResult>;
  validateGeneratedCode(devOutput: DevAgentOutput): Promise<CodeValidationResult>;
  validateQAResults(qaOutput: QAAgentOutput): Promise<QAValidationResult>;
  validateUXDesign(uxOutput: UXAgentOutput): Promise<UXValidationResult>;

  // Quality scoring and recommendations
  generateQualityScore(validationResults: ValidationResult[]): Promise<QualityScore>;
  generateImprovementRecommendations(
    output: AgentOutput,
    validationResult: SuperClaudeValidationResult
  ): Promise<ImprovementRecommendation[]>;

  // Cross-phase consistency validation
  validatePhaseConsistency(
    previousPhases: PhaseOutput[],
    currentPhase: PhaseOutput
  ): Promise<ConsistencyValidationResult>;
}

interface SuperClaudeValidationResult {
  validationId: string;
  agentType: BMADAgentType;
  timestamp: Date;

  // Quality metrics
  overallScore: number; // 0.0-1.0
  confidenceScore: number; // 0.0-1.0

  // Validation breakdown
  validationResults: {
    completeness: ValidationScore;
    accuracy: ValidationScore;
    consistency: ValidationScore;
    feasibility: ValidationScore;
    security: ValidationScore;
    performance: ValidationScore;
  };

  // SuperClaude persona insights
  personaAnalysis: {
    primaryPersona: SuperClaudePersona;
    secondaryPersonas: SuperClaudePersona[];
    insights: PersonaInsight[];
  };

  // Recommendations
  recommendations: ImprovementRecommendation[];
  criticalIssues: CriticalIssue[];

  // Approval status
  approved: boolean;
  approvalThreshold: number;
  requiresRevision: boolean;
}

interface SuperClaudePersona {
  name: string; // 'architect', 'frontend', 'backend', 'analyzer', 'security', etc.
  confidence: number;
  analysis: string;
  recommendations: string[];
}

interface EnhancedBMADWorkflow {
  // Enhanced phase execution with quality validation
  async executePhaseWithValidation(
    phase: BMADPhase,
    context: ProjectContext
  ): Promise<EnhancedPhaseResult> {
    // 1. Execute BMAD agent
    const bmadResult = await this.executeBMADAgent(phase, context);

    // 2. SuperClaude quality validation
    const validationResult = await this.superClaudeValidator.validateAgentOutput(
      phase.agentType,
      bmadResult,
      phase.validationCriteria
    );

    // 3. Quality gate enforcement
    if (!validationResult.approved) {
      if (validationResult.criticalIssues.length > 0) {
        throw new QualityGateFailureError(validationResult.criticalIssues);
      }

      // Auto-retry with recommendations if possible
      const improvedResult = await this.retryWithRecommendations(
        phase,
        bmadResult,
        validationResult.recommendations
      );

      return improvedResult;
    }

    // 4. Log quality metrics and learning
    await this.logQualityMetrics(validationResult);
    await this.updateLearningContext(phase, validationResult);

    return {
      bmadOutput: bmadResult,
      validationResult,
      qualityScore: validationResult.overallScore,
      approved: true,
      recommendations: validationResult.recommendations
    };
  }
}
```

**SuperClaude Command Integration for BMAD Agents:**

```typescript
interface SuperClaudeCommandIntegration {
  // PM Agent validation
  async validateRequirements(pmOutput: PMAgentOutput): Promise<ValidationResult> {
    return await this.executeSuperClaudeCommand({
      command: '/sc:analyze',
      content: pmOutput.requirements,
      flags: ['--focus', 'completeness', '--persona-analyzer', '--think'],
      validationType: 'requirements_analysis'
    });
  }

  // Architect Agent validation
  async validateArchitecture(archOutput: ArchitectOutput): Promise<ValidationResult> {
    return await this.executeSuperClaudeCommand({
      command: '/sc:troubleshoot',
      content: archOutput.architectureDocument,
      flags: ['--focus', 'architecture', '--persona-architect', '--think-hard'],
      validationType: 'architecture_review'
    });
  }

  // Dev Agent validation
  async validateGeneratedCode(devOutput: DevAgentOutput): Promise<ValidationResult> {
    return await this.executeSuperClaudeCommand({
      command: '/sc:improve',
      content: devOutput.generatedCode,
      flags: ['--focus', 'security', '--persona-security', '--safe-mode', '--validate'],
      validationType: 'code_quality_review'
    });
  }

  // QA Agent validation
  async validateTestStrategy(qaOutput: QAAgentOutput): Promise<ValidationResult> {
    return await this.executeSuperClaudeCommand({
      command: '/sc:test',
      content: qaOutput.testPlan,
      flags: ['--focus', 'quality', '--persona-qa', '--coverage'],
      validationType: 'test_strategy_review'
    });
  }

  // UX Agent validation
  async validateUXDesign(uxOutput: UXAgentOutput): Promise<ValidationResult> {
    return await this.executeSuperClaudeCommand({
      command: '/sc:design',
      content: uxOutput.designSpecs,
      flags: ['--focus', 'accessibility', '--persona-frontend', '--magic'],
      validationType: 'ux_design_review'
    });
  }
}
```

**Quality Gate Configuration:**

```typescript
interface QualityGateConfig {
  // Minimum scores required for approval
  thresholds: {
    overall: 0.85; // Overall quality score
    completeness: 0.9; // Requirements completeness
    accuracy: 0.85; // Technical accuracy
    consistency: 0.8; // Cross-phase consistency
    feasibility: 0.85; // Implementation feasibility
    security: 0.9; // Security compliance
    performance: 0.75; // Performance considerations
  };

  // Critical issue handling
  criticalIssueHandling: {
    autoRetry: true;
    maxRetries: 2;
    escalateToHuman: boolean;
    blockProgression: boolean;
  };

  // Persona-specific validation
  personaValidation: {
    requireMultiplePersonas: true;
    minimumPersonaConfidence: 0.7;
    crossPersonaConsistency: 0.8;
  };
}
```

#### Memory Pickle MCP Tool Integration by Agent

**PM Agent Enhanced Tools:**

```typescript
interface PMAgentMCPTools {
  // Project management
  create_project: (
    name: string,
    description: string,
    type: string
  ) => Promise<string>;
  update_project: (projectId: string, updates: ProjectUpdates) => Promise<void>;
  set_current_project: (projectId: string) => Promise<void>;

  // Requirements tracking
  create_task: (
    title: string,
    description: string,
    priority: string
  ) => Promise<string>;
  list_tasks: (filters: TaskFilters) => Promise<Task[]>;
  remember_this: (content: string, importance: string) => Promise<void>;

  // Phase transitions
  generate_handoff_summary: (format: "detailed") => Promise<string>;
}
```

**Architect Agent Enhanced Tools:**

```typescript
interface ArchitectAgentMCPTools {
  // Context recall
  recall_state: () => Promise<ProjectContext>;
  recall_context: (query: string, importance?: string) => Promise<Memory[]>;

  // Architecture decisions
  remember_this: (
    content: string,
    importance: "critical" | "high"
  ) => Promise<void>;
  create_task: (
    title: string,
    description: string,
    lineRange?: CodeLocation
  ) => Promise<string>;

  // Technical documentation
  export_session: (format: "markdown", includeHandoff: true) => Promise<string>;
}
```

**Dev Agent Enhanced Tools:**

```typescript
interface DevAgentMCPTools {
  // Development tracking
  get_task: (taskId: string) => Promise<TaskDetails>;
  update_task: (
    taskId: string,
    progress: number,
    notes: string[]
  ) => Promise<void>;
  list_tasks: (status: "active", priority?: string) => Promise<Task[]>;

  // Implementation context
  recall_context: (query: string) => Promise<Memory[]>;
  remember_this: (
    content: string,
    taskId: string,
    lineRange?: CodeLocation
  ) => Promise<void>;

  // VibeKit sandbox integration
  create_sandbox: (
    userId: string,
    projectId: string,
    tier: "free" | "premium" | "enterprise"
  ) => Promise<SandboxInstance>;
  execute_code: (
    sandboxId: string,
    code: string,
    language: string
  ) => Promise<ExecutionResult>;
  generate_vsa_feature: (
    featureName: string,
    requirements: string,
    projectContext: ProjectContext
  ) => Promise<VSAFeature>;
}
```

#### BMAD Backend Agent (AI Fastify Template Integration)

**Enhanced Backend Development Agent with Enterprise-Grade Code Generation:**

```typescript
interface BMADBackendAgent extends EnhancedAgentService {
  // AI Fastify Template integration
  fastifyTemplate: AIFastifyTemplate;
  qualityGates: EnterpriseQualityGates;

  // Backend-specific operations
  generateVSABackendFeature(
    featureName: string,
    requirements: FeatureRequirements,
    projectContext: ProjectContext
  ): Promise<VSABackendFeature>;

  generateFastifyAPI(
    apiSpec: APISpecification,
    validationSchemas: ZodSchemas
  ): Promise<FastifyApplication>;

  generateServiceLayer(
    businessLogic: BusinessLogicSpec,
    dataModels: DataModelSpec
  ): Promise<ServiceImplementation>;

  validateEnterpriseQuality(
    generatedCode: GeneratedCode
  ): Promise<QualityReport>;

  // AI Fastify Template specific tools
  runMutationTesting: (
    codebase: string,
    testSuite: string
  ) => Promise<MutationTestResult>;

  validateZodSchemas: (schemas: ZodSchemas) => Promise<ValidationResult>;

  generatePropertyTests: (
    businessLogic: BusinessFunction[]
  ) => Promise<PropertyTestSuite>;

  enforceArchitecturalBoundaries: (
    codeStructure: CodeStructure
  ) => Promise<ArchitecturalValidation>;
}
```

**AI Fastify Template Integration Architecture:**

```typescript
interface AIFastifyTemplateIntegration {
  // Template-based code generation
  templateEngine: {
    routeTemplate: FastifyRouteTemplate;
    serviceTemplate: ServiceLayerTemplate;
    validationTemplate: ZodValidationTemplate;
    testTemplate: ComprehensiveTestTemplate;
  };

  // Quality assurance pipeline
  qualityPipeline: {
    linting: ESLintWithCustomRules;
    typeChecking: StrictTypeScriptValidation;
    testing: ViTestWithMutationTesting;
    security: GitLeaksAndAuditCI;
    architecture: DependencyCruiserValidation;
  };

  // Enterprise patterns
  enterprisePatterns: {
    errorHandling: FastifyErrorPatterns;
    logging: StructuredLogging;
    validation: ZodSchemaValidation;
    security: SecurityFirstPatterns;
    monitoring: OpenTelemetryIntegration;
  };
}
```

**Backend Code Generation Workflow:**

```typescript
export class BMADBackendAgentImplementation implements BMADBackendAgent {
  constructor(
    private vibeKit: VibeKit,
    private fastifyTemplate: AIFastifyTemplate,
    private mcpClient: MemoryPickleMCP
  ) {}

  async generateVSABackendFeature(
    featureName: string,
    requirements: FeatureRequirements,
    projectContext: ProjectContext
  ): Promise<VSABackendFeature> {
    // 1. Recall project context and patterns
    const context = await this.mcpClient.recallProjectState();
    const existingPatterns = await this.mcpClient.recall_context(
      `backend patterns for ${projectContext.projectType}`
    );

    // 2. Generate VSA-compliant backend structure
    const backendStructure = await this.fastifyTemplate.generateVSAStructure({
      featureName,
      requirements,
      context: { ...context, patterns: existingPatterns }
    });

    // 3. Generate enterprise-grade code components
    const components = await Promise.all([
      this.generateFastifyRoutes(featureName, requirements),
      this.generateServiceLayer(featureName, requirements),
      this.generateZodValidation(requirements.inputSchemas),
      this.generateComprehensiveTests(featureName, requirements),
      this.generateTypeDefinitions(requirements.dataModels)
    ]);

    // 4. Execute in VibeKit sandbox with quality validation
    const sandboxResult = await this.vibeKit.executeInSandbox({
      code: this.combineComponents(components),
      validationPipeline: [
        'lint', 'type-check', 'test', 'mutation-test', 'security-scan'
      ]
    });

    // 5. Ensure enterprise quality gates pass
    const qualityReport = await this.validateEnterpriseQuality(sandboxResult);
    if (qualityReport.mutationScore < 0.85) {
      throw new Error('Mutation testing threshold not met');
    }

    // 6. Remember successful patterns for future use
    await this.mcpClient.remember_this(
      `Successful ${featureName} backend pattern: ${qualityReport.summary}`,
      'high'
    );

    return {
      featureName,
      structure: backendStructure,
      components,
      qualityReport,
      deploymentReady: true
    };
  }

  private async generateFastifyRoutes(
    featureName: string,
    requirements: FeatureRequirements
  ): Promise<FastifyRoutes> {
    return this.fastifyTemplate.generateFromTemplate('route', {
      featureName,
      endpoints: requirements.endpoints,
      validation: requirements.validation,
      errorHandling: 'fastify-patterns',
      security: 'zod-validation'
    });
  }

  private async generateServiceLayer(
    featureName: string,
    requirements: FeatureRequirements
  ): Promise<ServiceLayer> {
    return this.fastifyTemplate.generateFromTemplate('service', {
      featureName,
      businessLogic: requirements.businessLogic,
      dataAccess: requirements.dataAccess,
      logging: 'structured',
      errorHandling: 'comprehensive'
    });
  }

  private async validateEnterpriseQuality(
    code: GeneratedCode
  ): Promise<QualityReport> {
    // Run AI Fastify Template quality pipeline
    const results = await Promise.all([
      this.runMutationTesting(code.businessLogic, code.tests),
      this.validateZodSchemas(code.validationSchemas),
      this.enforceArchitecturalBoundaries(code.structure),
      this.runSecurityScan(code.fullCodebase)
    ]);

    return {
      mutationScore: results[0].score,
      validationCoverage: results[1].coverage,
      architecturalCompliance: results[2].compliance,
      securityScore: results[3].score,
      overallGrade: this.calculateOverallGrade(results),
      deploymentReady: results.every(r => r.passed)
    };
  }
}ndbox: (
    userId: string,
    projectId: string,
    tier: "free" | "premium" | "enterprise"
  ) => Promise<SandboxInstance>;
  execute_code: (
    sandboxId: string,
    code: string,
    language: string
  ) => Promise<ExecutionResult>;
  generate_vsa_feature: (
    featureName: string,
    requirements: string,
    projectContext: ProjectContext
  ) => Promise<VSAFeature>;
}
```

#### VibeKit Integration Architecture

**Enhanced BMAD Agents with VibeKit Sandbox Isolation:**

```typescript
interface VibeKitEnhancedAgent {
  // User isolation
  userId: string;
  projectId: string;
  sandboxManager: UserSandboxManager;

  // VibeKit integration
  vibeKit: VibeKit;
  sandboxConfig: SandboxConfig;

  // Enhanced capabilities
  generateIsolatedCode(
    prompt: string,
    context: ProjectContext
  ): Promise<CodeResult>;
  executeInSandbox(code: string, environment: string): Promise<ExecutionResult>;
  createVSAFeature(featureSpec: FeatureSpecification): Promise<VSAFeature>;
  validateFeatureIsolation(feature: VSAFeature): Promise<ValidationResult>;
}
```

**User Sandbox Manager:**

```typescript
interface UserSandboxManager {
  // Sandbox lifecycle
  createSandbox(
    userId: string,
    projectId: string,
    tier: SandboxTier
  ): Promise<SandboxInstance>;
  pauseSandbox(sandboxId: string): Promise<void>;
  resumeSandbox(sandboxId: string): Promise<void>;
  terminateSandbox(sandboxId: string): Promise<void>;

  // Resource management
  getSandboxUsage(sandboxId: string): Promise<UsageMetrics>;
  optimizeResources(userId: string): Promise<OptimizationResult>;

  // Multi-tier support
  upgradeSandbox(sandboxId: string, newTier: SandboxTier): Promise<void>;
  getSandboxTier(userId: string): Promise<SandboxTier>;
}
```

**VSA-Aware Code Generation:**

```typescript
interface VSACodeGenerator {
  // Feature generation
  generateFeature(
    featureName: string,
    requirements: FeatureRequirements,
    projectContext: ProjectContext
  ): Promise<VSAFeature>;

  // Feature validation
  validateFeatureIsolation(feature: VSAFeature): Promise<IsolationReport>;
  validateFeatureIntegration(
    feature: VSAFeature,
    existingFeatures: VSAFeature[]
  ): Promise<IntegrationReport>;

  // Code quality
  generateTests(feature: VSAFeature): Promise<TestSuite>;
  generateDocumentation(feature: VSAFeature): Promise<Documentation>;
}
```

````

#### Agent Communication Protocol

**Synchronous Communication:**

- Direct HTTP calls for immediate responses
- Used for validation and quick queries

**Asynchronous Communication:**

- Event-driven messaging for workflow progression
- Document generation and processing tasks

**Document Handoffs:**

```typescript
interface AgentHandoff {
  fromAgent: string;
  toAgent: string;
  projectId: string;
  documents: Document[];
  context: {
    phase: WorkflowPhase;
    userPreferences: any;
    constraints: any;
  };
  instructions: string;
}
````

### Workflow State Management

**State Machine Implementation:**

```typescript
interface WorkflowState {
  projectId: string;
  currentPhase:
    | "vision"
    | "requirements"
    | "prototyping"
    | "architecture"
    | "development";
  currentAgent: string;
  completedSteps: string[];
  pendingTasks: Task[];
  documents: DocumentReference[];
  userDecisions: Decision[];
}
```

**Phase Transitions:**

- Automated progression based on completion criteria
- User approval gates for major phase transitions
- Rollback capability for iterative refinement

---

## VibeKit Integration Strategy

### User Isolation Architecture

**Core Problem Solved:** Complete isolation between users and projects to prevent interference, data leakage, and resource conflicts.

**VibeKit Solution:** Each user project gets its own dedicated sandbox environment with configurable resource allocation and automatic lifecycle management.

#### Sandbox Tier Strategy

**Free Tier (E2B):**

```typescript
const freeTierConfig: SandboxConfig = {
  type: "e2b",
  apiKey: process.env.E2B_API_KEY,
  templateId: "vibekit-nextjs-basic",
  resources: {
    cpu: 2,
    memory: 2048, // 2GB
    storage: 5120, // 5GB
    maxConcurrent: 1,
    autoPauseMinutes: 15,
  },
};
```

**Premium Tier (Northflank):**

```typescript
const premiumTierConfig: SandboxConfig = {
  type: "northflank",
  apiKey: process.env.NORTHFLANK_API_KEY,
  projectId: user.northflankProjectId,
  resources: {
    cpu: 4,
    memory: 8192, // 8GB
    storage: 20480, // 20GB
    maxConcurrent: 3,
    autoPauseMinutes: 60,
  },
};
```

**Enterprise Tier (Daytona):**

```typescript
const enterpriseTierConfig: SandboxConfig = {
  type: "daytona",
  apiKey: process.env.DAYTONA_API_KEY,
  serverUrl: process.env.DAYTONA_SERVER_URL,
  resources: {
    cpu: 8,
    memory: 16384, // 16GB
    storage: 51200, // 50GB
    maxConcurrent: 10,
    autoPauseMinutes: 120,
  },
};
```

#### Enhanced BMAD Agent Integration

**Dev Agent with VibeKit Sandbox:**

```typescript
export class EnhancedDevAgent extends BaseAgent {
  private vibeKit: VibeKit;
  private sandboxManager: UserSandboxManager;

  constructor(userProject: UserProject) {
    super();
    this.sandboxManager = new UserSandboxManager(userProject.userId);
    this.vibeKit = new VibeKit({
      agent: {
        type: this.selectAgentType(userProject.preferences),
        model: {
          apiKey: this.getModelApiKey(userProject.modelProvider),
          provider: userProject.modelProvider,
        },
      },
      environment: this.getSandboxConfig(userProject.tier),
      github: {
        token: userProject.githubToken,
        repository: userProject.repository,
      },
      sessionId: userProject.sessionId,
      workingDirectory: `/projects/${userProject.id}`,
    });
  }

  async generateVSAFeature(
    featureName: string,
    requirements: FeatureRequirements
  ): Promise<VSAFeature> {
    // Ensure sandbox is active
    await this.sandboxManager.ensureActive(this.userProject.id);

    const prompt = this.buildVSAPrompt(featureName, requirements);

    const result = await this.vibeKit.generateCode({
      prompt,
      mode: "code",
      branch: `feature/${featureName}`,
      callbacks: {
        onUpdate: (message) => this.streamToUser(message),
        onError: (error) => this.handleError(error),
      },
    });

    return this.parseVSAFeature(result);
  }

  private buildVSAPrompt(name: string, reqs: FeatureRequirements): string {
    return `
Generate a complete VSA feature for "${name}" with the following requirements:
${reqs.description}

CRITICAL VSA Requirements:
1. Create complete vertical slice in features/${name}/
2. Include: API routes, components, services, database models, tests
3. NO dependencies on other features (except shared utilities)
4. Follow established patterns from existing features
5. Ensure complete feature isolation

Structure:
features/${name}/
├── api/${name}-routes.ts
├── components/${name}Components.tsx
├── services/${name}.service.ts
├── database/${name}.model.ts
├── types/${name}.types.ts
└── tests/${name}.test.ts

Generate production-ready, type-safe code following Next.js 15 best practices.
    `;
  }
}
```

#### Sandbox Lifecycle Management

**Automatic Resource Optimization:**

```typescript
interface SandboxLifecycleManager {
  // Automatic pause/resume based on activity
  scheduleAutoPause(sandboxId: string, inactivityMinutes: number): void;
  resumeOnDemand(sandboxId: string): Promise<void>;

  // Resource monitoring
  monitorUsage(sandboxId: string): Promise<UsageMetrics>;
  optimizeResources(userId: string): Promise<OptimizationResult>;

  // Billing integration
  trackUsage(sandboxId: string, operation: string): Promise<void>;
  generateUsageReport(userId: string, period: DateRange): Promise<UsageReport>;
}
```

#### Multi-Project Context Management

**Project Isolation with Cross-Project Learning:**

```typescript
interface ProjectContextManager {
  // Isolated project contexts
  createProjectContext(
    userId: string,
    projectId: string
  ): Promise<IsolatedProjectContext>;

  // Cross-project insights (anonymized)
  getProjectTypeInsights(projectType: string): Promise<ProjectInsights>;
  getUserPatterns(userId: string): Promise<UserPatterns>;

  // Template recommendations
  suggestTemplates(
    userHistory: UserHistory,
    projectType: string
  ): Promise<TemplateRecommendations>;
}
```

---

## AI/LLM Integration Architecture

### Multi-Provider LLM Strategy

**Provider Abstraction Layer:**

```typescript
interface LLMProvider {
  name: string;
  models: string[];
  capabilities: string[];

  generateCompletion(prompt: string, options: any): Promise<string>;
  streamCompletion(prompt: string, options: any): AsyncIterator<string>;
  validateCredentials(credentials: any): Promise<boolean>;
}
```

**Supported Providers:**

- **OpenAI:** GPT-4, GPT-3.5-turbo for general tasks
- **Anthropic:** Claude for complex reasoning and analysis
- **Google AI:** Gemini for large context requirements
- **User BYOLLM:** Custom API endpoints with credential management

### LLM Routing Strategy

**Agent-Specific Model Selection:**

- **PM Agent:** GPT-4 for requirement analysis and documentation
- **Architect Agent:** Claude for complex system design reasoning
- **Developer Agent:** GPT-4 for code generation and debugging
- **QA Agent:** GPT-3.5-turbo for test case generation
- **UX Agent:** GPT-4 for design and user experience tasks

**Fallback Strategy:**

1. Primary model (user preference or agent default)
2. Secondary model (platform default)
3. Graceful degradation with user notification

### Context Management

**Template-Based Context:**

- Structured prompts using proven templates
- Context injection based on project phase and history
- Token optimization through intelligent summarization

**Document Context Integration:**

```typescript
interface ContextBuilder {
  buildAgentContext(agent: string, project: Project): Promise<string>;
  injectDocumentContext(basePrompt: string, documents: Document[]): string;
  optimizeTokenUsage(context: string, maxTokens: number): string;
}
```

#### Implementation Roadmap

**Phase 1: Foundation (Weeks 1-4)**

```typescript
// MVP Implementation with E2B sandboxes + AI Fastify Template + SuperClaude QA
const mvpImplementation = {
  sandboxProvider: "e2b",
  supportedAgents: ["claude", "codex"],
  backendAgent: "ai-fastify-template-integration",
  qualityValidator: "superclaude-quality-validation",
  userTiers: ["free"],
  maxConcurrentSandboxes: 1,
  features: [
    "basic user isolation",
    "VSA backend generation with AI Fastify Template",
    "enterprise-grade quality gates (85% mutation testing)",
    "SuperClaude multi-perspective validation",
    "automated quality scoring and recommendations",
    "GitHub integration",
    "session persistence",
    "Zod validation enforcement",
    "comprehensive testing pipeline",
  ],
};
```

**Phase 2: Multi-Tier Support (Weeks 5-8)**

```typescript
// Add Northflank for premium users
const premiumImplementation = {
  sandboxProviders: ["e2b", "northflank"],
  supportedAgents: ["claude", "codex", "gemini"],
  userTiers: ["free", "premium"],
  features: [
    "tier-based resource allocation",
    "advanced VSA patterns",
    "cost optimization",
    "usage analytics",
  ],
};
```

**Phase 3: Enterprise Features (Weeks 9-12)**

```typescript
// Full enterprise deployment
const enterpriseImplementation = {
  sandboxProviders: ["e2b", "northflank", "daytona"],
  supportedAgents: ["claude", "codex", "gemini", "opencode"],
  userTiers: ["free", "premium", "enterprise"],
  features: [
    "custom sandbox configurations",
    "advanced security policies",
    "compliance frameworks",
    "white-label deployment",
  ],
};
```

#### Cost Optimization Strategy

**Automatic Resource Management:**

```typescript
interface CostOptimizationEngine {
  // Predictive scaling
  predictUsage(userId: string, timeWindow: number): Promise<UsagePrediction>;
  optimizeResourceAllocation(sandboxId: string): Promise<OptimizationResult>;

  // Smart pause/resume
  scheduleAutoPause(sandboxId: string, inactivityThreshold: number): void;
  preemptiveResume(userId: string, predictedActivity: ActivityPrediction): void;

  // Cost monitoring
  trackRealTimeCosts(sandboxId: string): Promise<CostMetrics>;
  generateCostAlerts(userId: string, threshold: number): Promise<Alert[]>;

  // Resource pooling
  shareResourcesAcrossUsers(region: string): Promise<PoolingResult>;
  optimizeRegionalDistribution(): Promise<DistributionPlan>;
}
```

**Billing Integration:**

```typescript
interface BillingIntegration {
  // Usage-based billing
  calculateUsageCosts(
    userId: string,
    period: DateRange
  ): Promise<BillingAmount>;
  applyTierDiscounts(
    usage: UsageMetrics,
    tier: UserTier
  ): Promise<DiscountedAmount>;

  // Real-time cost tracking
  trackOperationCosts(operation: SandboxOperation): Promise<void>;
  generateUsageReports(userId: string): Promise<UsageReport>;

  // Budget controls
  setBudgetLimits(userId: string, limits: BudgetLimits): Promise<void>;
  enforceSpendingLimits(userId: string): Promise<EnforcementResult>;
}
```

---

## Security Architecture

### Authentication & Authorization

**Authentication Strategy:**

- **Primary:** OAuth 2.0 with JWT tokens
- **Providers:** Google, GitHub, email/password
- **Session Management:** Secure HTTP-only cookies with refresh tokens

**Authorization Model:**

```typescript
interface UserPermissions {
  userId: string;
  projectPermissions: {
    [projectId: string]: "owner" | "collaborator" | "viewer";
  };
  platformPermissions: string[];
  sandboxPermissions: {
    [sandboxId: string]: "execute" | "read" | "admin";
  };
}
```

**API Security:**

- Rate limiting per user and IP
- Request validation and sanitization
- CORS configuration for web

### VibeKit Sandbox Security

**Complete User Isolation:**

```typescript
interface SandboxSecurityModel {
  // Network isolation
  networkPolicy: {
    ingressRules: NetworkRule[];
    egressRules: NetworkRule[];
    isolatedFromOtherUsers: boolean;
  };

  // Resource isolation
  resourceLimits: {
    cpu: string; // e.g., "2000m"
    memory: string; // e.g., "4Gi"
    storage: string; // e.g., "10Gi"
    networkBandwidth: string; // e.g., "100Mbps"
  };

  // File system isolation
  fileSystemSecurity: {
    readOnlyRootFS: boolean;
    tmpfsMount: boolean;
    userNamespaceIsolation: boolean;
    seLinuxContext: string;
  };

  // Process isolation
  processIsolation: {
    pidNamespace: boolean;
    userNamespace: boolean;
    mountNamespace: boolean;
    networkNamespace: boolean;
  };
}
```

**Multi-Tier Security Policies:**

```typescript
// Free Tier - Basic isolation
const freeTierSecurity: SandboxSecurityModel = {
  networkPolicy: {
    ingressRules: [{ port: 3000, protocol: "HTTP" }],
    egressRules: [
      { destination: "github.com", protocol: "HTTPS" },
      { destination: "npmjs.org", protocol: "HTTPS" },
    ],
    isolatedFromOtherUsers: true,
  },
  resourceLimits: {
    cpu: "1000m",
    memory: "2Gi",
    storage: "5Gi",
    networkBandwidth: "50Mbps",
  },
  fileSystemSecurity: {
    readOnlyRootFS: true,
    tmpfsMount: true,
    userNamespaceIsolation: true,
    seLinuxContext: "container_t",
  },
};

// Premium Tier - Enhanced security + performance
const premiumTierSecurity: SandboxSecurityModel = {
  networkPolicy: {
    ingressRules: [
      { port: 3000, protocol: "HTTP" },
      { port: 8000, protocol: "HTTP" },
    ],
    egressRules: [
      { destination: "*", protocol: "HTTPS" }, // More permissive
      { destination: "api.stripe.com", protocol: "HTTPS" },
    ],
    isolatedFromOtherUsers: true,
  },
  resourceLimits: {
    cpu: "4000m",
    memory: "8Gi",
    storage: "20Gi",
    networkBandwidth: "200Mbps",
  },
  fileSystemSecurity: {
    readOnlyRootFS: true,
    tmpfsMount: true,
    userNamespaceIsolation: true,
    seLinuxContext: "container_t",
  },
};
```

**Sandbox Security Monitoring:**

```typescript
interface SandboxSecurityMonitoring {
  // Real-time threat detection
  threatDetection: {
    suspiciousProcessMonitoring: boolean;
    networkAnomalyDetection: boolean;
    fileSystemIntegrityChecking: boolean;
    resourceUsageAnomalies: boolean;
  };

  // Audit logging
  auditLogging: {
    allAPICallsLogged: boolean;
    fileSystemAccessLogged: boolean;
    networkConnectionsLogged: boolean;
    processExecutionLogged: boolean;
  };

  // Automatic response
  automaticResponse: {
    suspendOnThreatDetection: boolean;
    alertSecurityTeam: boolean;
    quarantineSuspiciousFiles: boolean;
    rateLimit: boolean;
  };
}
```

**Data Protection in Sandboxes:**

- **Encryption at Rest:** All sandbox storage encrypted with AES-256
- **Encryption in Transit:** TLS 1.3 for all communications
- **Memory Protection:** Secure memory allocation and cleanup
- **Secrets Management:** Environment variables encrypted and rotated
- **Code Isolation:** User code cannot access other users' data
- **Temporary Storage:** Automatic cleanup of temporary files

**Compliance & Governance:**

````typescript
interface ComplianceFramework {
  // Data residency
  dataResidency: {
    region: string; // User-specified region
    crossBorderDataTransfer: boolean;
    dataLocalizationCompliance: string[];
  };

  // Regulatory compliance
  compliance: {
    gdprCompliant: boolean;
    ccpaCompliant: boolean;
    soc2Type2: boolean;
    iso27001: boolean;
    hipaaReady: boolean; // For healthcare projects
  };

  // Data retention
  dataRetention: {
    sandboxDataRetentionDays: number;
    logRetentionDays: number;
    backupRetentionDays: number;
    automaticDataPurging: boolean;
  };
}
``` clients

### Data Security

**Encryption:**

- **At Rest:** AES-256 encryption for sensitive data
- **In Transit:** TLS 1.3 for all communications
- **Database:** Encrypted PostgreSQL with column-level encryption for PII

**User Data Protection:**

- **BYOLLM Credentials:** Encrypted storage with user-controlled access
- **Generated Code:** User owns all generated intellectual property
- **Project Data:** Isolated per user with no cross-contamination

**Compliance:**

- **GDPR:** Right to deletion, data portability, consent management
- **SOC 2:** Security controls and audit logging
- **Privacy:** No training on user data, explicit consent for analytics

---

## Deployment Architecture

### Container Strategy

**Docker Configuration:**

```dockerfile
# Example agent service Dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY dist/ ./dist/
EXPOSE 3000
CMD ["node", "dist/index.js"]
````

**Kubernetes Deployment:**

- **Namespace Isolation:** Separate namespaces for different environments
- **Resource Limits:** CPU and memory limits for cost control
- **Health Checks:** Liveness and readiness probes for all services

### Environment Management

**Development Environment:**

- **Local:** Docker Compose for full stack development
- **Cloud:** Dedicated EKS cluster for integration testing
- **Database:** Local PostgreSQL with test data

**Staging Environment:**

- **Purpose:** Production-like testing and user acceptance
- **Scale:** Reduced replica counts for cost optimization
- **Data:** Anonymized production data subset

**Production Environment:**

- **High Availability:** Multi-AZ deployment with auto-scaling
- **Monitoring:** Comprehensive observability stack
- **Backup:** Automated daily backups with point-in-time recovery

### Generated Application Deployment

**Deployment Pipeline:**

1. **Code Generation:** Agent services generate complete application code
2. **Quality Validation:** Automated testing and security scanning
3. **Container Building:** Docker image creation with optimized layers
4. **Environment Provisioning:** Automated subdomain and SSL setup
5. **Application Deployment:** Zero-downtime deployment to user environment

**Infrastructure as Code:**

```yaml
# Example Terraform configuration for user app deployment
resource "aws_ecs_service" "user_app" {
name            = "user-app-${var.project_id}"
cluster         = aws_ecs_cluster.apps.id
task_definition = aws_ecs_task_definition.user_app.arn
desired_count   = 1

load_balancer {
target_group_arn = aws_lb_target_group.user_app.arn
container_name   = "app"
container_port   = 3000
}
}
```

---

## Performance & Scalability

### Scalability Strategy

**Horizontal Scaling:**

- **Agent Services:** Auto-scaling based on queue depth and CPU usage
- **Database:** Read replicas for query optimization
- **CDN:** Global content delivery for static assets

**Performance Targets:**

- **API Response Time:** < 2 seconds for 95% of requests
- **Document Generation:** < 30 seconds for complex documents
- **Application Deployment:** < 10 minutes for full stack applications
- **Concurrent Users:** Support for 10,000+ simultaneous users

### Caching Strategy

**Multi-Level Caching:**

```typescript
interface CacheStrategy {
  // Application level
  documentTemplates: "memory"; // Frequently used templates
  userSessions: "redis"; // Session data and preferences

  // Database level
  queryResults: "redis"; // Expensive query results
  documentContent: "cdn"; // Static document exports

  // CDN level
  staticAssets: "cloudfront"; // Images, CSS, JS files
  generatedApps: "cloudfront"; // Deployed user applications
}
```

### Monitoring & Observability

**Application Monitoring:**

- **APM:** Datadog or New Relic for performance monitoring
- **Logging:** Structured logging with ELK stack
- **Metrics:** Prometheus and Grafana for custom metrics
- **Alerting:** PagerDuty integration for critical issues

**Business Metrics:**

- **User Journey Analytics:** Track completion rates by phase
- **Agent Performance:** Monitor success rates and user satisfaction
- **Platform Health:** System availability and response times
- **Cost Optimization:** Resource usage and efficiency metrics

---

## Integration Architecture

### External Service Integration

**LLM Provider Integration:**

```typescript
interface ExternalIntegration {
  // AI/LLM Services
  openai: OpenAIConfig;
  anthropic: AnthropicConfig;
  google: GoogleAIConfig;

  // Development Tools
  github: GitHubIntegration;
  vercel: VercelDeployment;

  // Business Services
  stripe: PaymentProcessing;
  sendgrid: EmailDelivery;

  // Analytics
  mixpanel: UserAnalytics;
  sentry: ErrorTracking;
}
```

**API Rate Limiting:**

- **Provider Limits:** Respect individual provider rate limits
- **User Quotas:** Enforce subscription-based usage limits
- **Graceful Degradation:** Queue requests during peak usage

### BYOLLM Integration

**User Credential Management:**

```typescript
interface BYOLLMConfig {
  userId: string;
  provider: "openai" | "anthropic" | "custom";
  credentials: EncryptedCredentials;
  preferences: {
    defaultModel: string;
    maxTokens: number;
    temperature: number;
  };
  usage: {
    tokensUsed: number;
    requestCount: number;
    lastUsed: Date;
  };
}
```

**Security Considerations:**

- **Credential Encryption:** AES-256 encryption with user-specific keys
- **Access Isolation:** User credentials never shared between projects
- **Audit Logging:** Complete audit trail of credential usage

---

## Development Workflow

### Local Development Setup

**Prerequisites:**

- Node.js 20+ LTS
- Docker and Docker Compose
- PostgreSQL 15+
- pnpm package manager

**Quick Start:**

```bash
# Clone repository
git clone <repository-url>
cd no-code-ai-platform

# Install dependencies
pnpm install

# Start development environment
docker-compose up -d postgres redis
pnpm dev

# Run tests
pnpm test
```

**Development Services:**

- **Frontend:** http://localhost:3000
- **API Gateway:** http://localhost:3001
- **Agent Services:** http://localhost:3002-3007
- **Memory Pickle MCP:** http://localhost:3008
- **Database:** postgresql://localhost:5432

### Memory Pickle MCP Development Configuration

**MCP Server Configuration:**

```json
{
  "mcpServers": {
    "memory-pickle": {
      "command": "npx",
      "args": ["-y", "@cabbages/memory-pickle-mcp"],
      "env": {
        "NODE_ENV": "development"
      }
    }
  }
}
```

**VibeKit Memory Manager Implementation:**

```typescript
// VibeKit Memory Manager Wrapper Implementation
export class VibeKitMemoryManager {
  private static userSessions = new Map<string, MemoryPickleSession>();
  private userId: string;
  private userDatabase: UserDatabase;

  constructor(userId: string) {
    this.userId = userId;
    this.userDatabase = new UserDatabase();
  }

  // Get or create user-specific MCP session
  private async getUserSession(): Promise<MemoryPickleSession> {
    if (!VibeKitMemoryManager.userSessions.has(this.userId)) {
      const session = await MemoryPickleCore.create();
      await this.restoreUserProjects(session);
      VibeKitMemoryManager.userSessions.set(this.userId, session);
    }
    return VibeKitMemoryManager.userSessions.get(this.userId)!;
  }

  // Enhanced project creation with user context
  async createProject(params: {
    name: string;
    description: string;
    type: "ecommerce" | "saas" | "marketplace";
    techStack?: string[];
  }): Promise<UserProject> {
    const session = await this.getUserSession();

    // 1. Create project in Memory Pickle
    const mcpProject = await session.create_project({
      name: params.name,
      description: params.description,
    });

    // 2. Store in PostgreSQL with user context
    const projectRecord = await this.userDatabase.createProject({
      id: mcpProject.id,
      user_id: this.userId,
      name: params.name,
      description: params.description,
      project_type: params.type,
      tech_stack: params.techStack || [],
      mcp_project_id: mcpProject.id,
      status: "draft",
    });

    // 3. Apply intelligent template
    await this.applyProjectTemplate(session, mcpProject.id, params.type);

    return projectRecord;
  }

  // Cross-user learning implementation
  async getProjectTypeInsights(
    projectType: string
  ): Promise<ProjectTypeInsights> {
    const globalInsights = await this.userDatabase.getProjectTypeInsights(
      projectType
    );
    const userInsights = await this.userDatabase.getUserProjectTypeInsights(
      this.userId,
      projectType
    );
    return this.combineInsights(globalInsights, userInsights);
  }
}
```

**Local Development Integration:**

```typescript
// Development configuration for Memory Pickle MCP
export const mcpConfig = {
  development: {
    serverUrl: "http://localhost:3008",
    autoReconnect: true,
    sessionPersistence: true,
    debugMode: true,
    userIsolation: true,
  },
  production: {
    serverUrl: process.env.MCP_SERVER_URL,
    autoReconnect: true,
    sessionPersistence: true,
    userIsolation: true,
    debugMode: false,
  },
};
```

- **Database:** postgresql://localhost:5432

### Code Organization

**Monorepo Structure:**

```
no-code-ai-platform/
├── apps/
│   ├── web/                 # Next.js frontend
│   ├── api-gateway/         # API gateway service
│   └── agents/              # Agent microservices
│       ├── pm-agent/
│       ├── architect-agent/
│       ├── developer-agent/
│       ├── qa-agent/
│       └── ux-agent/
├── packages/
│   ├── shared/              # Shared utilities and types
│   ├── database/            # Database schemas and migrations
│   └── templates/           # BMAD templates and workflows
├── infrastructure/
│   ├── terraform/           # Infrastructure as code
│   ├── kubernetes/          # K8s manifests
│   └── docker/              # Docker configurations
└── docs/                    # Architecture and API documentation
```

### Quality Assurance

**Code Quality Gates:**

- **TypeScript:** Strict mode with comprehensive type checking
- **ESLint:** Airbnb configuration with custom rules
- **Prettier:** Consistent code formatting
- **Husky:** Pre-commit hooks for quality enforcement

**Testing Strategy:**

- **Unit Tests:** Vitest for individual function testing
- **Integration Tests:** Supertest for API endpoint testing
- **E2E Tests:** Playwright for complete user journey testing
- **Load Tests:** K6 for performance and scalability testing

---

## Risk Assessment & Mitigation

### Technical Risks

**Risk: LLM Provider Outages**

- **Probability:** Medium
- **Impact:** High
- **Mitigation:** Multi-provider fallback strategy, request queuing, user notifications

**Risk: Scaling Challenges**

- **Probability:** Medium
- **Impact:** Medium
- **Mitigation:** Horizontal scaling architecture, performance monitoring, capacity planning

**Risk: Security Vulnerabilities**

- **Probability:** Low
- **Impact:** High
- **Mitigation:** Security audits, penetration testing, automated vulnerability scanning

### Business Risks

**Risk: Competitive Response**

- **Probability:** High
- **Impact:** Medium
- **Mitigation:** Focus on BMAD methodology differentiation, rapid feature development

**Risk: User Adoption Challenges**

- **Probability:** Medium
- **Impact:** High
- **Mitigation:** Extensive user testing, onboarding optimization, customer success programs

### Operational Risks

**Risk: Cost Overruns**

- **Probability:** Medium
- **Impact:** Medium
- **Mitigation:** Cost monitoring, resource optimization, usage-based pricing

**Risk: Talent Acquisition**

- **Probability:** Medium
- **Impact:** Medium
- **Mitigation:** Competitive compensation, remote-first culture, comprehensive documentation

---

## Memory Pickle MCP Implementation Examples

### Multi-Project User Journey Example

**Scenario: User "Sarah" building multiple projects**

```typescript
// User starts first project (E-commerce)
const ecommerceProject = await memoryPickle.create_project({
  name: "Sarah's Fashion Boutique",
  description: "Luxury fashion e-commerce with subscription boxes",
  project_type: "ecommerce",
});

// Template system auto-populates based on project type
await memoryPickle.remember_this({
  content:
    "E-commerce template applied: Product catalog, Shopping cart, Payment processing, User accounts",
  importance: "high",
  project_id: ecommerceProject.id,
});

// User works through BMAD phases...
// Phase handoffs are automatically generated
const handoff = await memoryPickle.generate_handoff_summary({
  project_id: ecommerceProject.id,
  format: "detailed",
});

// User starts second project (SaaS) - learning from first project
const saasProject = await memoryPickle.create_project({
  name: "Inventory Management SaaS",
  description: "B2B inventory tracking for small businesses",
  project_type: "saas",
});

// System applies user learnings from previous project
const userInsights = await memoryPickle.getUserInsights();
// Returns: "User prefers React, likes minimalist design, focuses on mobile-first"

// Cross-project context helps with better recommendations
const techStackInsights = await memoryPickle.getTechStackInsights([
  "react",
  "nodejs",
]);
// Returns: "Based on previous projects, user successfully used Next.js + PostgreSQL"
```

### Agent Workflow with Memory Pickle Integration

**PM Agent Enhanced Workflow:**

```typescript
class EnhancedPMAgent extends PMAgent {
  async createPRD(userInput: string, projectId: string) {
    // 1. Recall all project context
    const projectContext = await this.memoryPickle.recall_state({
      project_id: projectId,
    });

    // 2. Get user's historical preferences
    const userInsights = await this.memoryPickle.getUserInsights();

    // 3. Get project type best practices
    const projectType = projectContext.current_project?.type || "custom";
    const typeInsights = await this.memoryPickle.getProjectTypeInsights(
      projectType
    );

    // 4. Generate PRD with full context
    const prd = await this.generatePRDWithContext({
      userInput,
      projectContext,
      userInsights,
      typeInsights,
    });

    // 5. Remember key PRD decisions
    await this.memoryPickle.remember_this({
      content: `PRD created with ${prd.features.length} features. Key focus: ${prd.primaryGoal}`,
      importance: "critical",
      project_id: projectId,
    });

    // 6. Create tasks for next phase
    for (const feature of prd.features) {
      await this.memoryPickle.create_task({
        title: `Design ${feature.name}`,
        description: feature.description,
        priority: feature.priority,
        project_id: projectId,
      });
    }

    // 7. Generate handoff for Architect
    const handoff = await this.memoryPickle.generate_handoff_summary({
      project_id: projectId,
      format: "detailed",
    });

    return { prd, handoff };
  }
}
```

### Integration Benefits Summary

**Immediate Value (Week 1):**

- ✅ **Zero Context Loss**: Agents maintain perfect memory across sessions
- ✅ **Professional Handoffs**: Automated phase transitions with comprehensive summaries
- ✅ **Multi-Project Support**: Users can manage multiple projects seamlessly
- ✅ **Session Recovery**: Resume complex projects after interruptions

**Enhanced User Experience (Month 1):**

- ✅ **Intelligent Templates**: Smart project initialization based on type and history
- ✅ **Cross-Project Learning**: Recommendations improve with each project
- ✅ **Progress Visibility**: Clear tracking of workflow progression
- ✅ **Professional Documentation**: Investor-ready project summaries

**Competitive Advantages (Month 3+):**

- ✅ **Superior Workflow Management**: Best-in-class project lifecycle management
- ✅ **Learning Platform**: Gets smarter with every user interaction
- ✅ **Enterprise Readiness**: Professional project management capabilities
- ✅ **User Retention**: Reduced abandonment due to context preservation

---

## Future Considerations

### Phase 2 Enhancements

**Advanced Features:**

- **Multi-user Collaboration:** Real-time collaborative editing and project sharing
- **Advanced Analytics:** Comprehensive project success metrics and optimization recommendations
- **Enterprise Features:** SSO integration, advanced security controls, audit logging
- **Memory Pickle Extensions:** Custom tool development for VibeKit-specific workflows

**Technical Improvements:**

- **Performance Optimization:** Advanced caching strategies, database optimization
- **Scalability Enhancements:** Global deployment, edge computing integration
- **AI Improvements:** Fine-tuned models, advanced reasoning capabilities

### Memory Pickle MCP Roadmap Integration

**Phase 2 Memory Pickle Enhancements:**

- **Team Collaboration:** Multi-user project access with role-based permissions
- **Advanced Learning:** Machine learning-powered recommendation engine
- **Integration Ecosystem:** Third-party tool integrations (Figma, Slack, etc.)
- **Enterprise Features:** Advanced audit logging and compliance reporting

### Long-term Vision

**Platform Evolution:**

- **Industry Specialization:** Vertical-specific templates and workflows
- **Ecosystem Integration:** Third-party plugin architecture
- **Advanced AI:** Autonomous project management and optimization

**Technology Roadmap:**

- **Edge Computing:** Reduced latency through edge deployment
- **Advanced Security:** Zero-trust architecture, advanced threat detection
- **Global Scale:** Multi-region deployment with data residency compliance

---

## Conclusion

**V0-CLONE FOUNDATION DECISION:** After comprehensive evaluation, we have selected the V0-Clone template as our foundation. This decision provides:

**Immediate Benefits:**

- **80% infrastructure complete** - Authentication, real-time, AI integration ready
- **Production-proven stack** - Next.js 15, Convex, Inngest, VibeKit
- **6-8 week timeline** vs 16-20 weeks from scratch
- **Modern UI components** - Complete shadcn/ui system
- **Extensible architecture** - Perfect for BMAD methodology overlay

**Implementation Confidence:**

- ✅ **Technical feasibility confirmed** through V0-Clone analysis
- ✅ **Architecture alignment verified** with BMAD requirements
- ✅ **Development timeline realistic** based on extension approach
- ✅ **Risk mitigation achieved** through proven foundation

**Key Architectural Strengths:**

- **Scalable:** Designed for 100,000+ users from day one
- **Secure:** Comprehensive security controls and compliance
- **Maintainable:** Clear separation of concerns and comprehensive documentation
- **User-Focused:** Optimized for non-technical user success

**Next Steps:**

1. **Infrastructure Setup:** Provision AWS resources and Kubernetes clusters
2. **Core Service Development:** Implement API gateway and orchestrator services
3. **Agent Service Implementation:** Develop individual BMAD agent services
4. **Frontend Development:** Build user interface and agent interaction flows
5. **Integration Testing:** Comprehensive testing of agent workflows and handoffs

This architecture serves as the definitive blueprint for development teams, ensuring consistent implementation of the platform vision while maintaining flexibility for future enhancements and optimizations.

---

_This architecture document represents a comprehensive technical blueprint for the No-Code AI Platform, designed to deliver on all PRD requirements while maintaining production-ready quality and scalability._
