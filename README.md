# 🧠 Meeting Summarizer (Whisper.cpp + Ollama + Gradio)

This project is an **AI-powered Meeting Summarizer** that converts audio recordings of meetings into **text transcripts** using **Whisper.cpp**, and then **summarizes** them using a **local Ollama LLM model** — all through a simple and beautiful **Gradio web interface**.

---

## 🚀 Features

✅ **Automatic Speech-to-Text** using `whisper.cpp`
✅ **Smart Summarization** using your preferred **Ollama** model
✅ **Context-Aware Summaries** (optional context input)
✅ **Downloadable Transcript File**
✅ **Fully Local Processing** – No API keys, no cloud costs
✅ **Cross-Platform Setup Script** for quick installation

---

## 🧩 Project Structure

```
meeting-summarizer/
│
├── main.py                    # Main Python app with Gradio interface
├── requirements.txt            # Python dependencies
├── setup.sh                    # Auto setup script (builds whisper.cpp, installs deps)
├── whisper.cpp/                # Cloned whisper.cpp repo
│   ├── models/                 # Stores Whisper model binaries (.bin)
│   └── main                    # whisper.cpp binary (after build)
└── README.md                   # You’re reading it now!
```

---

## ⚙️ Installation & Setup

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/<your-username>/meeting-summarizer.git
cd meeting-summarizer
```

---

### 2️⃣ Run the Setup Script

Run the setup file to automatically:

* Create a Python virtual environment
* Install all dependencies (`gradio`, `requests`, etc.)
* Install and build `whisper.cpp`
* Download the chosen Whisper model
* Check for and install `ffmpeg` if missing
* Finally, run the app 🚀

```bash
bash setup.sh
```

---

### 3️⃣ Manual Setup (Alternative)

If you prefer to install manually:

#### 🐍 Create & Activate Virtual Environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

#### 📆 Install Dependencies

```bash
pip install -r requirements.txt
```

#### 🧠 Clone & Build whisper.cpp

```bash
git clone https://github.com/ggerganov/whisper.cpp.git
cd whisper.cpp
make
cd ..
```

#### 📅 Download Whisper Model

```bash
./whisper.cpp/models/download-ggml-model.sh small
```

(You can replace `small` with `base`, `medium`, or `large`.)

---

## 🥪 Running the App

Once everything is set up, launch the Gradio web interface:

```bash
python main.py
```

Gradio will display a local link in your terminal:

```
Running on local URL: http://127.0.0.1:7860
```

Open it in your browser to start using the summarizer.

---

## 🖥️ How It Works

1. **Upload an audio file** (e.g., `.mp3`, `.wav`, `.m4a`, `.flac`)
2. The audio is **converted to 16kHz mono WAV** using FFmpeg
3. `whisper.cpp` generates the **transcript text file**
4. Ollama model (like `llama3`, `mistral`, etc.) summarizes the transcript
5. You can **read, copy, and download** both the summary and transcript

---

## 🧠 Example Flow

| Step | Action                 | Result                                        |
| ---- | ---------------------- | --------------------------------------------- |
| 🎤   | Upload `meeting.mp3`   | Audio converted → Transcript generated        |
| 📝   | Choose Whisper model   | `small` (default)                             |
| 💬   | Choose LLM model       | `llama3`, `mistral`, etc.                     |
| 📚   | (Optional) Add Context | “Team standup about product roadmap”          |
| ⚡    | Click Submit           | Summary generated and transcript downloadable |

---

## 🧩 Dependencies

All dependencies are handled automatically, but here are the key packages:

| Package                 | Purpose              |
| ----------------------- | -------------------- |
| `gradio`                | Web UI               |
| `requests`              | Ollama API calls     |
| `ffmpeg`                | Audio preprocessing  |
| `torch`, `transformers` | (for LLMs if needed) |
| `whisper.cpp`           | Local ASR model      |

---

## 🧱 Requirements

* Python ≥ 3.8
* `ffmpeg` installed
* `ollama` running locally (`ollama serve`)
* Sufficient storage for model binaries (~2–3 GB for large models)

---

## 🧠 Environment Variables

| Variable            | Description                 | Default                  |
| ------------------- | --------------------------- | ------------------------ |
| `OLLAMA_SERVER_URL` | URL for Ollama server       | `http://localhost:11434` |
| `WHISPER_MODEL_DIR` | Directory of Whisper models | `./whisper.cpp/models`   |

---

## 🧩 Available Models

### 🕡 Whisper Models

* `base`
* `small`
* `medium`
* `large`
* `large-V3`

### 💬 LLM Models (Ollama)

Run this to check available models:

```bash
ollama list
```

---

## 🛠️ Troubleshooting

| Problem                                          | Solution                                     |
| ------------------------------------------------ | -------------------------------------------- |
| ❌ “Failed to retrieve models from Ollama server” | Ensure Ollama is running (`ollama serve`)    |
| ❌ `ffmpeg` not found                             | Install manually (`sudo apt install ffmpeg`) |
| ❌ `whisper.cpp/main: not found`                  | Run `make` inside `whisper.cpp` again        |
| ❌ Permission denied                              | Run `chmod +x setup.sh`                      |

---

## 📄 License

MIT License © 2025 — Akash Pandranki

Feel free to use, modify, and distribute this project.

---

## 💡 Credits

* [ggerganov/whisper.cpp](https://github.com/ggerganov/whisper.cpp)
* [Ollama](https://ollama.ai/)
* [Gradio](https://gradio.app/)
