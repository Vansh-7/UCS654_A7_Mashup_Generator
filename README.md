# 🎵 YouTube Mashup Generator & Web Service

![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python)
![Flask](https://img.shields.io/badge/Flask-Web_App-green?style=for-the-badge&logo=flask)
![FFmpeg](https://img.shields.io/badge/FFmpeg-Audio_Processing-orange?style=for-the-badge&logo=ffmpeg)

A robust, full-stack Python application that automatically generates audio mashups by downloading songs from YouTube, processing them, and merging them into a single track. This project includes a **Command-Line Interface (CLI)** and a **Web Interface (Flask)** with email delivery capabilities.

---

## 📋 Table of Contents
1.  [Project Overview](#-project-overview)
2.  [Methodology](#-methodology)
3.  [Installation & Setup](#-installation--setup)
4.  [Usage Guide](#-usage-guide)
    * [Program 1: CLI Script](#1-program-1-cli-script)
    * [Program 2: Web Service](#2-program-2-web-service)
5.  [Results & Analysis](#-results--analysis)
6.  [Project Structure](#-project-structure)
7.  [License](#-license)

---

## 🚀 Project Overview

This assignment consists of two major components:
1.  **Mashup Script (`102483084.py`):** A backend script that:
    * Downloads $N$ videos of a specific singer from YouTube.
    * Extracts audio and trims the first $Y$ seconds.
    * Merges all clips into a single seamless audio file.
2.  **Web App (`app.py`):** A Flask-based web interface that:
    * Takes user inputs (Singer, Count, Duration, Email).
    * Triggers the mashup generation in the background.
    * Zips the final result and emails it to the user.

---

## 🛠 Methodology

The project follows a modular pipeline approach to ensure robustness and error handling.

### 1. Data Acquisition (Downloading)
* **Library:** `yt-dlp`
* **Process:** The script searches for the specified singer on YouTube and downloads the top $N$ videos.
* **Optimization:** It uses `ignoreerrors=True` to skip over premium/unavailable videos without crashing the program.

### 2. Audio Processing
* **Library:** `moviepy` (with `ffmpeg` backend)
* **Trimming:** Each downloaded audio file is trimmed to start from `0:00` up to `Y` seconds.
* **Normalization:** Audio is processed to ensure consistent formats (`.mp3`, `.m4a`, etc.) are handled correctly.

### 3. Merging & Effects
* **Merging:** All trimmed clips are concatenated into a single audio track.
* **Post-Processing:** A **Fade-In** (2s) and **Fade-Out** (2s) effect is applied to the master track for a premium listening experience.

### 4. Delivery (Web Service)
* **Framework:** `Flask`
* **Concurrency:** Uses `subprocess` to run the generation script independently, ensuring the web server remains responsive.
* **Emailing:** Uses `smtplib` with SSL to securely send the final `.zip` file to the user's inbox.

---

## ⚙ Installation & Setup

### Prerequisites
* Python 3.7+
* FFmpeg (Placed in the root directory or added to System PATH)

### Step 1: Clone the Repository
```bash
git clone [https://github.com/YOUR_USERNAME/mashup-assignment.git](https://github.com/YOUR_USERNAME/mashup-assignment.git)
cd mashup-assignment
```
### Step 2: Install Dependencies
```bash
pip install -r requirements.txt
```
### Step 3: Configure Environment
Create a `.env` file in the root directory and add your credentials:
```Ini, TOML
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-16-digit-app-password
ROLL_NUMBER_SCRIPT=102483084.py
```
---

## 📖 Usage Guide
### 1. Program 1: CLI Script
Run the script directly from the terminal.
Syntax:
```Bash
python <RollNumber>.py <SingerName> <NumberOfVideos> <Duration> <OutputFileName>
```
Example:
```Bash
python 102483084.py "Ed Sheeran" 20 30 output.mp3
```
* Singer: "Ed Sheeran"
* Count: 20 videos (Must be > 10)
* Duration: 30 seconds (Must be > 20)
* Output: output.mp3

### 2. Program 2: Web Service
Start the local web server:
```Bash
python app.py
```
* Open your browser and go to: `http://127.0.0.1:5000`
* Fill in the form and click **"Generate Mashup"**.
* Wait for the email confirmation! 📧

---

## 📂 Project Structure
```
├── 102483084.py        # Core Logic (CLI Script)
├── app.py              # Web Application (Flask)
├── requirements.txt    # Python Dependencies
├── .env                # Configuration Secrets (GitIgnored)
├── ffmpeg.exe          # Audio Processing Tool
├── .gitignore          # Files to exclude from Git
└── README.md           # Documentation
```
