# Agent Guidelines for opencode-multi-model-setup Repository

## Overview
This repository contains configuration files and documentation for setting up a multi-model environment with opencode. Agents working in this repository should focus on maintaining and improving configuration files, documentation, and deployment manifests.

## Repository Structure
- `docs/` - Installation and setup guides for various models and platforms
- `k8s/` - Kubernetes deployment manifests for Ollama
- `configs/` - Configuration files for opencode and shell environment
- Miscellaneous - LICENSE, README.md

## Build/Lint/Test Commands

Since this is primarily a configuration repository, traditional build/test commands don't apply. However, agents should follow these validation practices:

### Documentation Validation
- Check markdown files for broken links: `markdown-link-check docs/`
- Validate YAML syntax: `yamllint k8s/ configs/`
- Validate JSON syntax: `jq . configs/opencode-config.json > /dev/null && echo "Valid JSON"`

### Kubernetes Manifest Validation
- Validate Kubernetes manifests: `kubeval k8s/*.yaml`
- Check for security issues: `kube-score score k8s/*.yaml`

### Configuration Validation
- Validate opencode config: Ensure JSON is properly formatted
- Validate shell scripts: `shellcheck configs/.zshrc-exports.sh`

### Running Specific Validations
To validate a single file:
- Markdown link check: `markdown-link-check docs/01-installation.md`
- YAML lint: `yamllint k8s/ollama-deployment.yaml`
- JSON validation: `jq empty configs/opencode-config.json && echo "Valid"`
- Shell script check: `shellcheck configs/.zshrc-exports.sh`

## Code Style Guidelines

### Documentation (Markdown)
- Use consistent heading levels (starting with H1 for document title)
- Keep line length under 100 characters for readability
- Use fenced code blocks with language specifiers:
  ```yaml
  apiVersion: v1
  kind: Service
  ```
- Link format: Use descriptive link text `[Kubernetes Deployment Guide](docs/06-kubernetes-deployment.md)`
- Lists: Use consistent indentation (2 spaces) and either dashes or asterisks
- Tables: Align columns properly with headers separated by dashes

### YAML Files (Kubernetes Manifests)
- Indentation: 2 spaces (no tabs)
- Key ordering: Put metadata first, then spec, then status (if applicable)
- String quoting: Quote strings that contain special characters or start with numbers
- Multi-line strings: Use `|` for preserving newlines, `>` for folding newlines
- Resource definitions: Group related resources in separate files when possible
- Labels and annotations: Use meaningful, consistent naming conventions
- Image tags: Prefer specific version tags over `latest` in production manifests

### JSON Files (Configuration)
- Indentation: 2 spaces
- Trailing commas: Never use trailing commas
- String quotes: Use double quotes consistently
- Commenting: JSON doesn't support comments; use separate documentation files
- Structure: Group related settings logically
- Validation: Ensure all JSON is valid before committing

### Shell Scripts
- Shebang: Use `#!/usr/bin/env bash` for portability
- Indentation: 2 spaces (no tabs)
- Quoting: Quote all variable expansions `"$VAR"`
- Error handling: Use `set -euo pipefail` at the top of scripts
- Variable naming: Use lowercase with underscores for variables
- Constants: Use UPPERCASE_WITH_UNDERSCORES for constants
- Functions: Define functions before calling them
- Comments: Explain why, not what

### General Principles
- Files should end with a newline
- Remove trailing whitespace
- Use UTF-8 encoding without BOM
- Keep configurations as simple as possible while being explicit
- Document non-obvious decisions in comments or adjacent documentation
- Version numbers should be specific and tracked

## Error Handling Practices

### In Documentation
- Clearly distinguish between required and optional steps
- Provide troubleshooting sections for common issues
- Include verification steps after procedures
- Use callouts/admonitions for warnings and important notes

### In Configuration Files
- Use sensible defaults where possible
- Validate values fall within acceptable ranges
- Provide clear error messages through documentation
- Separate environment-specific configurations

### In Scripts
- Check for required dependencies early
- Validate input parameters
- Use meaningful exit codes
- Log errors to stderr
- Clean up resources on failure when appropriate

## Commit Message Guidelines
- Use conventional commits format: `type(scope): description`
- Types: feat, fix, docs, style, refactor, test, chore
- Scope: Optional, indicates what part of the repo is affected (docs, k8s, configs)
- Description: Imperative mood, max 50 characters
- Body: Optional, wrap at 72 characters, explain why and what changed
- Footer: Optional, for breaking changes or issue references

## Pull Request Guidelines
- Keep PRs focused on a single topic
- Update documentation when changing configurations
- Include validation steps in PR description
- Reference related issues
- Ensure all files pass validation checks

## File Naming Conventions
- Use lowercase letters and numbers
- Separate words with hyphens (`-`) for markdown and YAML files
- Use underscores (`_`) for shell scripts when appropriate
- Extension should clearly indicate file type (.md, .yaml, .json, .sh)
- Kubernetes resources: Use descriptive names that indicate purpose
- Configuration files: Prefix with application name when relevant (opencode-)

## Updating Documentation
When making changes that affect documentation:
1. Update relevant docs files in the `docs/` directory
2. Ensure examples remain accurate
3. Check that all links still work
4. Verify code samples are valid
5. Update table of contents if needed

## Working with Kubernetes Manifests
- Keep manifests environment-agnostic when possible
- Use labels and annotations consistently
- Document resource requirements
- Consider using namespaces for isolation
- Validate resource limits and requests
- Check API version compatibility

## Security Considerations
- Never commit secrets or credentials
- Use environment variables for sensitive values
- Review base images for vulnerabilities
- Follow principle of least privilege for service accounts
- Regularly update dependencies and base images

## Testing Strategies
While this repository doesn't contain traditional code to test:
- Validate all configuration files are syntactically correct
- Ensure documentation examples are accurate
- Check that referenced files exist and are accessible
- Verify that changes don't break existing functionality
- Test in staging environments when possible before promoting to production