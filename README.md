# Stream Tracker - Smart Lecture Progress Tracker

Track real learning progress by analyzing unique watched intervals — not just whether a video played till the end.

🔗 Live Demo: https://s-frontend-alpha.vercel.app/login  
📁 GitHub Repository: https://github.com/Prateek-rajput-007/Stream-Tracker

---

## Problem Statement

Most platforms mark a video "complete" when it finishes playing. However, this doesn’t account for users skipping content or watching the same part repeatedly.

This project accurately tracks how much of a video a user has *actually* watched by only counting unique video segments.

---

## Objectives

- Track unique parts of the video watched
- Prevent progress from increasing if user skips or rewatches
- Persist watched data and resume from last watched position
- Show real-time progress updates as a percentage

---

## Features

- ✅ Accurate tracking of watched intervals
- ✅ Skipping ahead or rewatching does not falsely increase progress
- ✅ Resume from last watched position
- ✅ Display visual progress updates
- ✅ JWT-based authentication for user sessions

---

## Technologies Used

**Frontend:**
- React.js
- Tailwind CSS
- Axios
- React Router

**Backend:**
- Node.js
- Express.js
- MongoDB
- Mongoose
- JSON Web Tokens (JWT) for secure authentication

---

## Folder Structure

frontend/
├── public/
│   ├── video2.mp4
│   ├── video3.mp4
│   ├── video4.mp4
├── src/
│   ├── components/
│   │   ├── VideoPlayer.jsx
│   │   ├── Dashboard.jsx
│   │   ├── Login.jsx
│   │   ├── Register.jsx
│   │   ├── Navbar.jsx
│   ├── pages/
│   │   ├── VideoPage.jsx
│   │   ├── DashboardPage.jsx
│   │   ├── LoginPage.jsx
│   │   ├── RegisterPage.jsx
│   │   ├── AnalyticsPage.jsx
│   ├── App.jsx
│   ├── main.jsx
│   ├── index.css

backend/
├── models/
│   ├── User.js
│   ├── VideoProgress.js
├── routes/
│   ├── auth.js
│   ├── progress.js
├── middleware/
│   ├── auth.js
├── .env
├── server.js

---

## How Unique Watching is Tracked

1. Every second a user watches is logged as an interval.
2. Overlapping intervals are merged on the backend to avoid duplication.
3. Unique seconds are calculated using these merged intervals.
4. Progress (%) = (unique watched seconds / video duration) * 100
5. Data is saved in the database and synced on re-login.

---

## Authentication

- JWT is used for secure user authentication.
- Users receive a token on login/register, stored in localStorage.
- Protected routes validate token using middleware.

---

## Setup Instructions

1. Clone the repo:
   git clone https://github.com/Prateek-rajput-007/Stream-Tracker

2. Navigate to `backend/`:
   - Run `npm install`
   - Create `.env` file with your Mongo URI and JWT secret
   - Run `npm start`

3. Navigate to `frontend/`:
   - Run `npm install`
   - Run `npm run dev`

---

## Design Decisions

- Used JWT for secure and stateless user sessions.
- Used `timeupdate` event for real-time interval tracking.
- Merged intervals using a utility function on backend to avoid duplicates.
- Simple and clean UI with Tailwind CSS.

---

## Challenges Faced

- Ensuring precise interval merging with edge cases.
- Preventing duplicated progress on rewatching.
- Keeping video resume smooth without flickering.

---

## Future Improvements

- Add support for YouTube embeds or external players
- Add analytics dashboard for user video engagement
- Enhance UI with tooltips and time markers

---

## License

This project is for educational and demonstration purposes.
