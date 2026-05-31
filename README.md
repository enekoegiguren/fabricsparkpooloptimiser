# ⚡ Fabric Spark Pool Optimiser

Analyses real Spark session data across your Fabric workspaces and recommends the optimal Spark pool configuration.

---

### How it works
1. **Auto-discovers** all workspaces you have access to
2. **Detects Workspace Monitoring** — uses real vCores where available
3. **Classifies sessions** — separates automated (pipeline/SPN) from interactive (dev) sessions
4. **Collects Spark sessions** via the Fabric Monitoring API (1 call per workspace)
5. **Analyses** duration, data movement (GB via stages), and parallelism
6. **Recommends** optimal nodeSize + maxNodes with full explanation and config steps
7. **Estimates** monthly CU savings vs current pool
8. **Renders an interactive dashboard** with an About page explaining the methodology

### Requirements
- **Spark Notebook** in Microsoft Fabric · Viewer role on workspaces · No lakehouse needed

### Data sources & known limitations
| Data | Source | Notes |
|------|--------|-------|
| Session duration | Livy Sessions API | Real |
| GB read/written/shuffle | Spark History Stages | Real — not attributable to sub-notebooks |
| Max concurrent sessions | Livy Sessions API | Real |
| vCores really used | Workspace Monitoring KQL | Only if monitoring enabled |
| vCores really used | resourceusage API | ❌ 500 for pipeline-triggered sessions |
| Sub-notebook breakdown | itemsnapshots / jobGroups | ❌ Not available (all jobGroup=None) |
