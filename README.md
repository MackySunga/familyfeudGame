# Family Feud – Pinoy Edition (Browser Game)

A lightweight, browser-based **Family Feud–style game** designed for **classrooms, events, and workshops**.  

This project uses **HTML, CSS, and vanilla JavaScript** to create:

- An **Admin screen** (game master controls)
- A **Show screen** (projector/TV view for the audience)
- Features like **Fast Money**, **animated backgrounds**, **sound effects**, **timer**, and **local question editing**.

> **Created by:** **Bob Mathew Sunga**  
> **Intended use:** Free for **educational and non-commercial** purposes.

---

## 🎮 Features

- **Two-screen setup**
  - `feud_admin.html` → Admin / host controls
  - `feud_show.html` → Audience-facing screen

- **Teams & Scores**
  - Up to **4 teams**
  - Editable team names
  - Automatic score updates when answers are revealed
  - Active team highlighting

- **Questions & Answers**
  - Default **Pinoy-themed** question set
  - Edit any question and its answers directly in the admin
  - Save custom questions to `localStorage`
  - Reset a single question or all questions to defaults

- **Strikes**
  - Add / clear strikes (up to 3)
  - Visual display on both admin and show screens
  - Wrong answer sound + red flash on show screen

- **Sounds (using audio files)**
  - Correct answer sound (`correct_star.*`)
  - Wrong/buzz sound (`wrong_buzz.*` or similar)
  - Audience clapping (`audience_clap.*`)
  - Countdown sound (`countdown.*`)
  - All sounds triggered from Admin controls or gameplay events

- **Animated Show Screen**
  - Game-show style animated background
  - Glowing title and board
  - Answers stacked one per row in show mode
  - “Pop” animation when answers are revealed

- **Fast Money Round**
  - Dedicated overlay panel for Fast Money
  - Shows current question and **top 5 answers**
  - Indicates which **team** is playing
  - Shows **round points** and **updated total score**

- **Timer System**
  - Controlled from Admin (start, pause, reset)
  - Configurable seconds (e.g., 30s for Fast Money)
  - Optional “Show/Hide Timer” toggle for the audience
  - Timer appears:
    - Under the main question (normal rounds), or
    - Inside Fast Money header (Fast Money mode)
  - Auto behavior:
    - Plays countdown sound when started (from Admin)
    - When it reaches zero:
      - Hides the timer
      - Plays the wrong/buzzer sound
      - Shows a big **TIME’S UP!** flash on the show screen

- **Visual Feedback**
  - CORRECT / WRONG / TIME’S UP overlays on the show screen
  - Strikes and active team displayed prominently
  - Splash/title screen for introductions & photo ops

---

## 📁 File Structure

A typical project folder might look like this:

```text
family-feud-pinoy/
├── feud_admin.html        # Admin / host control screen
├── feud_show.html         # Audience / projector screen
├── feud_state.js          # Shared game state + questions
├── feud_admin.js          # Admin logic (controls, sounds, timer commands)
├── feud_show.js           # Show logic (display, flashes, timer handling)
├── feud.css               # Shared styles (admin + show)
├── correct_star.wav       # Correct answer sound
├── wrong_buzz.wav         # Wrong answer / time's up buzzer
├── audience_clap.wav      # Audience clapping
└── countdown.wav          # Countdown ticking sound
```

> You can use `.mp3`, `.wav`, or other formats supported by the browser—just make sure the filenames in the JS match the actual files.

---

## 🧰 Requirements

- Any **modern web browser** (Chrome, Edge, Firefox, etc.)
- No server required – can run from:
  - Opening the `.html` files directly, or
  - Serving from a simple static server (VS Code Live Server, `python -m http.server`, etc.)

---

## 🚀 Getting Started

1. **Download or copy** all files into a single folder.
2. Make sure your **sound files** are named the same as in `feud_admin.js` and `feud_show.js`:
   - `correct_star.wav`
   - `wrong_buzz.wav`
   - `audience_clap.wav`
   - `countdown.wav`
3. Open **`feud_show.html`** in a browser and drag it to the projector/second screen.
4. Open **`feud_admin.html`** in another browser window (for the host/admin).

> To avoid browser restrictions on `localStorage` and audio, it’s often best to serve the files via a small local server (e.g., VS Code Live Server, or run `python -m http.server` in the folder and visit `http://localhost:8000`).

---

## 🕹 How to Use (Game Flow)

### 1. Setup

- On the **Admin screen**:
  - Set up **Team Names** (e.g., “Engineering 1A”, “Professors”, etc.).
  - Check the **question list** and edit any question/answers if needed.
- On the **Show screen**:
  - Use the **Splash mode** to display the title while you introduce the game.

### 2. Screen Modes

On the admin panel, you can select:

- **Splash**  
  Shows a big title card for intros & photos.
- **Main Board**  
  The standard Family Feud board (questions + stacked answers).
- **Fast Money**  
  Overlays a Fast Money panel with:
  - The current question
  - Top 5 answers
  - Team playing + round and total scores
  - Fast Money timer (if enabled)

### 3. Playing a Round

1. Select the **current question** (via the select dropdown or Prev/Next).
2. Set the **active team** (“Team X Turn” buttons).
3. Ask the question.
4. When a team guesses a correct answer:
   - Click that answer on the **Admin board**.
   - It will:
     - Reveal that answer on the **Show screen**.
     - Add the answer’s points to the **active team’s score**.
     - Play the **correct** sound and show a green flash.
5. When a team gives a wrong answer:
   - Click **Add Strike**.
   - It will:
     - Add a strike (up to 3).
     - Play the **buzz** sound.
     - Show a red **WRONG!** flash.

### 4. Fast Money Round

1. Pick the question you want to use for **Fast Money**.
2. Click **“Fast Money”** in screen mode.
3. Ensure the **correct team** is active (this team’s score will be updated).
4. Use the **Timer**:
   - Set seconds (e.g., `30`).
   - Click **Show Timer**.
   - Click **Start** → countdown sound plays, timer appears in the Fast Money header.
5. Reveal answers as the player gives them:
   - The first 5 answers are shown in the Fast Money panel.
   - Each revealed answer:
     - Adds points to that team’s total.
     - Updates **Round: +NN pts | Total: TT pts** in the header.
6. When time runs out:
   - Timer hits **0**.
   - Timer hides automatically.
   - **Buzzer** plays.
   - A golden **TIME’S UP!** flash appears on the show screen.

---

## 💾 Data & Persistence

- **Game state** (scores, current question, strikes, revealed answers, team names, screen mode) is saved via `localStorage` under `feud_pinoy_state_v1`.
- **Custom questions** are also stored locally in `localStorage` under `feud_pinoy_questions_v1`.
- You can:
  - **Reset just one question** to its default (button in the editor).
  - **Reset all questions** back to defaults (admin button).
  - **Reset the game** to clear scores and state (admin button).

> Note: Because everything is in `localStorage`, each browser/computer has its *own* saved state and question set.

---

## 🎨 Customization Tips

- **Changing sounds**  
  Replace the audio files or change the filenames in:
  - `feud_admin.js`
  - `feud_show.js` (for the time’s up buzzer)

- **Changing the background/theme**  
  Most of the visual style lives in `feud.css`, including:
  - Game show background animations → `body.show-mode::before` / `::after`
  - Answer card style → `.answer-card`
  - Fast Money overlay → `.fast-money-panel`, `.fast-answer-card`

- **Changing the default questions**  
  In `feud_state.js`, edit the `defaultQuestions` array.

---

## ⚖️ License / Usage

This project is intentionally kept simple so it can be used in **schools, workshops, and community events**.

**Suggested license (non-commercial, educational use):**

> Copyright © 2025, Bob Mathew Sunga  
>  
> You are free to **use, copy, modify, and distribute** this project for  
> **educational and other non-commercial purposes**, provided that:  
> 
> - You keep this notice and credit the original author: **Bob Mathew Sunga**  
> - You do **not** sell this project or include it in a paid product/service  
> - You understand this project is provided **“as is”**, without any warranty  
> 
> For commercial use, please contact the author for permission.

If you prefer something more formal, you can adapt this to a proper license such as **CC BY-NC 4.0** (Attribution–NonCommercial) or switch to MIT if you want to allow commercial use.

---

## 🙏 Credits

- Concept inspired by the TV show **“Family Feud”** (this project is an **unofficial, fan-made educational tool**, not affiliated with or endorsed by the official rights holders).
- Code & design by **Bob Mathew Sunga**.
- Sound effects and visual ideas adapted for use in a **classroom / event setting**.
