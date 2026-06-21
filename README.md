# Ollama Model Splitter & Offline Reconstructor

This directory contains the files used to download and chunk the **Qwen2.5-Coder-7B-Instruct (Q4_K_M GGUF)** model, and instructions for reconstruct and import it on your offline office laptop.

## How the Split and Upload Work

1. Run `python split_and_upload.py` to:
   - Download the model from Hugging Face: `qwen2.5-coder-7b-instruct-q4_k_m.gguf` (~4.7 GB).
   - Split it into 3 equal chunks: `.parta`, `.partb`, and `.partc` (each ~1.57 GB).
   - Upload the chunks to GitHub release assets on `chandanv106/q4`.
   - Clean up the large 4.7 GB downloaded model file locally to save disk space.

---

## Reconstruction on Office Laptop (Offline Environment)

Since GitHub is accessible from your office laptop, follow these steps to reconstruct and import the model:

### Step 1: Download the Chunks
1. Open GitHub in your office laptop browser and navigate to your repository releases:
   `https://github.com/chandanv106/q4/releases/tag/v1.0.0-qwen-coder`
2. Download all 3 chunk files to the same folder on your office laptop:
   - `qwen2.5-coder-7b-instruct-q4_k_m.gguf.parta`
   - `qwen2.5-coder-7b-instruct-q4_k_m.gguf.partb`
   - `qwen2.5-coder-7b-instruct-q4_k_m.gguf.partc`

### Step 2: Combine the Chunks
Open your command terminal (Command Prompt or PowerShell) on Windows, navigate to the folder where you downloaded the parts, and run the following command:

**For Windows (Command Prompt - CMD):**
```cmd
copy /b qwen2.5-coder-7b-instruct-q4_k_m.gguf.parta + qwen2.5-coder-7b-instruct-q4_k_m.gguf.partb + qwen2.5-coder-7b-instruct-q4_k_m.gguf.partc qwen2.5-coder-7b-instruct-q4_k_m.gguf
```

**For Windows (PowerShell):**
```powershell
cmd /c "copy /b qwen2.5-coder-7b-instruct-q4_k_m.gguf.parta + qwen2.5-coder-7b-instruct-q4_k_m.gguf.partb + qwen2.5-coder-7b-instruct-q4_k_m.gguf.partc qwen2.5-coder-7b-instruct-q4_k_m.gguf"
```

**For macOS / Linux (if applicable):**
```bash
cat qwen2.5-coder-7b-instruct-q4_k_m.gguf.part* > qwen2.5-coder-7b-instruct-q4_k_m.gguf
```

This will reconstruct the original 4.7 GB GGUF model file.

---

### Step 3: Import into Ollama
To run the model with Ollama on your office laptop:

1. Create a text file named `Modelfile` (without any extension) in the same directory as the reconstructed GGUF file.
2. Paste the following configuration into the `Modelfile`:
   ```dockerfile
   FROM ./qwen2.5-coder-7b-instruct-q4_k_m.gguf
   
   # Set parameter temperature
   PARAMETER temperature 0.7
   
   # Set context window size (Qwen2.5 supports up to 32k)
   PARAMETER num_ctx 16384
   
   # Set system prompt
   SYSTEM "You are a helpful, expert AI programming assistant."
   ```
3. Open a terminal and run the Ollama create command:
   ```bash
   ollama create qwen2.5-coder-7b -f Modelfile
   ```
4. Now you can run the model locally on your office laptop anytime:
   ```bash
   ollama run qwen2.5-coder-7b
   ```
