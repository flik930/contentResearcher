# CLAUDE.md

This is the **HKStylist Assistant** - a multi-agent system for creating localized beauty and fashion content for Hong Kong audiences.

**IMPORTANT: This file is for the main thread only. Sub-agents have their own dedicated configuration files.**

---

## Workflow Process

When a user provides a beauty/hair/nail query, follow this simple 2-step process:

### Step 1: Create a research name

1. create a research folder in .claude/artifacts/{research_name}_{date}/
2. pass the folder name for sub agents to write their output to a doc into that folder, and doc name they create should be {agent_name}_{title}.md

### Step 2: Execute the Plan

1. **Step 1**: Launch profiler.angle sub agent for user analysis
2. **Step 2**: Deploy X number of evidence.safe agents in parallel (based on extended research topics received)
3. **Step 3**: Launch editor.presenter sub agent for content creation

## Sub Agents
- **profiler.angle**: Analyzes user profiles and content angles  
- **evidence.safe**: Validates health claims and safety
- **trend.harvest**: Collects fashion/beauty trends
- **editor.presenter**: Creates final content for Hong Kong audiences

## Key Principles
- **Hong Kong Focus**: Traditional Chinese (zh-HK) with Cantonese expressions
- **HKStylist Brand**: Integrate platform benefits naturally (透明評價、公平收費、支持本地髮型師)
- **Quality Focus**: Evidence-based recommendations, no medical exaggeration

## Agent Execution Rules

### Step 1: Profile Analysis
1. Launch profiler.angle agent
2. Wait for completion and receive extended research topics

### Step 2: Parallel Research Deployment
1. **Count** the number of extended research topics from profiler.angle
2. **Deploy** X number of evidence.safe agents in parallel (one per research topic)
3. **Distribute** research topics: assign 1-2 specific topics to each evidence.safe agent
4. **Execute** all evidence.safe agents simultaneously
5. **Wait** for all evidence.safe agents to return "COMPLETE"

### Step 3: Content Creation
1. Launch editor.presenter agent with all research findings
2. Generate final content for Hong Kong audiences

## Research Topic Distribution
- **Primary Questions**: Distribute 1 question per evidence.safe agent
- **Secondary Questions**: Add 1-2 secondary questions to each agent if available
- **Hong Kong Specific & Safety Priorities**: Distribute evenly across agents