# Cursor Window Activate Hook

Automatically activates the Cursor window and brings it to the foreground after each AI agent response. Saves the active window before submitting a prompt and restores it after receiving a response.


## 🎯 Features

- ✅ Automatic Cursor window activation after agent response
- ✅ Save active window before submitting prompt
- ✅ Restore the same window after response
- ✅ Cross-platform support: macOS, Linux, Windows
- ✅ Works with multiple Cursor windows simultaneously

## 🚀 Quick Installation

Install using the `cursor-hook` CLI tool:

```bash
npx cursor-hook install beautyfree/cursor-window-activate-hook
```

This will:
- Download the repository
- Install system dependencies (if needed)
- Prompt you to choose installation location (global or project)
- Configure hooks automatically

**Install globally:**
```bash
npm install -g cursor-hook
cursor-hook install beautyfree/cursor-window-activate-hook
```

### Linux dependencies installation (automatic)

The CLI automatically attempts to install `xdotool` using the appropriate package manager for your Linux distribution:

- **Debian/Ubuntu**: `apt-get`
- **CentOS/RHEL**: `yum`
- **Fedora**: `dnf`
- **Arch Linux**: `pacman`

If automatic installation fails, install manually:
```bash
sudo apt-get install xdotool  # Debian/Ubuntu
sudo yum install xdotool      # CentOS/RHEL
sudo dnf install xdotool      # Fedora
sudo pacman -S xdotool        # Arch Linux
```

## 📋 Requirements

### macOS
- Cursor installed
- No additional dependencies (uses built-in AppleScript)

### Linux
- Cursor installed
- One of the following tools (installed automatically if needed):
  - `xdotool` (recommended)
  - `wmctrl`

### Windows
- Cursor installed
- Node.js (for cursor-hook CLI)
- PowerShell (built-in on Windows 10+)

## 🔧 How It Works

1. **Before submitting prompt** (`beforeSubmitPrompt`):
   - Script saves the identifier of the current active Cursor window
   - Saves it to `~/.cursor/hooks/activate-window-ids/`

2. **After agent response** (`afterAgentResponse`):
   - Script loads the saved window identifier
   - Activates that specific window and brings it to the foreground
   - Removes the temporary file after use

## 📁 File Structure

After installation, files will be located at:

**Global installation:**
```
~/.cursor/
├── hooks.json                    # Hooks configuration
└── hooks/
    ├── activate-window.sh         # Main script
    └── activate-window-ids/      # Temporary files with window IDs (created automatically)
```

**Project installation:**
```
.cursor/
├── hooks.json                    # Hooks configuration
└── hooks/
    ├── activate-window.sh         # Main script
    └── activate-window-ids/      # Temporary files with window IDs (created automatically)
```

## 🛠️ Manual Setup

If you prefer to set up manually:

1. Download `activate-window.sh` from the repository
2. Copy it to `~/.cursor/hooks/` (or `.cursor/hooks/` for project installation)
3. Make it executable: `chmod +x ~/.cursor/hooks/activate-window.sh`
4. Create or update `~/.cursor/hooks.json` (or `.cursor/hooks.json` for project) with hooks configuration (see `hooks.json.example`)

## 🧪 Testing

Test the script:

```bash
# Test window saving
echo '{
  "conversation_id": "test-123",
  "hook_event_name": "beforeSubmitPrompt",
  "cursor_version": "2.4.20",
  "workspace_roots": ["/path/to/workspace"],
  "user_email": "test@example.com"
}' | ~/.cursor/hooks/activate-window.sh

# Check saved ID
cat ~/.cursor/hooks/activate-window-ids/test-123.txt

# Test window activation
echo '{
  "conversation_id": "test-123",
  "hook_event_name": "afterAgentResponse",
  "cursor_version": "2.4.20",
  "workspace_roots": ["/path/to/workspace"],
  "user_email": "test@example.com"
}' | ~/.cursor/hooks/activate-window.sh
```

## 🔄 Updating

```bash
npx cursor-hook install beautyfree/cursor-window-activate-hook
```

## 🗑️ Uninstallation

**For global installation:**
```bash
# Remove hooks and scripts
rm -rf ~/.cursor/hooks/activate-window.sh
rm -rf ~/.cursor/hooks/activate-window-ids
# Edit ~/.cursor/hooks.json and remove the corresponding entries
```

**For project installation:**
```bash
# Remove hooks and scripts
rm -rf .cursor/hooks/activate-window.sh
rm -rf .cursor/hooks/activate-window-ids
# Edit .cursor/hooks.json and remove the corresponding entries
```

## 📝 License

MIT

## 🤝 Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change.

## 📚 Additional Information

- [Cursor Hooks Documentation](https://cursor.com/docs/agent/hooks)
- [cursor-hook CLI Tool](https://github.com/beautyfree/cursor-hook-cli) - Install hooks from Git repositories
- [Issues and Discussions](https://github.com/beautyfree/cursor-window-activate-hook/issues)
