# Graph Report - workflows  (2026-10-14)

## Corpus Check
- Corpus is ~7,640 words - fits in a single context window. You may not need a graph.

## Summary
- 99 nodes · 188 edges · 12 communities (10 shown, 1 thin omitted)
- Extraction: 93% EXTRACTED · 5% INFERRED · 2% AMBIGUOUS · INFERRED: 10 edges (avg confidence: 0.83)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- Go CI composite actions
- Node CI composite actions
- Python CI composite actions
- Semver and release pipeline
- SonarCloud and coverage
- GitOps homelab deploy
- Betterleaks secret scan
- GHCR image build and login
- Host ops and cron triggers
- Manual version CD
- Actionlint linting

## God Nodes (most connected - your core abstractions)
1. `ci/steps/sonar-scan composite action (SonarCloud)` - 10 edges
2. `ci-go.yml (reusable Go CI)` - 9 edges
3. `Go CI: ci-ok gate job` - 9 edges
4. `Node setup composite action` - 9 edges
5. `Python setup composite action` - 9 edges
6. `semver CD: build job (push image + git tag)` - 8 edges
7. `ci/steps/secret-scan composite action (Betterleaks)` - 8 edges
8. `Bump homelab values.yaml composite action` - 7 edges
9. `Go setup composite action` - 7 edges
10. `manual CD: build job` - 7 edges

## Surprising Connections (you probably didn't know these)
- `github-runner ops: build and push image job` --semantically_similar_to--> `GHCR login composite action`  [INFERRED] [semantically similar]
  .github/workflows/ops-github-runner-build-and-deploy.yml → cd/steps/ghcr-login/action.yml
- `Bump homelab values.yaml composite action` --semantically_similar_to--> `github-runner ops: update homelab job (environment production)`  [INFERRED] [semantically similar]
  cd/steps/homelab-deploy/action.yml → .github/workflows/ops-github-runner-build-and-deploy.yml
- `coverage.out (Go coverage profile)` --shares_data_with--> `ci/steps/sonar-scan composite action (SonarCloud)`  [AMBIGUOUS]
  ci/go/steps/test/action.yml → README.md
- `coverage XML report` --shares_data_with--> `ci/steps/sonar-scan composite action (SonarCloud)`  [AMBIGUOUS]
  ci/python/steps/test/action.yml → README.md
- `README.md (workflows repo overview)` --references--> `semver CD: version job`  [AMBIGUOUS]
  README.md → .github/workflows/cd-build-deploy-semver.yml

## Import Cycles
- None detected.

## Hyperedges (group relationships)
- **Semver CD pipeline (version -> build -> deploy)** — github_workflows_cd_build_deploy_semver_job_version, github_workflows_cd_build_deploy_semver_job_build, github_workflows_cd_build_deploy_semver_job_deploy, github_workflows_cd_build_deploy_semver_job_deploy_no_environment [EXTRACTED 1.00]
- **GitOps bump: homelab values.yaml -> ArgoCD sync** — cd_steps_homelab_deploy_action_file, homelab_values_yaml, argocd_service, github_workflows_ops_github_runner_build_and_deploy_job_deploy [INFERRED 0.75]
- **ci-ok aggregate gate pattern (Go, Node, Python)** — github_workflows_ci_go_job_ci_ok, github_workflows_ci_node_job_ci_ok, github_workflows_ci_python_job_ci_ok [INFERRED 0.85]
- **Go CI pipeline steps** — ci_go_steps_tidy_check_action_file, ci_go_steps_vet_action_file, ci_go_steps_vulncheck_action_file, ci_go_steps_test_action_file, ci_go_steps_tidy_check_action_go_toolchain [INFERRED 0.75]
- **SONAR_TOKEN flow from Infisical to SonarCloud Quality Gate** — ci_steps_sonar_scan_action_file, ci_steps_sonar_scan_action_infisical, ci_steps_sonar_scan_action_sonar_token, ci_steps_sonar_scan_action_sonarcloud, ci_steps_sonar_scan_action_quality_gate [EXTRACTED 1.00]
- **Coverage reports produced by test steps for SonarCloud** — ci_go_steps_test_action_file, ci_python_steps_test_action_file, ci_go_steps_test_action_coverage_file, ci_python_steps_test_action_coverage_xml, ci_steps_sonar_scan_action_file [INFERRED 0.65]

## Communities (12 total, 1 thin omitted)

### Community 0 - "Go CI composite actions"
Cohesion: 0.19
Nodes (20): Go build composite action, Go lint composite action, Go setup composite action, Go test composite action, Go tidy-check composite action, git CLI, Go toolchain, Go vet composite action (+12 more)

### Community 1 - "Node CI composite actions"
Cohesion: 0.33
Nodes (13): Node build composite action, Node check composite action, Node lint composite action, Bun runtime (oven-sh/setup-bun v2.2.0), Node setup composite action, Node test composite action, ci-node.yml (reusable Node CI), Node CI: build verification job (+5 more)

### Community 2 - "Python CI composite actions"
Cohesion: 0.29
Nodes (13): Python ruff composite action, ruff, Python setup composite action, Python 3.14 toolchain (python-version input), uv (astral-sh/setup-uv v9.0.0, uvx), Python test composite action, pytest with pytest-cov, ci-python.yml (reusable Python CI) (+5 more)

### Community 3 - "Semver and release pipeline"
Cohesion: 0.40
Nodes (10): cd-build-deploy-semver.yml (reusable workflow), semver CD: build job (push image + git tag), semver CD: deploy job (environment production), semver CD: deploy-no-environment job, semver CD: version job, release.yml (repo release tagging), Release: tag vX.Y.Z and move floating vN tag, README.md (workflows repo overview) (+2 more)

### Community 4 - "SonarCloud and coverage"
Cohesion: 0.31
Nodes (9): coverage.out (Go coverage profile), coverage XML report, ci/steps/sonar-scan composite action (SonarCloud), Infisical secrets (OIDC via secrets-action), SonarCloud Quality Gate, SONAR_TOKEN, SonarCloud, SONAR_TOKEN (fetched from Infisical) (+1 more)

### Community 5 - "GitOps homelab deploy"
Cohesion: 0.48
Nodes (7): ArgoCD (syncs homelab repo), Bump homelab values.yaml composite action, GitHub environment: production, manual CD: deploy job (environment production), github-runner ops: update homelab job (environment production), devidence-dev/homelab values.yaml (GitOps source), HOMELAB_DEPLOY_TOKEN (push access to homelab)

### Community 6 - "Betterleaks secret scan"
Cohesion: 0.38
Nodes (7): Betterleaks (secret scanner over full git history), Betterleaks image (v1.9.0, digest pinned), ci/steps/secret-scan composite action (Betterleaks), GHCR (ghcr.io registry), Renovate (dependency bot), actionlint repo: Betterleaks secrets job, Go CI: Betterleaks secrets job

### Community 7 - "GHCR image build and login"
Cohesion: 0.47
Nodes (6): GHCR login composite action, GHCR (ghcr.io/devidence-dev/*), github-runner ops: build and push image job, Infisical/secrets-action (pinned v1.0.16), Infisical (secrets manager, GitHub OIDC auth), GHCR_TOKEN (fetched from Infisical)

### Community 8 - "Host ops and cron triggers"
Cohesion: 0.40
Nodes (5): automation-hub (cron scheduler sending workflow_dispatch), Self-hosted github-runner box (runs-on: self-hosted), github-runner ops: Docker and containerd prune job, TELEGRAM_BOT_TOKEN and TELEGRAM_CHAT_ID, Telegram Bot API (notifications and /run_cleanup trigger)

### Community 9 - "Manual version CD"
Cohesion: 0.83
Nodes (4): GitHub OIDC id-token (id-token: write), cd-build-deploy-manual-version.yml (reusable workflow), manual CD: build job, manual CD: deploy-no-environment job

## Ambiguous Edges - Review These
- `ci-actionlint.yml` → `ops-github-runner-build-and-deploy.yml`  [AMBIGUOUS]
  .github/workflows/ops-github-runner-build-and-deploy.yml · relation: depends_on
- `README.md (workflows repo overview)` → `semver CD: version job`  [AMBIGUOUS]
  README.md · relation: references
- `ci/steps/sonar-scan composite action (SonarCloud)` → `coverage.out (Go coverage profile)`  [AMBIGUOUS]
  ci/steps/sonar-scan/action.yml · relation: shares_data_with
- `ci/steps/sonar-scan composite action (SonarCloud)` → `coverage XML report`  [AMBIGUOUS]
  ci/steps/sonar-scan/action.yml · relation: shares_data_with

## Knowledge Gaps
- **17 isolated node(s):** `actionlint job`, `Go build composite action`, `Node build composite action`, `Infisical (secrets manager, GitHub OIDC auth)`, `ArgoCD (syncs homelab repo)` (+12 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 18 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **What is the exact relationship between `ci-actionlint.yml` and `ops-github-runner-build-and-deploy.yml`?**
  _Edge tagged AMBIGUOUS (relation: depends_on) - confidence is low._
- **What is the exact relationship between `README.md (workflows repo overview)` and `semver CD: version job`?**
  _Edge tagged AMBIGUOUS (relation: references) - confidence is low._
- **What is the exact relationship between `ci/steps/sonar-scan composite action (SonarCloud)` and `coverage.out (Go coverage profile)`?**
  _Edge tagged AMBIGUOUS (relation: shares_data_with) - confidence is low._
- **What is the exact relationship between `ci/steps/sonar-scan composite action (SonarCloud)` and `coverage XML report`?**
  _Edge tagged AMBIGUOUS (relation: shares_data_with) - confidence is low._
- **Why does `Python setup composite action` connect `Python CI composite actions` to `Go CI composite actions`, `Node CI composite actions`?**
  _High betweenness centrality (0.140) - this node is a cross-community bridge._
- **Why does `Node setup composite action` connect `Node CI composite actions` to `Python CI composite actions`?**
  _High betweenness centrality (0.088) - this node is a cross-community bridge._
- **Why does `ci/steps/secret-scan composite action (Betterleaks)` connect `Betterleaks secret scan` to `Go CI composite actions`, `Node CI composite actions`, `Python CI composite actions`?**
  _High betweenness centrality (0.086) - this node is a cross-community bridge._