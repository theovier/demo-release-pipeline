# Demo Release Pipeline 🚀

A demonstration repository showcasing automated release pipelines using GitHub Actions. This project illustrates how to implement continuous integration and deployment workflows with automated tagging and release processes.

## 📋 Overview

This repository demonstrates a common CI/CD pattern where:
1. **Pre-release branches** automatically create incremental version tags
2. **Tag creation** triggers deployment/release workflows
3. **Automated versioning** removes manual tag management overhead

Perfect for teams looking to implement automated release workflows in their projects.

## 🏗️ Architecture

### Workflow 1: Automated Tag Creation
- **Trigger**: Push to `pre-release` branch
- **Purpose**: Automatically creates incremental tags (v1, v2, v3, etc.)
- **Benefits**: No manual tag management, consistent versioning

### Workflow 2: Tag-Based Release
- **Trigger**: New tag push (v* pattern)
- **Purpose**: Executes release/deployment actions
- **Benefits**: Decoupled release process, consistent deployments

## 🔧 Implementation Details

### Prerequisites
- Repository with GitHub Actions enabled
- Fine-grained Personal Access Token (PAT) with `Contents: Write` permission
- PAT stored as repository secret named `PAT_TOKEN`

### Why PAT Instead of GITHUB_TOKEN?
The default `GITHUB_TOKEN` has a security limitation: workflows it triggers don't activate other workflows. Using a PAT ensures the tag-creation workflow properly triggers the release workflow.

### Required Permissions
For fine-grained PAT:
- **Contents: Write** - Create and push tags
- **Metadata: Read** - Basic repository access
- **Actions: Read** - Use within GitHub Actions

## 🚀 Usage

### Step 1: Setup
1. Create a fine-grained PAT with required permissions
2. Add PAT as repository secret `PAT_TOKEN`
3. Deploy the workflow files (`create-tag.yml` and `on-tag-created.yml`) to `.github/workflows/`

### Step 2: Development Flow
```bash
# Work on your feature
git checkout -b feature/my-feature
git commit -m "Add new feature"

# Ready for pre-release
git checkout pre-release
git merge feature/my-feature
git push origin pre-release  # 🎯 This triggers tag creation
```

### Step 3: Automated Process
1. Push to `pre-release` → Creates tag (e.g., v1, v2, v3)
2. Tag creation → Triggers release workflow
3. Release workflow → Executes deployment logic

## 📁 Workflow Files Structure

```
.github/
└── workflows/
    ├── create-tag.yml       # Tag creation workflow
    └── on-tag-created.yml   # Release workflow
```