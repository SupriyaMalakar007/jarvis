# Jarvis 🎙️

**A private, local AI voice assistant that runs on your computer.**

Jarvis is a voice-controlled AI assistant designed to run locally using **Ollama**, **Whisper**, **Piper TTS**, and Python.

Say **"Jarvis"** naturally in a sentence, and Jarvis can listen, understand your request, process it using a local AI model, and respond with voice.

The project is currently being developed and tested primarily on **Windows**.

---

## ✨ Features

- 🎙️ **Voice activation** — Say "Jarvis" to activate the assistant.
- 🧠 **Local AI** — Uses Ollama for local LLM inference.
- 🗣️ **Speech recognition** — Uses Faster-Whisper for speech-to-text.
- 🔊 **Text-to-speech** — Uses Piper for local voice responses.
- 💾 **Conversation memory** — Stores conversation-related information locally.
- 🛠️ **Tool support** — Designed to work with tools and MCP servers.
- 🌐 **Web search support** — Optional web search functionality.
- 📍 **Location awareness** — Optional GeoLite2-based location detection.
- 📋 **Voice dictation** — Dictate text using a keyboard shortcut.
- 🔒 **Privacy-focused** — Designed around local processing.
- 🪟 **Windows support** — Development and testing currently focus on Windows.

---

# 🧠 AI Models

Jarvis uses [Ollama](https://ollama.com/) as the default local LLM provider.

The recommended model for the current Windows setup is:


llama3.2:3b

Install it with:

ollama pull llama3.2:3b

Check installed models:

ollama list

Test the model:

ollama run llama3.2:3b

Then try:

Say hello
Other Models

The project may also support other Ollama models depending on your hardware and configuration.

For example:

gemma4:e2b

However, model compatibility can depend on the Ollama version, available RAM/VRAM, and the Jarvis configuration.

---

#💻 Requirements
Windows

Recommended:

Windows 10 or Windows 11
Python 3.11
Git
Ollama
Working microphone
Working speakers/headphones
Microsoft Visual C++ Build Tools

For some Python packages, native C++ compilation may be required.

Visual C++ Build Tools

If you encounter:

Microsoft Visual C++ 14.0 or greater is required

install Visual Studio Build Tools and select:

Desktop development with C++

Make sure the installation includes:

MSVC C++ build tools
Windows SDK
C++ build tools

#🚀 Installation
1. Clone the repository
git clone https://github.com/SupriyaMalakar007/Jarvis.git
cd Jarvis
2. Create a virtual environment
python -m venv .venv
3. Activate the virtual environment
.\.venv\Scripts\Activate.ps1

If PowerShell blocks the script:

Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned

Then activate again:

.\.venv\Scripts\Activate.ps1
4. Upgrade pip
python -m pip install --upgrade pip
5. Install dependencies

For Windows:

pip install -r requirements-windows.txt

If the project provides a general requirements file:

pip install -r requirements.txt

#🦙 Ollama Setup

Install Ollama and verify:

ollama --version

Start Ollama if necessary, then verify that the API is available:

python -c "import urllib.request; print(urllib.request.urlopen('http://127.0.0.1:11434/api/tags').status)"

A successful installation should return:

200

Check your models:

ollama list

Example:

NAME          SIZE
llama3.2:3b   2.0 GB
▶️ Running Jarvis

Activate the environment:

.\.venv\Scripts\Activate.ps1

Then start Jarvis using the project's Windows startup script.

For example:

powershell -ExecutionPolicy Bypass -File scripts\run_windows.ps1

Once Jarvis starts, wait for the voice listener to initialize.

Then say:

Jarvis, say hello.
🎙️ Voice Input

Jarvis uses sounddevice to access your microphone.

Check available audio devices:

python -c "import sounddevice as sd; print(sd.query_devices())"

You should see an input device such as:

Microphone Array

If Jarvis cannot hear you:

Open Windows Settings
Go to System → Sound
Open Input
Select your microphone
Make sure the microphone is enabled
Check the Windows microphone permission settings

You can also test the microphone directly through Windows.

#🗣️ Speech Recognition

Jarvis uses Faster-Whisper for speech recognition.

The current configuration uses:

Whisper model: medium
Backend: auto
Compute type: int8

The medium model provides good multilingual recognition but requires more system resources than smaller models.

For lower-resource computers, a smaller Whisper model can be configured.

Example:

{
  "whisper_model": "small"
}

Possible models include:

tiny
base
small
medium
large-v3-turbo
🔊 Text-to-Speech

Jarvis uses Piper for local text-to-speech.

The configuration currently uses:

tts_engine = piper

Piper runs locally and does not require a cloud voice service.

🎤 Dictation Mode

Jarvis includes a voice dictation mode.

The default Windows hotkey is:

Ctrl + Win

Hold the hotkey, speak, and release it to insert the transcription into the active application.

Dictation is designed to work with applications such as:

VS Code
Notepad
Browsers
Terminals
Chat applications
Text editors
🧠 Conversation Memory

Jarvis includes local conversation memory.

Memory is intended to allow the assistant to use relevant information from previous interactions.

The project supports:

Conversation history
Dialogue memory
Memory enrichment
Semantic search when embeddings are available
Local database storage

The database is stored locally.

🔌 MCP Support

Jarvis supports MCP-based integrations.

MCP can allow Jarvis to interact with external tools and services.

Potential integrations include:

GitHub
Home Assistant
Slack
Discord
Databases
Browser automation
Other MCP-compatible tools

Example configuration:

{
  "mcps": {
    "github": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-github"
      ],
      "env": {
        "GITHUB_TOKEN": "YOUR_TOKEN"
      }
    }
  }
}

Never commit real API keys or access tokens to GitHub.

Use environment variables or local configuration files instead.

🌐 Web Search

Jarvis can optionally use web search functionality.

The project supports configurable search providers and fallback behavior.

Web search can be disabled for a completely local setup.

Example:

{
  "web_search_enabled": false
}

When web search is enabled, remember that search requests may leave your computer.

📍 Location Features

Jarvis supports optional location-aware functionality.

Location features use a local MaxMind GeoLite2 City database.

If the database is not installed, Jarvis will continue running but location detection will be unavailable.

To enable location features:

Create a MaxMind GeoLite2 account.
Download the GeoLite2 City database.
Save the database as:
~/.local/share/jarvis/geoip/GeoLite2-City.mmdb

On Windows, this corresponds to a path similar to:

C:\Users\<username>\.local\share\jarvis\geoip\GeoLite2-City.mmdb
⚙️ Configuration

Jarvis supports configuration for:

LLM provider
Ollama
Chat model
Fast model
Whisper
Voice input
Wake word
VAD
TTS
Dictation
Memory
MCP servers
Web search
Location

The current Ollama configuration looks similar to:

{
  "llm_provider": "ollama",
  "llm_base_url": "http://127.0.0.1:11434",
  "llm_chat_model": "llama3.2:3b",
  "ollama_base_url": "http://127.0.0.1:11434",
  "ollama_chat_model": "llama3.2:3b"
}
🏗️ Project Structure
Jarvis/
│
├── src/
│   └── jarvis/
│       ├── llm/
│       ├── memory/
│       ├── tools/
│       ├── voice/
│       └── ...
│
├── scripts/
├── tests/
├── docs/
├── requirements.txt
├── requirements-windows.txt
├── README.md
└── .gitignore
🧪 Testing

Run the test suite:

pytest

Check the Python environment:

python --version

Check Ollama:

ollama --version

Check installed models:

ollama list

Check audio devices:

python -c "import sounddevice as sd; print(sd.query_devices())"
🛠️ Troubleshooting
Jarvis does not hear me

Check the available microphones:

python -c "import sounddevice as sd; print(sd.query_devices())"

Make sure Windows has microphone permissions enabled.

Also make sure the correct virtual environment is active:

.\.venv\Scripts\Activate.ps1
sounddevice cannot load

Install it inside the active virtual environment:

python -m pip install sounddevice

Then test:

python -c "import sounddevice as sd; print(sd.query_devices())"
webrtcvad fails to install

If you see:

Microsoft Visual C++ 14.0 or greater is required

install:

Visual Studio Build Tools → Desktop development with C++

Then restart PowerShell and run:

pip install webrtcvad
Ollama is not recognized

If:

ollama --version

returns:

ollama : The term 'ollama' is not recognized

make sure Ollama is installed and available in your Windows PATH.

Restart PowerShell after installing Ollama.

Then run:

ollama --version
Ollama model does not respond

Check:

ollama list

Then test the model directly:

ollama run llama3.2:3b

If the model responds correctly in Ollama but Jarvis times out, check Jarvis's LLM configuration and timeout settings.

LLM request timed out

If Jarvis shows:

LLM request timed out

first test Ollama directly:

ollama run llama3.2:3b

If Ollama works, check that Jarvis is using:

http://127.0.0.1:11434

and the correct model:

llama3.2:3b

Larger models can require significantly more time and system resources.

🔒 Privacy

Jarvis is designed with a local-first architecture.

When using Ollama locally:

Your voice
    ↓
Whisper
    ↓
Jarvis
    ↓
Ollama
    ↓
Local AI model
    ↓
Piper TTS
    ↓
Your speakers

No cloud LLM is required for the core assistant.

However, optional features such as web search or external MCP integrations may communicate with third-party services.

Always review the services you connect to Jarvis.

🔐 Security

Do not commit:

.env
*.db
*.sqlite
*.sqlite3
.venv/
venv/
__pycache__/
*.pem
*.key
API keys
access tokens
passwords

Make sure your .gitignore contains appropriate entries before pushing the project.

Example:

# Python
__pycache__/
*.py[cod]
*.pyo

# Virtual environments
.venv/
venv/
env/

# Environment variables
.env
.env.*

# Databases
*.db
*.sqlite
*.sqlite3

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db

# Logs
*.log

# Build
build/
dist/
*.egg-info/
🚧 Current Status

Jarvis is actively under development.

Current development focus includes:

Windows compatibility
Local Ollama integration
Reliable voice input
Faster Whisper integration
Piper TTS
Conversation memory
MCP integration
Tool routing
Agent reliability
Performance improvements

Some features may still require additional configuration or may not work identically across operating systems.

🗺️ Roadmap

Planned improvements include:

 Improve Windows audio compatibility
 Improve voice intent detection
 Reduce LLM response latency
 Improve wake-word detection
 Improve MCP tool routing
 Improve memory retrieval
 Add more Windows-specific documentation
 Improve installation automation
 Add more automated tests
 Improve UI and system-tray integration
 Expand cross-platform support
🤝 Contributing

Contributions are welcome.

To contribute:

git clone git@github.com:SupriyaMalakar007/Jarvis.git
cd Jarvis

Create a branch:

git checkout -b feature/my-feature

Make your changes, test them, and commit:

git add .
git commit -m "Add my feature"

Push the branch:

git push -u origin feature/my-feature

Then open a Pull Request on GitHub.

📜 License

See the LICENSE file for the license associated with this project.

👤 Author

Supriya Malakar

GitHub:

https://github.com/SupriyaMalakar007

Project:

https://github.com/SupriyaMalakar007/Jarvis

⭐ Support

If you find this project useful, consider giving the repository a ⭐ on GitHub.

Built with Python, Ollama, Faster-Whisper, Piper TTS, and open-source tools.
