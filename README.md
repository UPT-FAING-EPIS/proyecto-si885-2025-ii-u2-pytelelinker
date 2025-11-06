<<<<<<< HEAD
# Telelinker

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](CONTRIBUTING.md)

**Telelinker** is a command-line tool that extracts and analyzes links shared in Telegram groups. It automatically detects content type (Instagram, LinkedIn, YouTube, TikTok, etc.), retrieves relevant metadata, and exports all information in different formats for further analysis.

## 👥 Integrantes del Equipo

* **César Nikolas Camac Meléndez**
* **Jefferson Rosas Chambilla**

## 🚀 What does Telelinker do?

Telelinker allows you to:

- **📱 Extract links** from Telegram groups automatically
- **🔍 Detect platforms** automatically (Instagram, LinkedIn, YouTube, TikTok, Medium, Dev.to)
- **📊 Get metadata** like titles, descriptions, dates, interaction counters
- **💾 Export data** in multiple formats (CSV, PostgreSQL)
- **⚡ Process multiple groups** efficiently

### Typical use cases:

- **Content analysis**: Study what type of links are shared most in communities
- **Social research**: Analyze trends and sharing patterns
- **Community management**: Monitor content shared in groups
- **Data mining**: Collect data for social media analysis

## 📦 Installation

### Option 1: Scoop (Windows - Recommended)

```powershell
# Add the bucket
scoop bucket add telelinker https://github.com/nkmelndz/telelinker

# Install
scoop install telelinker

# Update
scoop update telelinker
```

### Option 2: From source code

**⚠️ System requirements:**
```bash
# Windows (Scoop)
scoop install googlechrome chromedriver

# Linux/macOS
# Chrome/Chromium + ChromeDriver
```

**Installation:**
```bash
git clone https://github.com/nkmelndz/telelinker.git
cd telelinker
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
python -m src.main setup
```

### Option 3: Docker

```bash
# Clone the repository
git clone https://github.com/nkmelndz/telelinker.git

# Navigate to project directory
cd telelinker

# Build the image
docker build -t telelinker .

# Run (Linux/macOS)
docker run --rm -it -u "$(id -u):$(id -g)" -v "$(pwd)":/app telelinker

# Run (Windows PowerShell) - With configuration persistence
docker run --rm -it -v "${PWD}:/app" -v "${HOME}/.telelinker:/root/.telelinker" telelinker

# Run (Windows CMD) - With configuration persistence  
docker run --rm -it -v "%cd%:/app" -v "%USERPROFILE%/.telelinker:/root/.telelinker" telelinker
```

## ⚙️ Initial setup

Before using Telelinker, you need to configure your Telegram API access:

### 1. Get Telegram credentials

1. Go to https://my.telegram.org
2. Log in with your phone number
3. Click on "API development tools"
4. Fill out the form to create an application
5. Save your **API ID** and **API HASH**

### 2. Configure Telelinker

```powershell
# Configure credentials
telelinker setup

# Log in to Telegram
telelinker login
```

## 🎯 How to use Telelinker

### Basic commands

#### 1. List your available groups

**Basic mode:**
```powershell
# View groups in console
telelinker groups

# Export to CSV
telelinker groups --format csv --out my_groups.csv

# Export to JSON
telelinker groups --format json --out my_groups.json
```

**Interactive mode (Recommended):**
```powershell
# Select groups interactively
telelinker groups --interactive

# Interactive mode allows selecting output format and file
telelinker groups --interactive
```

#### 2. Extract links from a specific group

**Basic mode:**
```powershell
# Extract last 50 links
telelinker fetch --group -1001234567890 --limit 50 --format csv --out links.csv

# Use group username
telelinker fetch --group @my_group --limit 100 --format csv --out data.csv
```

**Interactive mode (Recommended):**
```powershell
# Select groups interactively and extract links
telelinker fetch --interactive

# Interactive mode allows configuring all parameters
telelinker fetch --interactive
```

#### 3. Process multiple groups

**From csv file:**
```powershell
# First export groups to CSV
telelinker groups --format csv --out my_groups.csv

# Process all groups from file
telelinker fetch --groups-file my_groups.csv --format postgresql --out data.sql
```

**From JSON file (previously exported):**
```powershell
# First export groups to JSON
telelinker groups --format json --out my_groups.json

# Then use JSON file to process multiple groups
telelinker fetch --groups-file my_groups.json --limit 200 --format csv --out complete_analysis.csv
```

**Interactive mode for multiple groups:**
```powershell
# Select multiple groups interactively
telelinker fetch --interactive
```

### Available parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| `--group` | Group ID or username | `-1001234567890` or `@mygroup` |
| `--groups-file` | File with group list (CSV or JSON) | `groups.csv` or `my_groups.json` |
| `--interactive` | Interactive mode for group selection | `--interactive` |
| `--limit` | Maximum number of links | `100` |
| `--format` | Output format | `csv`, `postgresql` |
| `--out` | Output file | `data.csv` |

### Practical examples

**Quick analysis with interactive mode:**
```powershell
# Select groups interactively and analyze
telelinker fetch --interactive
```

**Export data for database:**
```powershell
# Traditional mode
telelinker fetch --group -1001234567890 --format postgresql --out insert_data.sql

# Interactive mode
telelinker fetch --interactive
```

**Complete workflow:**
```powershell
# 1. List and select groups interactively
telelinker groups --interactive

# 2. Process selected groups
telelinker fetch --groups-file groups_of_interest.json --limit 500 --format csv --out complete_analysis.csv

# 3. Or use direct interactive mode for entire process
telelinker fetch --interactive
```

**Specific use cases:**
```powershell
# Trend research in multiple communities
telelinker fetch --interactive

# Content analysis of specific groups
telelinker fetch --groups-file tech_communities.txt --limit 200 --format csv --out tech_content.csv

# Quick monitoring of recent activity
telelinker fetch --interactive
```

## 🛠️ Supported platforms

Telelinker detects and extracts metadata from:

- **📸 Instagram**: Posts, reels, stories
- **💼 LinkedIn**: Posts, articles
- **🎥 YouTube**: Videos, shorts
- **🎵 TikTok**: Videos
- **📝 Medium**: Articles
- **👨‍💻 Dev.to**: Technical posts

## 📋 System requirements

- **Python 3.11+**
- **Internet connection** (to access APIs)
- **Telegram account** with access to groups you want to analyze
- **Telegram API credentials** (API ID and API HASH)

### Optional dependencies:
- **Docker** (for container execution)
- **PostgreSQL** (if using SQL export format)

## 🤝 Contributing to the project

Telelinker is an open source project and contributions are very welcome!

### How can you help?

- 🐛 **Report bugs** - Find errors and help us improve
- 💡 **Suggest features** - Propose new characteristics
- 🔧 **Add platforms** - Implement support for new social networks
- 📝 **Improve documentation** - Help other users
- ✨ **Optimize code** - Improve performance and quality

### Getting started with contributions

1. **Read the guide**: Check [CONTRIBUTING.md](CONTRIBUTING.md) for detailed instructions
2. **Review code of conduct**: [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)
3. **Explore issues**: Look for [open issues](../../issues) to get started
4. **Fork the repo**: Create your own copy to work on
5. **Submit a PR**: Share your improvements with the community

### Local development

```bash
# Fork and clone the repository
git clone https://github.com/your-username/telelinker.git
cd telelinker

# Set up environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt

# Create a branch for your feature
git checkout -b feature/my-new-feature

# Start coding! 🚀
```

## 📄 License

This project is licensed under the **MIT License**. This means you can:

- ✅ Use the code commercially
- ✅ Modify the code
- ✅ Distribute the code
- ✅ Use the code privately

See [LICENSE](LICENSE) for more details.

## 🆘 Support and help

Need help? Here are several options:

- 📋 **Issues**: [Report bugs or request features](../../issues)
- 💬 **Discussions**: [General questions and help](../../discussions)
- 📖 **Documentation**: [Complete contribution guide](CONTRIBUTING.md)

## ⚠️ Important considerations

- **Privacy**: You can only extract links from groups where you are a member
- **Rate limiting**: Respect Telegram API limits
- **Terms of service**: Make sure to comply with platform ToS
- **Sensitive data**: Never share your API HASH publicly

---

**Like Telelinker?** ⭐ Give the repository a star and share it with other developers!
=======
[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/ykj1qgxA)
[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=21419031)
# proyecto-formatos-012
>>>>>>> 9c2d0319ae8ae1e51c5608f928899bcb4f335246
