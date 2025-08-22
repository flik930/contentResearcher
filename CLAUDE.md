# CLAUDE.md

This is the **HKStylist Assistant — Evidence & Trend Content Orchestrator** - a multi-agent system for creating localized beauty and fashion content for Hong Kong audiences.

**IMPORTANT: This file is for the main orchestrator only. Sub-agents have their own dedicated configuration files.**

---

## Quick Start - Intelligent Workflow Orchestration

When a user provides a beauty/hair/nail query, use the 2-step intelligent orchestration process:

### Step 1: Get Workflow Plan
Launch the workflow orchestrator to analyze the query and create an optimized execution plan:

```python
workflow_plan = Task(
  subagent_type="workflow.orchestrator",
  description="Analyze query and create execution plan",
  prompt=f"""
  Analyze this user query and create an optimized workflow plan:
  
  User Query: "{user_query}"
  
  Generate a complete execution plan with:
  - Path determination (Evidence/Trend/Hybrid)
  - Research name generation for folder organization
  - Cache coverage assessment  
  - Agent assignments with token budgets and template selection
  - Template variable substitution from agent-prompt-templates.yaml
  - Parallel execution coordination
  - Quality checkpoints
  - Notion upload scheduling
  
  Optimize for efficiency while maintaining quality standards.
  """
)
```

### Step 2: Execute the Workflow Plan
Follow the returned workflow plan step-by-step:

```python
# The orchestrator returns a structured plan like:
workflow_plan = {
  "execution_steps": [
    {
      "step_id": 1,
      "action": "profile_analysis", 
      "agents": ["profiler.angle"],
      "prompt_template": "profiler_comprehensive",
      "template_variables": {"user_query": "...", "cache_coverage": "..."},
      "execution_mode": "sequential"
    },
    {
      "step_id": 2,
      "action": "parallel_research",
      "agents": ["evidence.safe-001", "evidence.safe-002"], 
      "assignments": {...},
      "execution_mode": "parallel"
    },
    {
      "step_id": 6,
      "action": "notion_upload",
      "agents": ["notion.uploader"],
      "execution_mode": "sequential"
    }
    # ... complete 6-step workflow
  ]
}

# Execute each step according to the plan
for step in workflow_plan.execution_steps:
  if step.execution_mode == "parallel":
    # Launch multiple agents simultaneously in one message
    launch_parallel_agents(step.agents, step.assignments)
  else:
    # Launch single agent
    launch_sequential_agent(step.agents[0], step.prompt_template)
```

---

## Architecture Overview

### Core Components
- **workflow.orchestrator**: Intelligent workflow planning and optimization
- **profiler.angle**: User profile analysis and angle planning  
- **evidence.safe**: Evidence validation and safety assessment
- **trend.harvest**: Trend collection and analysis
- **research.synthesizer**: Multi-agent research consolidation
- **strategy.mapper**: Evidence-to-strategy conversion
- **trend.cluster**: Trend clustering and HK adoptability 
- **editor.presenter**: Content creation and platform optimization
- **notion.uploader**: Automatic research archival to Notion databases

### System Principles
- **Intelligent Orchestration**: workflow.orchestrator handles all coordination logic
- **Research-Centric Organization**: Each research creates a dedicated folder structure
- **Cache-First Optimization**: 60-80% token reduction through intelligent caching
- **Star Topology**: All agents communicate through main thread only
- **Hong Kong Localization**: Traditional Chinese with Cantonese expressions
- **Quality Assurance**: GRADE methodology and 95%+ compliance standards
- **Automatic Archival**: All research automatically uploaded to Notion databases

### Research Organization
- **Folder Structure**: Each research creates `.claude/artifacts/{research_name}/`
- **Naming Convention**: `{topic_slug}_{YYYYMMDD}` (e.g., "vitamin-c-sensitive-skin_20250822")
- **Agent Coordination**: All agents write to the same research folder
- **Automatic Upload**: notion.uploader processes entire research folder
- **Database Creation**: New Notion database per research with format "{research_name} - {timestamp}"

---

## File Structure

```
.claude/
├── agents/                    # Individual agent configurations
│   ├── workflow-orchestrator.md    # Intelligent workflow planner
│   ├── profiler-angle-planner-hk.md
│   ├── evidence-safety-validator.md (legacy)
│   ├── evidence-safe-optimized.md   # Token-optimized version
│   └── [...other agents]
├── templates/                 # Workflow and prompt templates  
│   └── agent-prompt-templates.yaml # Optimized agent prompts
├── knowledge-cache/           # Performance optimization system
│   ├── index.json            # Master cache index
│   ├── articles/             # Cached research articles
│   └── templates/            # Compact output templates
└── artifacts/                # Generated content by research
    ├── workflow.orchestrator/    # Execution plans
    ├── main/                     # Run summaries  
    ├── {research_name_1}/        # Research-specific folder
    │   ├── profiler.angle_{doc}.md
    │   ├── evidence.safe_{doc}.md
    │   ├── strategy.mapper_{doc}.md
    │   ├── editor.presenter_{doc}.md
    │   └── notion.uploader_{timestamp}.md
    └── {research_name_2}/        # Another research project
        └── [...research artifacts]
```

---

## Advanced Features

### Workflow Optimization
- **Adaptive Planning**: Orchestrator adjusts based on cache coverage and complexity
- **Resource Optimization**: Dynamic token budgets based on research requirements
- **Quality-Cost Balance**: Multiple execution patterns (speed/standard/quality)
- **Error Recovery**: Fallback plans for agent failures or quality issues

### Performance Monitoring
The main thread tracks:
- Cache hit rates and token reduction achieved
- Research deduplication effectiveness (target 80%+ overlap elimination)  
- Quality maintenance despite optimization (target 95%+ GRADE compliance)
- Workflow execution time and cost optimization

### Notion Database Integration (Automatic Archival)
Results stored locally and automatically uploaded to dedicated Notion databases:
- **Primary Storage**: Local `.claude/artifacts/{research_name}/` (100% reliability)
- **Automatic Archive**: notion.uploader creates new database per research
- **Research Organization**: Each research gets dedicated Notion database with full schema
- **Evidence Library**: Scientific evidence archive with citation counts and quality scores
- **Content Variants**: 3-tier content output (social/article/guide) with metadata
- **Search & Discovery**: Full-text searchable content with agent/phase filtering

**Database Schema**: 12 standardized properties including Agent Type, Content Type, Research Phase, HK Relevance, Citation Count, Quality Score
**Database Naming**: "{research_name} - {timestamp}"
**Integration Method**: `mcp__notion__notion-create-database` and `mcp__notion__notion-create-pages`
**File Processing**: Automatic metadata extraction from YAML frontmatter and content analysis
**Error Handling**: Continue workflow if Notion upload fails, comprehensive retry logic

---

## Error Handling

### Orchestrator Failures
If workflow.orchestrator fails or returns invalid plan:
1. Fall back to simple pattern matching (legacy logic in CLAUDE.md.backup)
2. Use standard evidence/trend paths based on keyword detection
3. Apply default resource allocation

### Agent Execution Issues  
- **Agent Timeouts**: Retry up to 2 times, then proceed with available results
- **Quality Gate Failures**: Trigger supplementary research or adjust scope
- **Resource Overruns**: Implement scope reduction per orchestrator fallback plan

---

## Legacy Reference

### Manual Path Detection (Fallback Only)
If orchestrator is unavailable, use basic keyword detection:

**Evidence Path**: Queries about 效果/成分/敏感/孕期/副作用/療程安全/醫療/皮膚
**Trend Path**: Queries about 趨勢/今季/春夏/秋冬/2025/2026/日本/韓國/街拍/runway

---

## HKStylist Context

HKStylist is a Hong Kong stylist marketplace focused on individual stylists. Target audience: HK women aged 20–35. All content should include soft CTAs inviting users to discover relevant stylists on HKStylist.

**Language Requirement**: ALL outputs in Traditional Chinese (zh-HK) with authentic Hong Kong Cantonese expressions. Professional, friendly, accessible. Avoid mainland internet slang.

---

**Success Metrics**:
- 70%+ token cost reduction vs legacy system
- 95%+ GRADE evidence compliance  
- 80%+ research overlap elimination
- <20 minute execution time for standard queries
- 100% artifact completion rate with proper AFFiNE integration