# Deviantika - Full-Stack Online Learning Platform

Deviantika is a modern, full-stack educational app that allows users to stream video lectures/lessons and listen to audiobooks. It consists of a cross-platform mobile client built with Flutter and a RESTful backend server powered by Node.js, Express, and MongoDB.

---

## 🚀 Features

### Mobile Client (Flutter)
- **User Authentication**: Secure signup, login, persistent sessions via local storage, and automatic JWT access token refreshing.
- **Interactive Dashboard**: Clean user interface displaying latest courses, featured audiobooks, and search actions.
- **Video Lesson Player**: Interactive page to view specific lessons/video streaming for courses, powered by `video_player`.
- **Audiobook Player**: Dedicated streaming audio player allowing users to play, pause, seek, adjust, repeat, and favorite (like) audiobooks.
- **Search System**: Find courses and audiobooks instantly.
- **Favorites/Likes**: Keep track of liked courses and audiobooks.
- **User Profile**: View account info and logout options.

### Backend REST API (Node.js & Express)
- **Authentication**: JWT authentication with refresh token rotation and password hashing using bcrypt.
- **Validation**: Strict schema validation using Joi for all endpoints.
- **Admin Guards**: Middlewares to protect course, video, and audiobook creation/updates, restricting them to admins.
- **File Uploads**: Multipart upload capabilities (using Multer) for course videos and audiobook audio files.
- **Media Streaming**: Custom endpoints configured to stream video and audio files from storage directories.

---

## 🛠️ Tech Stack

### Frontend (Mobile App)
- **Framework**: [Flutter](https://flutter.dev/) (Dart)
- **State & Route Management**: [GetX](https://pub.dev/packages/get)
- **Networking**: `http` package
- **Storage**: `get_storage` (fast key-value local storage)
- **Audio Playback**: `audioplayers`
- **Video Playback**: `video_player`
- **Utility**: `wakelock` (keeps the screen awake during playback)

### Backend (REST API)
- **Runtime**: Node.js
- **Framework**: Express
- **Database**: MongoDB (via Mongoose ODM)
- **Authentication**: `jsonwebtoken`, `bcrypt`
- **File Handling**: `multer`
- **Code Standards**: ES Modules (supported via `esm` package)

---

## 📂 Project Structure

```text
├── App/                       # Flutter Mobile Client
│   ├── lib/                   # Source files (.dart)
│   │   ├── main.dart          # Entry point, automatic refresh token loops
│   │   ├── colors.dart        # Global custom app color palette
│   │   ├── login_page.dart    # Login view & API integration
│   │   ├── signup_page.dart   # Registration view
│   │   ├── home_page.dart     # Dashboard showing courses and options
│   │   ├── course_page.dart   # Course overview & video streaming widget
│   │   ├── audiobook_page.dart # Audiobooks catalog view
│   │   ├── audioplay_page.dart # Custom audiobook stream controller
│   │   └── ...
│   └── pubspec.yaml           # Flutter dependencies list
│
└── Backend/                   # Node.js REST API Server
    ├── config/                # Environment variables parsing
    ├── controllers/           # Request controllers (courses, auth, audiobooks, etc.)
    ├── middlewares/           # Authentication check, error handlers, and admin validator
    ├── models/                # MongoDB Mongoose Schemas (User, Course, Video, Audiobook)
    ├── routes/                # Express routing map
    ├── services/              # JWT & refresh services
    ├── uploads/               # Storage directory for course videos
    ├── audiobook/             # Storage directory for audiobook tracks
    ├── package.json           # Backend npm dependencies and scripts
    └── server.js              # Server bootstrapper & DB connection
```

---

## ⚙️ Getting Started

### 1. Backend Server Setup

#### Prerequisites
- Node.js installed on your machine
- MongoDB instance (local or Atlas)

#### Installation
1. Go to the `Backend` directory:
   ```bash
   cd Backend
   ```
2. Install npm dependencies:
   ```bash
   npm install
   # or if using yarn
   yarn install
   ```
3. Set up environment variables:
   - Duplicate the `.env.example` file and rename it to `.env`:
     ```bash
     cp .env.example .env
     ```
   - Open `.env` and fill in your custom values, such as MongoDB connection URI, JWT secrets, and PORT.

4. Start the server:
   - For development mode (uses nodemon):
     ```bash
     npm run dev
     # or
     yarn dev
     ```
   - For production mode:
     ```bash
     npm start
     # or
     yarn start
     ```
   - The backend runs on `http://localhost:8000` by default.

---

### 2. Flutter App Setup

#### Prerequisites
- Flutter SDK configured (`flutter doctor` should be successful)
- An active emulator or physical device connected

#### Installation
1. Go to the `App` directory:
   ```bash
   cd App
   ```
2. Fetch Flutter packages:
   ```bash
   flutter pub get
   ```
3. **Configure API Base URL**:
   By default, the client points to a hosted instance at `https://deviantika-t930.onrender.com`. If you are running the backend locally:
   - Search for `https://deviantika-t930.onrender.com` inside the files in `App/lib/` (including `main.dart`, `login_page.dart`, `signup_page.dart`, `home_page.dart`, `audioplay_page.dart`, `audiobook_page.dart`, etc.).
   - Replace it with your backend IP/URL. For example, if using an Android Emulator, use `http://10.0.2.2:8000`. If using an iOS Simulator or local testing, use `http://localhost:8000`.

4. Run the app:
   ```bash
   flutter run
   ```
   *Note: On your first request, there might be a slight delay if the backend server was inactive or spin-up was slow.*
