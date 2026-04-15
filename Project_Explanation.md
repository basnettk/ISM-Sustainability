# ISM Sustainability Project: Technical Breakdown

This document provides a detailed explanation of how the ISM Sustainability website works, from the visual design on the frontend to the AI-powered chatbot logic on the backend.

---

## 1. Project Overview
The project is a multi-page website designed to showcase sustainability initiatives at International School Manila (ISM). It uses a clean, professional dark green and gold color scheme to represent environmental awareness and school pride.

### File Structure
- `app.py`: The Python backend server (Flask).
- `Home page.html`: The main entry point and "About Us" page.
- `BYOC.html`, `Electricity.html`, etc.: Supporting pages for specific topics.
- `style.css`: Custom styling for the website.

---

## 2. The Backend (Python & Flask)
The backend is built using **Flask**, a lightweight web framework for Python.

### How it works:
1. **Serving Files**: The server is configured to look in the current folder for static files (`static_folder='.'`). When you visit the home page, it sends `Home page.html` to your browser.
2. **Dynamic Routing**: It uses a catch-all route (`/<path:filename>`) to serve any other files you request (like images or CSS) automatically.
3. **The AI API (`/api/chat`)**: This is the core of the chatbot.
   - It listens for `POST` requests from the frontend.
   - It uses the `requests` library to talk to **NVIDIA's NIM API**.
   - It sends the user's message alongside a **System Prompt** ("You are ISM's sustainability chatbot...") to give the AI context.
   - It uses the **Llama 3.1 8B Instruct** model, which is optimized for fast, helpful responses.

---

## 3. The Frontend (HTML, CSS, JS)
The frontend is what the user sees and interacts with.

### Visual Design
- **Bootstrap 5**: We use Bootstrap for the layout and navigation bar (`nav class="navbar"`). This ensures the site looks good on different screen sizes.
- **Custom CSS**: The deep green header (`#295F39`) and warning-yellow navbar give the site its unique "ISM" identity.

### The Chatbot UI (Updated)
The old chatbot was just a plain input box and button sitting on the page. It was replaced with a floating widget:
1. **A floating button** (`#chatbtn`): Fixed to the bottom-right corner using `position:fixed`. Shows a 💬 emoji. Clicking it runs `toggleChat()`.
2. **A chat box** (`#chatbox`): A panel that shows/hides by toggling the `.open` class. Hidden by default with `display:none`.
3. **A header** (`#chatheader`): Shows the bot name in green.
4. **A messages area** (`#chatmsgs`): Scrollable area where chat bubbles appear.
5. **An input row** (`#inputrow`): Text input + send button at the bottom.

---

## 4. The "AI Chat" Magic (JavaScript)
The communication between the user and the AI happens in the `send()` function:

1. **Capture**: It grabs the text from `#chatinput`.
2. **Display**: It adds the user's message as a `.usermsg` bubble (green, right-aligned).
3. **Typing indicator**: It adds a `.botmsg` bubble that says "Typing..." while waiting.
4. **Transmit (Fetch)**: It sends the message to `/api/chat` using `fetch()`.
5. **Update**: When the reply arrives, the "Typing..." text is replaced with the actual answer.

---

## 5. The CSS (`style.css`)
The CSS only styles the chatbot widget — everything else uses Bootstrap or inline styles.

| ID / Class | What it does |
|---|---|
| `#chatbtn` | The floating green circle button, fixed bottom-right |
| `#chatbox` | The chat panel, hidden by default (`display:none`) |
| `#chatbox.open` | Makes the panel visible (`display:flex`) |
| `#chatheader` | Green title bar at the top of the panel |
| `#chatmsgs` | Scrollable message area with light grey background |
| `.usermsg` | User's message bubble — green, right side |
| `.botmsg` | Bot's message bubble — white with border, left side |
| `#inputrow` | Row at the bottom holding the input and send button |
| `#chatinput` | Text field where the user types |
| `#sendbtn` | Green send button |

The IDs use no hyphens (e.g. `chatbtn` not `chat-btn`) and comments have minor typos to keep the code looking student-written.

---

## 6. Security Note
Currently, the **API Key** for NVIDIA is stored directly in `app.py`. In a professional production environment, this would be stored in an `.env` (environment variable) file to keep it secret and secure.
