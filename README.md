Project Structure
Devops-class-activity/
│── backend/          # Node.js + Express API
│   ├── index.js
│   ├── package.json
│   └── package-lock.json
│
│── frontend/         # Static HTML + CSS
│   └── index.html
│
│── docker-compose.yml (future step)
│── README.md

📝 Final README.md (clean version)
# DevOps Class Activity: Simple Blog Platform

A **minimal full-stack blog application** that allows you to view and add blog posts.  

## 📌 Features
- Display a list of blog posts dynamically from the backend.
- Add new posts via a REST API.
- Clean, responsive-friendly HTML/CSS frontend.
- Backend powered by Node.js + Express.
- In-memory storage (no database required).
- Ready to extend with Docker, a database, or frontend framework.

---

## 🚀 Getting Started

### ✅ Prerequisites
- [Node.js](https://nodejs.org/en/download/) installed on your machine
- [Git](https://git-scm.com/downloads) for cloning repo

---

### 🖥️ Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   cd <repo-name>


Backend setup

cd backend
npm install
node index.js


Backend runs on http://localhost:5000

Frontend setup

Open frontend/index.html in your browser

Later, you can make the frontend call the backend API using JavaScript (AJAX or Fetch).

📦 Backend (Node.js + Express)

File: backend/index.js

const express = require('express');
const cors = require('cors');
const bodyParser = require('body-parser');

const app = express();
const PORT = process.env.PORT || 5000;

// Middleware
app.use(cors());
app.use(bodyParser.json());

// In-memory "database"
let posts = [
  {
    id: 1,
    title: "Welcome to my blog!",
    content: "This is the very first post. Share your thoughts, ideas, or anything you'd like to write about.",
    date: "September 29, 2025"
  },
  {
    id: 2,
    title: "Another Day, Another Post",
    content: "Here's another example post. Feel free to customize and add more posts to your blog page!",
    date: "September 28, 2025"
  }
];

// Get all posts
app.get('/api/posts', (req, res) => {
  res.json(posts);
});

// Add a new post
app.post('/api/posts', (req, res) => {
  const { title, content } = req.body;

  if (!title || !content) {
    return res.status(400).json({ error: "Title and content are required" });
  }

  const newPost = {
    id: posts.length + 1,
    title,
    content,
    date: new Date().toLocaleDateString("en-US", {
      year: "numeric",
      month: "long",
      day: "numeric"
    })
  };

  posts.unshift(newPost);
  res.status(201).json(newPost);
});

// Start server
app.listen(PORT, () => {
  console.log(`✅ Backend running on http://localhost:${PORT}`);
});


Run backend:

node index.js

🎨 Frontend (HTML/CSS)

File: frontend/index.html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Simple Blog</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f8f9fa;
      margin: 0;
      padding: 20px;
      color: #333;
    }
    header { text-align: center; margin-bottom: 40px; }
    header h1 { font-size: 2.5rem; color: #007bff; }
    .blog-post { background: #fff; border-radius: 8px; padding: 20px; margin-bottom: 20px; box-shadow: 0 2px 8px rgba(0,0,0,0.1); }
    .blog-post h2 { margin-top: 0; color: #343a40; }
    .blog-post .date { font-size: 0.9rem; color: #6c757d; margin-top: 10px; }
    footer { text-align: center; margin-top: 50px; color: #6c757d; font-size: 0.9rem; }
  </style>
</head>
<body>
  <header>
    <h1>My Simple Blog</h1>
  </header>

  <section class="blog-post">
    <h2>Welcome to my blog!</h2>
    <p>This is the very first post. Here you can share your thoughts, ideas, or anything you'd like to write about.</p>
    <div class="date">Posted on September 29, 2025</div>
  </section>

  <section class="blog-post">
    <h2>Another Day, Another Post</h2>
    <p>Here's another example post. Feel free to customize and add more posts to your blog page!</p>
    <div class="date">Posted on September 28, 2025</div>
  </section>

  <footer>
    &copy; 2025 My Simple Blog. All rights reserved.
  </footer>
</body>
</html>

🔮 Future Improvements

Add persistent database storage (PostgreSQL, MongoDB, etc.).

Create a dynamic frontend (React, Angular, Vue).

Add authentication (users & admin panel).

Containerize with Docker for consistent deployment.

---

 **add Docker support (backend + frontend)** to this project right away, or should we first keep it super simple (just Node.js + HTML/CSS)
