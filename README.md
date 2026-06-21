# Offline Model Setup Guide

Follow these simple steps on your office laptop to reconstruct and use the Qwen2.5-Coder-7B model.

---

## Step 1: Download Ollama
Since you can't access other websites, download the official Ollama installer directly from GitHub:
👉 **[Ollama Setup Installer (GitHub Releases)](https://github.com/ollama/ollama/releases)**
*(Download `OllamaSetup.exe` from the latest release assets and run it to install).*

---

## Step 2: Combine the Chunks
1. Download all 3 chunk files from your release section to your **Downloads** folder:
   - `qwen2.5-coder-7b-instruct-q4_k_m.gguf.parta`
   - `qwen2.5-coder-7b-instruct-q4_k_m.gguf.partb`
   - `qwen2.5-coder-7b-instruct-q4_k_m.gguf.partc`

2. Open **Command Prompt** (search for `cmd` in the Windows Start Menu).
3. Navigate to your Downloads folder:
   ```cmd
   cd Downloads
   ```
4. Run this command to reconstruct the model file:
   ```cmd
   copy /b qwen2.5-coder-7b-instruct-q4_k_m.gguf.parta + qwen2.5-coder-7b-instruct-q4_k_m.gguf.partb + qwen2.5-coder-7b-instruct-q4_k_m.gguf.partc qwen2.5-coder-7b-instruct-q4_k_m.gguf
   ```

---

## Step 3: Import into Ollama
1. Open **Notepad**.
2. Paste the following configuration:
   ```dockerfile
   FROM ./qwen2.5-coder-7b-instruct-q4_k_m.gguf
   
   PARAMETER temperature 0.7
   PARAMETER num_ctx 16384
   SYSTEM "You are a helpful, expert AI programming assistant."
   ```
3. Save the file in your **Downloads** folder.
   - Set "Save as type" to **All Files (*.*)**.
   - Save it exactly as **`Modelfile`** (make sure there is no `.txt` extension).
4. Run the following command in the Command Prompt (still in your Downloads folder):
   ```cmd
   ollama create qwen2.5-coder-7b -f Modelfile
   ```

---

## Step 4: Run the Model
Start using your offline coding assistant by running:
```cmd
ollama run qwen2.5-coder-7b
```
