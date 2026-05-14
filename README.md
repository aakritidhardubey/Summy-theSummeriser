# 🎙️ Summy — The Summariser

Summy is an AI-powered web application that transcribes audio and video files and generates concise summaries. Upload a file, get a transcript powered by OpenAI Whisper, a summary powered by Groq (Mixtral), and download the results as a PDF — all from a simple web interface.

---

## ✨ Features

- **Audio & Video Upload** — Supports `.mp4`, `.mkv`, `.mov`, `.wav`, `.m4a`, and other audio/video formats
- **Automatic Transcription** — Uses OpenAI Whisper (`base` model) to transcribe speech to text
- **AI Summarisation** — Summarises transcripts using the Groq API with the `mixtral-8x7b-32768` model
- **Waveform Visualisation** — Generates a waveform image for uploaded audio files
- **PDF Export** — Download the transcript and summary as a formatted PDF
- **User Authentication** — Register/login system with hashed passwords (Flask-Login + Flask-Bcrypt)
- **Per-User Dashboard** — Each user sees only their own uploaded files and summaries
- **Delete Records** — Remove any uploaded summary from your dashboard

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python, Flask |
| Transcription | OpenAI Whisper |
| Summarisation | Groq API (Mixtral-8x7b) |
| Auth | Flask-Login, Flask-Bcrypt |
| User DB | SQLite (via Flask-SQLAlchemy) |
| Transcript Store | MongoDB |
| PDF Generation | fpdf |
| Audio Processing | soundfile, numpy, matplotlib |
| Video Processing | moviepy |

---

## 📁 Project Structure

```
Summy-theSummeriser/
├── app.py                  # Main Flask application
├── database.py             # (Database helpers)
├── models.py               # (SQLAlchemy models)
├── templates/
│   ├── index.html          # Landing page (login/register links)
│   ├── login.html          # Login page
│   ├── register.html       # Registration page
│   └── dashboard.html      # User dashboard (upload, view, download, delete)
├── uploads/                # Uploaded files and generated outputs
├── instance/
│   └── database.db         # SQLite database (auto-created)
└── README.md
```

---

## ⚙️ Installation

### Prerequisites

- Python 3.10+
- MongoDB running locally on `mongodb://localhost:27017/`
- A [Groq API key](https://console.groq.com/)
- ffmpeg (required by Whisper and moviepy for audio/video processing)

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/aakritidhardubey/Summy-theSummeriser.git
   cd Summy-theSummeriser
   ```

2. **Create and activate a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate      # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install flask flask-sqlalchemy flask-bcrypt flask-login pymongo openai-whisper soundfile numpy matplotlib moviepy fpdf requests
   ```

4. **Set your Groq API key**

   In `app.py`, replace the placeholder with your actual key:
   ```python
   GROQ_API_KEY = "your_groq_api_key_here"
   ```

5. **Make sure MongoDB is running**
   ```bash
   mongod
   ```

6. **Run the application**
   ```bash
   python app.py
   ```

7. **Open in your browser**
   ```
   http://127.0.0.1:5000
   ```

---

## 🚀 Usage

1. Go to `http://127.0.0.1:5000` and register a new account.
2. Log in with your credentials.
3. From the **Dashboard**, upload an audio or video file.
4. Summy will:
   - Extract audio from video files automatically
   - Transcribe the audio using Whisper
   - Summarise the transcript using Groq
   - Save results to your MongoDB dashboard
5. View your transcript and summary on the dashboard.
6. **Download** results as a PDF or **Delete** entries you no longer need.

---

## ⚠️ Notes

- The Whisper `base` model is used by default. For better accuracy on longer or noisier audio, consider switching to `small` or `medium` in `app.py`:
  ```python
  whisper_model = whisper.load_model("small")
  ```
- The `SECRET_KEY` in `app.py` should be changed to a secure random value before deploying.
- This project stores user credentials in SQLite and transcripts in MongoDB — ensure both are secured appropriately in production.

---

## 🤝 Contributing

Fork the repository, make your changes, and open a pull request. Bug reports and feature suggestions are welcome via GitHub Issues.

---

## 📄 License

This project is licensed under the MIT License.

---

## 📬 Contact

For issues or feature requests, open an issue on [GitHub](https://github.com/aakritidhardubey/Summy-theSummeriser/issues).
