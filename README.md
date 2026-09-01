# 🏋️ AI Fitness Coach

[![React](https://img.shields.io/badge/React-19.2-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-8.2-646CFF?logo=vite&logoColor=white)](https://vitejs.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-Express-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![SQLite](https://img.shields.io/badge/Database-SQLite3-003B57?logo=sqlite&logoColor=white)](https://www.sqlite.org/)
[![MediaPipe](https://img.shields.io/badge/Vision-MediaPipe%20Pose-0097A7?logo=google&logoColor=white)](https://developers.google.com/mediapipe)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-3.4-38B2AC?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Google Gemini](https://img.shields.io/badge/AI-Gemini%201.5%20Flash-8E75B2?logo=google&logoColor=white)](https://ai.google.dev/)

> **AI Fitness Coach** is an intelligent, full-stack fitness and workout tracking web application. It combines real-time computer vision pose estimation, automated rep counting, posture analysis, interactive AI coaching, workout routines, and data-driven progress analytics into a sleek, dark-mode cybernetic dashboard.

---

## 📑 Table of Contents

- [Features](#-features)
- [Architecture & Tech Stack](#-architecture--tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Environment Configuration](#environment-configuration)
  - [Running the App](#running-the-app)
- [Deploying to Vercel](#-deploying-to-vercel)
- [Demo Account](#-demo-account)
- [API Reference](#-api-reference)
- [Computer Vision & Pose Estimation](#-computer-vision--pose-estimation)
- [License](#-license)

---

## 🌟 Features

### 1. 📹 Real-Time AI Computer Vision Trainer
- **Live Landmark Tracking**: Uses `@mediapipe/pose` to detect 33 3D skeletal landmarks through your webcam at 30+ FPS.
- **Biomechanical Angle Calculations**: Computes real-time joint angles for knees, hips, elbows, ankles, and torso.
- **Smart Rep Counting & Form Feedback**:
  - Automatically identifies repetitions through state machines (Descent $\rightarrow$ Bottom $\rightarrow$ Ascent $\rightarrow$ Lockout).
  - Evaluates squat depth, knee alignment (detects knee valgus/collapse), torso posture (detects excessive forward lean), and foot stability.
  - Scores form from 0–100% on every rep with instant audio-visual guidance.
- **Exercise Support**: Squats, Push-ups, Jumping Jacks, Forward Lunges, Planks, Deadlifts, and Glute Bridges.

### 2. 🤖 AI Fitness Coach Chatbot
- **Gemini AI Integration**: Powered by `@google/generative-ai` (Gemini 1.5 Flash) for instant fitness consultations, meal planning, and recovery strategies.
- **Offline Fallback Engine**: Built-in intelligent rule engine for workout routines, calorie targets, macro splits, and exercise form guidelines when running without an API key.

### 3. 🏋️ Extensive Exercise Library
- Curated workout directory filterable by muscle groups: **Chest**, **Back**, **Legs**, **Shoulders**, **Arms**, and **Core**.
- Detailed exercise breakdowns with step-by-step instructions, target muscles, difficulty levels, and embedded instructional video guides.

### 4. 📊 Analytics & Progress Dashboard
- Interactive visual charts powered by **Recharts** displaying:
  - Daily & weekly calorie expenditure.
  - Average form accuracy scores over time.
  - Total workout sessions completed and milestone badges.
- Persistent session history with chronological workout logs and feedback.

### 5. 🧮 Smart Calorie & Macro Calculator
- **Mifflin-St Jeor Equation**: Accurately computes Basal Metabolic Rate (BMR) and Total Daily Energy Expenditure (TDEE).
- **Goal Tailoring**: Customizes target caloric intake for fat loss, muscle gain, or maintenance.
- **Macro Breakdown**: Generates target grams and calories for Protein, Carbohydrates, and Fats with multiple split strategies (Balanced, High Protein, Keto, Low Fat).
- Directly syncs and updates the user's active fitness profile.

### 6. 📝 Workout Planner & Notes Checklist
- Custom personal workout notes, to-do items, and session objectives.
- Real-time task toggle, creation, and deletion with persistent local storage.

### 7. 🔐 User Authentication & Custom Profiles
- Secure user registration and login with SHA-256 password hashing.
- Profile customization for fitness level (Beginner, Intermediate, Advanced), primary goals, workout locations (Home / Gym), and target calories.

---

## 🛠️ Architecture & Tech Stack

```
AI Fitness Coach
├── Frontend (React 19 + Vite)
│   ├── UI / Styling: Tailwind CSS, Lucide React, Framer Motion
│   ├── Computer Vision: @mediapipe/pose, @mediapipe/camera_utils, HTML5 Canvas
│   ├── Charts: Recharts
│   └── Routing: React Router DOM v7
│
├── Backend (Node.js + Express)
│   ├── Database: SQLite3 (sqlite3 package)
│   ├── AI Service: Google Generative AI (@google/generative-ai)
│   └── Security: SHA-256 Hashing, CORS, Dotenv
```

---

## 📁 Project Structure

```
.
├── backend/
│   ├── db/
│   │   └── db.js              # SQLite schema initialization, helpers, and seed data
│   ├── routes/
│   │   └── api.js             # REST API endpoints (Auth, Profile, Sessions, AI Chat)
│   ├── .env                   # Backend environment variables
│   ├── fitness.db             # Local SQLite database file
│   ├── index.js               # Express application server entry point
│   └── package.json           # Backend dependencies and scripts
│
├── frontend/
│   ├── public/                # Static public assets
│   ├── src/
│   │   ├── components/
│   │   │   ├── AIChatbot/     # Floating interactive AI coach component
│   │   │   └── Layout/        # Navigation sidebar & responsive layout
│   │   ├── pages/
│   │   │   ├── Auth/          # Login & Register views
│   │   │   ├── Dashboard/     # Main user statistics and metrics view
│   │   │   ├── Exercises/     # Categorized exercise library
│   │   │   ├── Notes/         # Workout notes & task manager
│   │   │   ├── Profile/       # Profile management, setup & Calorie Calculator
│   │   │   ├── Progress/      # Visual charting and history analytics
│   │   │   ├── Trainer/       # Real-time computer vision workout trainer
│   │   │   └── LandingPage.jsx# Hero landing page
│   │   ├── App.jsx            # Routing configuration
│   │   ├── index.css          # Tailwind CSS and global styles
│   │   └── main.jsx           # React DOM root entry
│   ├── package.json           # Frontend dependencies and Vite build scripts
│   ├── tailwind.config.js     # Tailwind design system configuration
│   └── vite.config.js         # Vite bundler configuration
│
├── package.json               # Root workspace scripts (run both frontend & backend)
└── README.md                  # Project documentation
```

---

## 🚀 Getting Started

### Prerequisites
- **Node.js**: v18.0.0 or higher
- **npm**: v9.0.0 or higher
- A working **Webcam** (for real-time pose tracking)

---

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/agastin-8/AI--Fitness-Coach.git
   cd AI--Fitness-Coach
   ```

2. **Install all dependencies**:
   ```bash
   # Install root dependencies
   npm install

   # Install frontend dependencies
   cd frontend
   npm install

   # Install backend dependencies
   cd ../backend
   npm install
   cd ..
   ```

---

### Environment Configuration

In the `backend/` directory, configure your `.env` file (a template is provided in `backend/.env`):

```env
PORT=5000
GEMINI_API_KEY=your_gemini_api_key_here
```

> 💡 **Note**: If `GEMINI_API_KEY` is not provided, the application will automatically fall back to its smart built-in fitness advice engine without errors.

---

### Running the App

You can run both frontend and backend concurrently or independently:

#### Option 1: Run Full Stack from Root
```bash
# Start backend server
npm run dev:backend

# In a second terminal, start frontend dev server
npm run dev:frontend
```

#### Option 2: Run Separately

- **Start Backend** (Runs on `http://localhost:5000`):
  ```bash
  cd backend
  npm run dev
  ```

- **Start Frontend** (Runs on `http://localhost:5173`):
  ```bash
  cd frontend
  npm run dev
  ```

Open your browser and navigate to `http://localhost:5173`.

---

## ⚡ Deploying to Vercel

This repository is pre-configured for **one-click and zero-config deployment on Vercel** as a full-stack application (Vite frontend + Serverless Express API backend).

### Method 1: Deploy via Vercel Dashboard (Recommended)

1. Push your repository to **GitHub**.
2. Go to your [Vercel Dashboard](https://vercel.com/dashboard) and click **"Add New..." $\rightarrow$ "Project"**.
3. Import your `AI--Fitness-Coach` repository.
4. Keep the default settings:
   - **Framework Preset**: Vite (detected automatically)
   - **Root Directory**: `./` (leave default)
   - **Build Command**: `npm run build`
   - **Output Directory**: `frontend/dist`
5. *(Optional)* Under **Environment Variables**, add:
   - `GEMINI_API_KEY`: Your Google Gemini API Key
6. Click **Deploy**. Vercel will build the frontend and deploy the serverless functions in `/api` automatically!

### Method 2: Deploy via Vercel CLI

```bash
# Install Vercel CLI globally
npm i -g vercel

# Login to your Vercel account
vercel login

# Deploy to preview
vercel

# Deploy to production
vercel --prod
```

---

## 👤 Demo Account

The database automatically seeds a pre-populated demo user with historical workout logs on first startup:

- **Email**: `alex@example.com`
- **Password**: `password123`

You can also register a new account at `/register` and set your personalized fitness goals during onboarding.

---

## 🔌 API Reference

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/auth/register` | Register a new user account |
| `POST` | `/api/auth/login` | Authenticate user and return session data |
| `GET` | `/api/user/profile/:userId` | Retrieve user profile details and goals |
| `POST` | `/api/user/profile/:userId` | Update user fitness targets, level, and calorie goals |
| `POST` | `/api/workout/session` | Record a completed workout session with reps, score, and calories |
| `GET` | `/api/workout/stats/:userId` | Get 7-day progress metrics, aggregated calories, and history logs |
| `POST` | `/api/generate-workout` | Generate a customized AI workout routine |
| `POST` | `/api/chat` | Query the AI coach via Gemini API or fallback engine |

---

## 📐 Computer Vision & Pose Estimation

The **Real-Time Trainer** uses a combination of MediaPipe Pose and custom trigonometric vector geometry:

1. **Joint Angle Calculation**:
   $$\theta = \arccos\left(\frac{\vec{BA} \cdot \vec{BC}}{\|\vec{BA}\| \|\vec{BC}\|}\right)$$
   Evaluates angle between points $A$ (Hip), $B$ (Knee), and $C$ (Ankle).

2. **Form Validation Checks**:
   - **Squat Depth**: Validates that hip height drops below knee level ($\text{Knee Angle} \le 90^\circ$).
   - **Knee Valgus**: Compares knee distance to ankle distance across frames to prevent inward knee collapse.
   - **Torso Lean**: Tracks shoulder-to-hip angle against vertical axis to detect spinal strain.
   - **Symmetry & Balance**: Verifies bilateral symmetry between left and right limb kinematics.

---

## 📄 License

This project is licensed under the [ISC License](LICENSE).
