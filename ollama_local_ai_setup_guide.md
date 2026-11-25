# Local AI Setup Guide with Ollama
**Octal Foundry Community — The Local AI Blueprint**

This guide walks you through installing Ollama, starting the local background server, pulling a compact open-weights model suitable for everyday student laptops, and running your first offline AI prompt.

---

## 1. Install Ollama

Choose the instructions for your operating system below.

### Linux (Ubuntu, Debian, Fedora, Arch, etc.)
Open your terminal and run the official install script using `curl`:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

### macOS
**Option A: Direct Installer (Recommended)**
1. Download the macOS installer from [ollama.com/download](https://ollama.com/download).
2. Unzip the downloaded file and drag **Ollama.app** into your **Applications** folder.
3. Open **Ollama** from Applications to complete the command-line setup.

**Option B: Homebrew**
```bash
brew install ollama
```

### Windows (Windows 10 or 11)
1. Go to [ollama.com/download](https://ollama.com/download) and click **Download for Windows** (`OllamaSetup.exe`).
2. Double-click `OllamaSetup.exe` and click **Install**.
3. Once installed, open **Command Prompt** or **PowerShell**.

---

## 2. Verify Installation & Start the Ollama Server

### Check that Ollama is recognized
Run this command in your terminal (Linux/macOS) or PowerShell (Windows):

```bash
ollama --version
```

### Start the Ollama Service
* **macOS & Windows:** Ollama starts automatically in the background once you launch the app (you will see the small llama icon in your top menu bar or bottom-right system tray).
* **Linux:** The install script sets up and starts a `systemd` service automatically. If you ever need to start or verify it manually:

```bash
# Check if the background service is running
systemctl status ollama

# If it is not active, start it manually in your terminal:
ollama serve
```

> **Note:** If `ollama serve` says `Error: listen tcp 127.0.0.1:11434: bind: address already in use`, that is good news—Ollama is already running in the background.

---

## 3. Pull a Lightweight Model

For student laptops (especially machines with 8 GB RAM) and faster downloads on mobile or campus Wi-Fi, start with a compact **1B–2B parameter** quantized model:

```bash
ollama pull gemma3:1b
```

*(Optional alternative: `ollama pull qwen3:1.7b` or `ollama pull llama3.2:1b`)*

To confirm the model downloaded properly and see its size on disk:

```bash
ollama list
```

---

## 4. Run Your First Local Model

Launch an interactive chat session directly in your terminal:

```bash
ollama run gemma3:1b
```

### Try These Test Prompts
Once you see the `>>>` prompt, test it offline (you can even turn off your Wi-Fi to verify it runs 100% locally):

1. `Explain how DNS works to a first-year computer science student in 4 bullet points.`
2. `Write a Python function that checks if a number is prime and explain its time complexity.`

### Useful Commands Inside the Chat Prompt
* `/show info` — View model architecture, parameter count, context window, and quantization format.
* `/clear` — Clear the current conversation context.
* `/bye` — Exit the chat session and return to your terminal.

---

## 5. Check Running Models & Memory Usage

Open a second terminal window while your model is active and run:

```bash
ollama ps
```

This shows which model is currently loaded into your RAM or GPU VRAM and how much memory it is using.

---

## 6. Quick Troubleshooting

* **`ollama: command not found` (Windows/macOS):** Close and reopen your terminal or PowerShell window after installation so your system `PATH` refreshes.
* **Slow responses on older laptops:** Close heavy browser tabs to free up RAM, and stick to `1b` models (`gemma3:1b` or `llama3.2:1b`) rather than `7b` or `8b` models.
* **Connection refused (`127.0.0.1:11434`):** Make sure the Ollama desktop app is open (Windows/macOS) or run `ollama serve` in a separate terminal tab (Linux).