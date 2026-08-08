# Setup & Development Guide — Galaxy Profile

This guide provides step-by-step instructions for setting up and updating your **Galaxy Profile README** generator on any new machine (macOS, Windows, or Linux).

---

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
* **Git** ([Download Git](https://git-scm.com/))
* **Python 3.9 or higher** ([Download Python](https://www.python.org/))

---

## 🚀 1. Clone the Repository

Open your terminal or command prompt and clone your repository:

```bash
git clone https://github.com/labib-ur-rahman/labib-ur-rahman.git
cd labib-ur-rahman
```

---

## 🛠️ 2. Set Up Virtual Environment

To isolate dependencies and avoid conflicts, create and activate a Python Virtual Environment (`.venv`):

### macOS / Linux:
```bash
# Create virtual environment
python3 -m venv .venv

# Activate virtual environment
source .venv/bin/activate

# Install required dependencies
pip install -r requirements.txt
```

### Windows (Command Prompt / PowerShell):
```cmd
:: Create virtual environment
python -m venv .venv

:: Activate virtual environment (Command Prompt)
.venv\Scripts\activate.bat

:: OR Activate virtual environment (PowerShell)
.venv\Scripts\Activate.ps1

:: Install required dependencies
pip install -r requirements.txt
```

---

## ⚙️ 3. Modify Profile Configuration

All profile data (bio, social links, skills, galaxy arms, featured projects, excluded languages) is managed inside `config.yml`.

Open `config.yml` in your editor and update the desired fields:

```yaml
username: labib-ur-rahman

profile:
  name: "Md Labibur Rahman"
  tagline: "Mobile App Developer | Flutter | Dart | Kotlin | Java"
  company: "Flutter Developer @ Softvence | Dhaka, Bangladesh"
  location: "Mohakhali, Dhaka, Bangladesh"
  bio: |
    "Flutter Developer with proven expertise in building 
    production-ready mobile applications..."

# Exclude languages from telemetry chart if needed
languages:
  exclude:
    - "HTML"
    - "CSS"
    - "Shell"
    - "Makefile"
    - "Python"
  max_display: 8
```

---

## 🎨 4. Generate SVGs Locally

After editing `config.yml` or generator code, you can test and generate the SVG assets locally.

Make sure your `.venv` is activated, then run:

### Real GitHub Data Generation:
*(Note: Uses GitHub API to fetch stats and repository language metrics)*
```bash
# Set optional GITHUB_TOKEN to avoid API rate limits
export GITHUB_TOKEN="your_personal_access_token"

python3 -m generator.main
```

### Demo Data Generation (Offline Mode):
*(Does not make any network calls; uses hardcoded demo stats)*
```bash
python3 -m generator.main --demo
```

Generated SVGs will be created in the `./assets/generated/` folder:
* `galaxy-header.svg`
* `stats-card.svg`
* `tech-stack.svg`
* `projects-constellation.svg`

---

## 📤 5. Save & Push Changes to GitHub

Once you are satisfied with the changes:

```bash
# 1. Stage modified files (Do NOT commit .venv)
git add config.yml assets/generated/ README.md

# 2. Commit your changes
git commit -m "feat: update profile config and regenerated assets"

# 3. Push to GitHub
git push origin main
```

---

## 🔄 6. Automatic Updates via GitHub Actions

You don't need to manually run generator scripts every time!

The GitHub Actions workflow defined in `.github/workflows/generate-profile.yml`:
1. **Runs automatically every 12 hours** to keep stats updated.
2. **Runs automatically whenever you push changes** to `config.yml` or `generator/`.
3. **Can be triggered manually** from the GitHub repository **Actions** tab by selecting **Generate Profile SVGs** > **Run workflow**.

---

## 🧹 Maintenance Tip: Cleaning Tracked `.venv` (If ever committed)

If `.venv` was previously tracked in Git history, run the following commands once to un-track it:

```bash
git rm -r --cached .venv
git commit -m "fix: remove tracked .venv from git repository"
git push origin main
```
