# Documentation

#### Setup Git and Project Structure
```shell
# Define git variables
GIT_USER_NAME="th3b1rdm2n"
GIT_USER_HOMEPAGE="https://github.com/$GIT_USER_NAME"
GIT_REPO_NAME="$GIT_USER_NAME"
GIT_REPO_URL="https://github.com/$GIT_USER_NAME/$GIT_REPO_NAME.git"
GIT_REPO_DESCRIPTION="The Roost of a Hacker with a Beginner's Mind."
GIT_MAIN_BRANCH="main"
GIT_DEV_BRANCH="dev"
GIT_REMOTE_NAME="origin"

# Define custom variables
PROJECT_ROOT="$HOME/Projects/$GIT_REPO_NAME"

# Authenticate to GitHub and create remote repository
gh auth status # Check authentication status
gh auth login -h github.com -p https -w # Authenticate to GitHub
gh auth setup-git # Configure Git to use GitHub CLI as credential helper
gh repo create "$GIT_REPO_NAME" --public --homepage "$GIT_USER_HOMEPAGE" --description "$GIT_REPO_DESCRIPTION" # Create remote repo

# Initialize local git repository
git init "$PROJECT_ROOT" && cd "$PROJECT_ROOT" # Initialize local Git repo
git config --local user.name "$GIT_USER_NAME" # Set local Git username
git config --local user.email "" # Set local Git email
git branch -M "$GIT_MAIN_BRANCH" # Rename default branch to main
git remote add "$GIT_REMOTE_NAME" "$GIT_REPO_URL" # Add remote origin
git commit --allow-empty -m "chore: initial commit - $(date +%F_%H:%M)" # initial empty commit
git push -u "$GIT_REMOTE_NAME" "$GIT_MAIN_BRANCH" # Push main branch to remote

# Configure pre-commit hooks
cat > "$PROJECT_ROOT/.pre-commit-config.yaml" <<EOF
repos:
- repo: https://github.com/pre-commit/pre-commit-hooks
  rev: v5.0.0
  hooks:
  - id: check-added-large-files
    args: ["--maxkb=102400", "--enforce-all"]
EOF
pre-commit install # Install pre-commit hooks
pre-commit autoupdate # Update hook repos to latest version
pre-commit run --all-files # Run pre-commit hooks on all files

# Create .gitignore file
cat > "$PROJECT_ROOT/.gitignore" <<EOF
# Android
**/*.apk
**/*.ap_
**/*.dex

# AWS
**/*.aws-sam

# Binaries
**/*.dll
**/*.exe
**/*.so

# Burp
**/*.burp

# C
**/*.a
**/*.lib
**/*.o
**/*.obj

# CSharp
**/*.csproj.user
**/*.sln.docstates
**/*.suo
**/*.user
**/*.userosscache

# Elixir
**/_build/
**/*.ez
**/deps/

# Go
**/*.out
**/*.test
**/vendor/

# IDE
**/.code-workspace
**/.idea
**/.vscode/
!**/.vscode/extensions.json
!**/.vscode/settings.json

# iOS
**/*.ipa
**/*.xcarchive

# Java
**/.gradle
**/.intellij/
**/.mtj.tmp/
**/.storm/
**/*.class
**/*.ear
**/*.idea/
**/*.iml
**/*.ipr
**/*.iws
**/*.jar
**/*.kotlin_module
**/*.nar
**/*.war
**/bin/
**/build/
**/kotlin/
**/target/

# JavaScript
**/.angular/
**/.next/
**/.node_repl_history
**/.npm
**/.nuxt/
**/.parcel-cache/
**/.temp
**/.vue-cli-service/
**/*.js.map
**/*.min.js
**/*.ts.map
**/*.tsbuildinfo
**/coverage/
**/dist/
**/e2e/
**/node_modules/
**/npm-debug.log
**/package-lock.json
**/public/
**/yarn-debug.log
**/yarn-error.log

# Linux
**/*.deb
**/*.lock
**/*.rpm
**/*.tar.gz
**/*.tmp
**/*.zip

# MacOs
**/*.dylib

# Miscellaneous
**/*.bak
**/*.log
**/*.swp
**/.env

# Obsidian
**/.obsidian/

# Perl
**/*.cgi
**/*.pl.swp
**/*.pm.swp
**/*.t.swp

# PHP
**/*.phpdbg/
**/*.phpstorm/
**/*.phpunit/
**/*.user.ini
**/app/etc/env.php
**/bootstrap/cache/
**/composer.lock
**/pub/media/
**/pub/static/
**/storage/
**/var/
**/vendor/
**/wp-content/cache/
**/wp-content/upgrade/
**/wp-content/uploads/

# PKI
**/*.crl
**/*.crt
**/*.csr
**/*.jks
**/*.key
**/*.p12
**/*.pem

# Python
**/*.dist-info/
**/*.egg-info/
**/*.pyc
**/*.pyd
**/*.pyo
**/__pycache__/
**/.ipynb_checkpoints/
**/.venv/
**/env/
**/ENV/
**/venv/

# Research
**/.asset_checkpoint
**/.dns_checkpoint
**/.url_checkpoint
**/.url_checkpoint4proxy
**/.url_checkpoint.json
**/*-tracker.txt
**/burp-crawl-*
**/burp-check-*
**/programs/
**/paused_programs/
**/technologies.jsonl

# Ruby
**/_site
**/*.gem
**/.bundle
**/.jekyll-cache
**/.jekyll-metadata
**/*.rbc
**/*.rbenv/
**/*.rvm/
**/.ruby-gemset
**/.ruby-version
**/Gemfile.lock
**/log/
**/tmp/
**/vendor

# Rust
**/Cargo.lock
**/target/

# Scala
**/*.cache
**/*.class
**/*.tasty
**/target/

# SQlite
**/*.db
**/*.sqlite3

# Swift
**/*.swiftpm/
**/*.swiftsourceinfo
**/*.xcodeproj/
**/*.xcworkspace/

# Terraform
**/*.tfstate
**/*.tfstate.backup

# Vagrant
.vagrant/

# WebAssembly
**/*.wasm
**/*.wat

EOF

# Create README and DOCS files
touch "$PROJECT_ROOT/README.md" "$PROJECT_ROOT/DOCS.md" 

# Switch to the dev branch and start working on new features
git checkout -b "$GIT_DEV_BRANCH" # Create and switch to main branch
git add .  # add the modified and populated files
git commit -m "chore: wrote some documentations - $(date +%F_%H:%M)"
git push -u "$GIT_REMOTE_NAME" "$GIT_DEV_BRANCH"

# Merge the changes from 'dev' into 'main' and push the updates
git switch "$GIT_MAIN_BRANCH"
git merge "$GIT_DEV_BRANCH"
git push -u "$GIT_REMOTE_NAME" "$GIT_MAIN_BRANCH" # Push main branch to remote
git switch "$GIT_DEV_BRANCH" # Switch back to development branch
```


