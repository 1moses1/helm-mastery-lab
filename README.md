# 🧭 Mastering Helm Core Concepts

This repository serves as a comprehensive knowledge base and cheat sheet for mastering Helm—the package manager for Kubernetes. It includes Helm chart structure, release lifecycles, repository management, chart provenance, hooks, and how to host and publish your own Helm charts.

---

## 📦 Helm Chart Anatomy Overview

```plaintext
mychart/
├── Chart.yaml          # Metadata about the chart
├── values.yaml         # Default configuration values
├── charts/             # Chart dependencies (subcharts)
├── templates/          # Kubernetes manifest templates
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── _helpers.tpl
│   ├── NOTES.txt
│   └── tests/
└── README.md           # Usage and documentation
```

---

## 📜 Helm CLI Cheatsheet

### 🔹 Chart Creation & Packaging

```bash
helm create mychart                     # Scaffold a new Helm chart
helm package mychart/                   # Package the chart into a .tgz archive
```

---

### 🔹 Chart Installation

```bash
helm install <release-name> <chart>     # Install a chart as a release
helm install -f custom-values.yaml <release-name> <chart>    # Install with custom values
helm install --set key=value <release-name> <chart>          # Override values inline
helm install --verify <release-name> <repo/chart>            # Verify chart signature before installing
```

---

### 🔹 Chart Upgrade

```bash
helm upgrade <release-name> <chart>     # Upgrade a release to a new chart or values
helm upgrade --install <release-name> <chart>   # Upgrade or install if release doesn't exist
helm upgrade --reset-values <release-name> <chart>  # Use only default values
```

---

### 🔹 Rollback & Uninstall

```bash
helm rollback <release-name> [revision] # Roll back to a previous release version
helm uninstall <release-name>           # Uninstall and delete the release
helm uninstall --keep-history <release-name>  # Keep history after uninstall
```

---

### 🔹 Repository Management

```bash
helm repo add <name> <url>              # Add a new chart repository
helm repo list                          # List added repositories
helm repo update                        # Refresh repo index files
helm repo remove <name>                 # Remove a repository
```

---

### 🔹 Chart Discovery

```bash
helm search hub <keyword>               # Search ArtifactHub for charts
helm search repo <chart-name>           # Search added repos for a chart
```

---

### 🔹 Inspecting Releases

```bash
helm list                               # List installed releases
helm get all <release-name>             # View all release data
helm history <release-name>             # Show revision history
```

---

### 🔹 Template Rendering

```bash
helm template <release-name> <chart>    # Render Kubernetes manifests locally
```

---

### 🔹 Helm Hooks

Add annotations in templates to define hooks:

```yaml
annotations:
  "helm.sh/hook": pre-install
  "helm.sh/hook-delete-policy": hook-succeeded
  "helm.sh/hook-weight": "0"
```

---

### 🔹 Hosting a Local Helm Repository

```bash
helm package mychart/                   # Package chart into .tgz
helm repo index . --url http://localhost:8000  # Create index.yaml with base URL
python3 -m http.server --directory .    # Serve repo with HTTP
helm repo add localrepo http://localhost:8000
```

---

### 🔹 Chart Signing & Provenance

```bash
helm package --sign --key <key-name> --keyring <path> mychart/
helm verify mychart-0.1.0.tgz           # Verify chart against its signature
```

---

## 🗂️ Suggested Use Cases

- Onboarding new team members to Helm
- Creating internal Helm chart repositories
- Preparing Helm charts for ArtifactHub publication
- Securing charts with GPG signatures

---

## 📅 Last Updated

May 13, 2025

---

## 📘 License

This documentation is provided for educational purposes and personal mastery of Helm.
