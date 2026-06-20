# 🧩 Face Puzzle Game

An interactive browser-based puzzle game that captures a photo using your webcam, converts it into a sliding puzzle, and challenges users to solve it as quickly as possible.

Built as a single HTML application using pure HTML, CSS, and JavaScript without external frameworks.

---

## 📌 Project Overview

Face Puzzle Game is a webcam-powered puzzle application where users:

- Capture a live photo using their camera
- Select puzzle difficulty (3×3, 4×4, or 5×5)
- Solve a shuffled image puzzle
- Track time, moves, and completion progress
- Store best scores using Local Storage
- View leaderboard rankings after completion

The project focuses on browser APIs, game logic, drag-and-drop interactions, responsive UI design, and local data persistence.

---

## 🎯 Task Objective

Create a complete HTML application that:

- Accesses the user's webcam
- Captures a square image snapshot
- Generates puzzle pieces dynamically
- Supports multiple difficulty levels
- Implements drag-and-drop gameplay
- Tracks timer and moves
- Stores leaderboard records
- Provides responsive desktop and mobile support

---

## 🚀 Features

### 📷 Camera Integration
- Uses WebRTC (`getUserMedia`)
- Live camera preview
- Capture photo directly from browser
- Retake photo option

### 🧩 Puzzle System
- Dynamic puzzle generation
- Difficulty Levels:
  - 3×3 (Easy)
  - 4×4 (Medium)
  - 5×5 (Hard)
- Randomized puzzle arrangement
- Real-time piece swapping

### 🎮 Gameplay
- Drag-and-drop interaction
- Touch support for mobile devices
- Move counter
- Live timer
- Completion progress tracking

### 🏆 Score Tracking
- Best times leaderboard
- Local Storage persistence
- Top score ranking system
- Performance statistics

### 🎨 UI/UX
- Modern dark theme
- Glassmorphism-inspired cards
- Gradient buttons
- Responsive layout
- Animated victory screen

---

## 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| HTML5 | Structure |
| CSS3 | Styling & Responsive Design |
| JavaScript (ES6+) | Game Logic |
| WebRTC API | Camera Access |
| Canvas API | Image Processing |
| Local Storage | Score Persistence |
| Drag & Drop Events | Puzzle Interaction |



---

## 📸 Screenshots



### Game Setup Screen

![Game Setup](screenshots/game-setup.png)

*Photo captured successfully and difficulty selection screen.*

---

### Puzzle Completion Screen

![Puzzle Solved](screenshots/puzzle-solved.png)

*Victory popup displaying completion time, moves, and leaderboard.*

---

## ⚙️ How to Run

### Method 1: Open Directly

1. Download the project.
2. Open:

```text
face-puzzle-game.html
```

in a modern browser.

---

### Method 2: Run with Local Server (Recommended)

VS Code:

```bash
npx serve
```

or

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

---

## 🔐 Permissions Required

The application requires:

- Camera Permission
- Secure Context (HTTPS or localhost)

If camera access is denied, the application displays an error message.

---

## 🧠 Key Learnings

During this project I learned:

### Browser APIs
- WebRTC Camera Access
- Canvas Image Manipulation
- Local Storage Management

### JavaScript Concepts
- DOM Manipulation
- Event Handling
- Drag & Drop Mechanics
- Touch Event Support
- State Management

### UI Development
- Responsive Design
- CSS Grid Layouts
- Flexbox Layouts
- Animations and Transitions

### Game Development
- Puzzle Piece Generation
- Randomization Algorithms
- Score Tracking
- Win Detection Logic

---

## 🔍 Challenges Faced

### Camera Permission Handling
Managing browser permission requests and handling denied access gracefully.

### Dynamic Puzzle Generation
Splitting captured images into equal puzzle pieces while maintaining image quality.

### Drag-and-Drop Support
Implementing both desktop and mobile interactions.

### Performance Optimization
Ensuring smooth gameplay across different devices and screen sizes.

---

## 📈 Future Improvements

- Multiple image upload support
- Online leaderboard
- Multiplayer challenge mode
- Hint system
- Sound effects
- Achievement badges
- Custom puzzle dimensions
- Share score functionality
- PWA support
- AI-generated puzzle themes

---

## ✅ Outcome

Successfully developed a fully functional Face Puzzle Game featuring:

- Webcam image capture
- Multiple difficulty levels
- Responsive gameplay
- Drag-and-drop interactions
- Score tracking system
- Leaderboard functionality
- Modern user interface

The project demonstrates practical implementation of JavaScript, Browser APIs, Canvas Processing, and Interactive Game Development concepts.

---


⭐ If you found this project interesting, consider giving it a star.
