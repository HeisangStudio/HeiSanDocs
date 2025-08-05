
# AudioDocs Audio Software Documentation Management System

This is an automation tool for managing and maintaining a website dedicated to audio software documentation. Built on VitePress, it integrates web scraping, content management, and server deployment functionalities.

## Project Overview

AudioDocs focuses on resources related to audio software, automating the collection, organization, and publication of content. The project utilizes VitePress as a static site generator and provides a streamlined management tool to simplify the entire workflow.

## Key Features

### 1. Automated Web Scraping of Audio Software Information
- Automatically fetches daily updates of audio software from designated websites
- Smart extraction of titles, images, author information, and descriptions
- Generates formatted Markdown documents automatically

### 2. VitePress Documentation Management
- Automatically updates VitePress configuration, adds new articles to sidebar navigation
- Organizes documents by date, facilitating easy access and management
- Supports Git version control, automatically commits and pushes changes

### 3. Automated Deployment
- One-click builds VitePress static website
- Smart file synchronization, transferring only changed files
- Supports multiple deployment methods: rsync or SCP implemented in Python

## Directory Structure

```
AudioDocs/
├── manage.py           # Main program
├── sync_record.json    # Synchronization record file
├── docs/               # Source document directory
│   ├── AboutDocs.md    # Website documentation
│   ├── DownloadTutorial.md  # Usage tutorial
│   └── YYYY-MM-DD/     # Articles organized by date
│       └── *.md        # Individual software documentation
├── .vitepress/         # VitePress configuration directory
│   ├── config.mts      # Website configuration file
│   └── dist/           # Build output directory (deployment files)
└── node_modules/       # Dependencies
```

## Usage

### Environment Setup

1. Install Python 3.6+
2. Install Node.js and npm
3. Install dependencies:
```bash
pip install selenium beautifulsoup4 paramiko scp requests
npm install
```

### Configuration Details

The tool uses two main configuration objects:

#### SYNC_CONFIG (Server Synchronization Configuration)

```python
SYNC_CONFIG = {
    "host": "Server IP",
    "username": "Username",
    "remote_path": "/www/wwwroot/audio-docs/",
    "port": 22,
    "ssh_key_path": "~/.ssh/id_rsa",
    "password": "Password",
    "build_dir": ".vitepress/dist",
    "exclude": ["*.pyc", "__pycache__", ".git", "node_modules", ".DS_Store", "*.log"],
    "include": [".md", ".html", ".css", ".js", ".json", ".png", ".jpg", ".jpeg", ".gif"]
}
```

#### UPDATE_CONFIG (Local Update Configuration)

```python
UPDATE_CONFIG = {
    "commit_message": "Automatic update",
    "push_to_remote": True,
    "build_command": "npm run docs:build"
}
```

## Workflow

1. **Content Collection**: Spider retrieves daily updates of audio software from AudioZ.
2. **Content Processing**: Converts fetched information into Markdown format and saves it into corresponding date folders.
3. **Configuration Update**: Updates VitePress configuration, adds new articles to sidebar navigation.
4. **Version Control**: Commits changes to Git repository and pushes to remote.
5. **Website Building**: Executes VitePress build command to generate static website files.
6. **Deployment**: Synchronizes built static files to remote server.

## Notes

- Ensure server connection information is correctly configured.
- Web scraping requires Chrome browser and ChromeDriver.
- Synchronization requires SSH key or password authentication.
- Regularly check and back up `sync_record.json`, which records file synchronization status.
