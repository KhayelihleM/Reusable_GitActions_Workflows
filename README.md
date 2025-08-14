# Reusable Autotagging Workflows

**Author:** Khayelihle Manyathi  
**Purpose:** Automate semantic version tagging and release notes generation for multiple repositories using GitHub Actions.  

This repository contains **two workflows**:  

1. **Autotagging Workflow** – reusable workflow that automatically tags and generates friendly release notes.  
2. **Caller Workflow** – example workflow demonstrating how to call the autotagging workflow from another repository.  

---

## 🔹 Autotagging Workflow

A reusable GitHub Actions workflow that:

- Reads commit messages using [Conventional Commits](https://www.conventionalcommits.org/).  
- Determines the next semantic version (`major.minor.patch`).  
- Generates **human-friendly release notes** (no raw filenames).  
- Creates a GitHub release with the new tag.  


### **How It Works**

1. **Trigger:** `workflow_call` (can be called from other workflows).  
2. **Analyze Commits:**  
   - `feat:` → minor  
   - `fix:` → patch  
   - `BREAKING CHANGE:` → major  
3. **Generate Tag:** Semantic version tag (e.g., `v1.2.0`).  
4. **Generate Release Notes:** Replace filenames with friendly terms (Application, Blog, CI pipeline, etc.).  
5. **Publish Release:** Push the tag and release to GitHub automatically.  

---

## 🔹 Caller Workflow Example

This workflow demonstrates calling the **Autotagging Workflow** from another repository.  

```yaml
name: Call Autotagging

on:
  push:
    branches:
      - main

jobs:
  release:
    uses: KhayelihleM/reusable-autotagging-workflows/.github/workflows/autotagging.yml@main
    with:
      repo-token: ${{ secrets.GITHUB_TOKEN }}
      release-branch: main

```

## **How it Works:**

  - uses: points to the reusable workflow URL and branch.

  - with: allows passing parameters (like token, branch, etc.).

   - Executes the autotagging process in the target repository without       duplicating logic.

## ✅ **Benefits**
**Consistency**: All repos follow the same tagging rules.

**Reusability**: Update the workflow once, use everywhere.

**Automation**: No manual version bumps.

Professional Releases: Clear, readable release notes for all stakeholders.

### 📦 **Setup**
Copy the **caller workflow** into your repo under **.github/workflows/.**

**NB:** Ensure your repo uses **Conventional Commits.**

Push to main (or configured branch) to trigger autotagging.

Check the Releases page for the new tag and notes.
Download the commitlint config file and place it in your project dir
