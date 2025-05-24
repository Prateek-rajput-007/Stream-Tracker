
# 🎥 Video Learning Platform

A full-stack video learning platform that allows users to watch videos, take notes, and track unique video progress through watched intervals.

---

## 🚀 Features

* 📹 Video player with real-time progress tracking
* 📝 Timestamped notes panel beside the video
* 📊 Intelligent merging of watched intervals to avoid double-counting
* 🎯 Dynamic dashboard to show percentage watched
* 💾 Notes & video progress stored per user
* 🎨 Tailwind CSS responsive UI

---

## 🛠️ Tech Stack

**Frontend**: React.js, Tailwind CSS, React Player
**Backend**: Node.js, Express.js, MongoDB, Mongoose
**Authentication**: JWT
**Other Tools**: Context API, Git, Postman

---

## 📁 File Structure

### 📦 Frontend (`/client`)

```
client/
├── public/
│   └── index.html
├── src/
│   ├── components/
│   │   ├── Navbar.jsx
│   │   ├── VideoPlayer.jsx
│   │   ├── NotesPanel.jsx
│   │   ├── Dashboard.jsx
│   │   └── ProgressBar.jsx
│   ├── context/
│   │   └── AuthContext.jsx
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── Login.jsx
│   │   └── Register.jsx
│   ├── utils/
│   │   └── intervalUtils.js  // merging watched intervals
│   ├── App.js
│   ├── index.js
│   └── App.css
├── tailwind.config.js
└── package.json
```

### 📦 Backend (`/server`)

```
server/
├── config/
│   └── db.js  // MongoDB connection
├── controllers/
│   ├── authController.js
│   ├── videoController.js
│   └── notesController.js
├── middleware/
│   ├── authMiddleware.js  // JWT verification
│   └── errorHandler.js
├── models/
│   ├── User.js
│   ├── Video.js
│   └── Note.js
├── routes/
│   ├── authRoutes.js
│   ├── videoRoutes.js
│   └── noteRoutes.js
├── utils/
│   └── mergeIntervals.js  // Merging watched intervals
├── .env
├── server.js
└── package.json
```

---

## ⚙️ Setup Instructions

### 1. Clone the Repo

```bash
git clone https://github.com/your-username/video-learning-platform.git
cd video-learning-platform
```

### 2. Setup Frontend

```bash
cd client
npm install
npm start
```

### 3. Setup Backend

```bash
cd server
npm install
touch .env
```

Inside `.env`, add:

```
PORT=5000
MONGO_URI=your_mongodb_uri
JWT_SECRET=your_secret_key
```

Then start the backend server:

```bash
npm run dev
```

---

## 📐 Design Documentation

### 🔍 Watched Interval Tracking

We used the `onProgress` event from React Player to get the current playback time, which is then stored as intervals:

```js
{ start: 120, end: 150 }
```

We track intervals when playback starts and ends or when the user seeks.

---

### 🧠 Merging Intervals

To calculate unique watched time (excluding overlaps), we:

1. Sort intervals by start time.
2. Merge overlapping or adjacent ones.
3. Sum the total length of merged intervals.

```js
function mergeIntervals(intervals) {
  intervals.sort((a, b) => a.start - b.start);
  const merged = [];

  for (const interval of intervals) {
    const last = merged[merged.length - 1];

    if (!last || interval.start > last.end) {
      merged.push(interval);
    } else {
      last.end = Math.max(last.end, interval.end);
    }
  }

  return merged;
}
```

---

### ⚠️ Challenges & Solutions

| Challenge               | Solution                                            |
| ----------------------- | --------------------------------------------------- |
| Overlapping Intervals   | Merged using a sort + merge pattern                 |
| Scrubbing through video | Added seek detection logic to track skips           |
| Notes syncing           | Tied notes with `playedSeconds` at time of creation |
| Performance             | Throttled progress updates using custom logic       |

