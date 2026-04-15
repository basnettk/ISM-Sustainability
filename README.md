# ISM Sustainability Project

This is a website that teaches people about sustainability at ISM. It has an AI-powered chatbot that can answer questions!

## How to run the website

Follow these steps to get the project working on your own computer.

### 1. Install the "Brain" (Libraries)
We need two libraries for the website to work: **Flask** (which runs the server) and **Requests** (which talks to the AI).

**On Windows:**
```bash
python -m pip install flask requests
```

**On Mac:**
```bash
python3 -m pip install flask requests
```

---

### 2. Start the Website
Now we tell the computer to start hosting the website files so people can see them.

**On Windows:**
```bash
python app.py
```

**On Mac:**
```bash
python3 app.py
```

---

### 3. Open it up!
Once the command is running, you just need to visit the local web address in your browser:

👉 **[http://127.0.0.1:5000](http://127.0.0.1:5000)**

---

### Troubleshooting
- **"No module named flask"**: This usually means the installation in Step 1 failed or you have multiple versions of Python. Make sure to use `python -m pip`.
- **"Address already in use"**: This means a server is already running. Close any old terminal windows and try again!

For a full technical explanation of how the code works, check out [Project_Explanation.md](Project_Explanation.md).