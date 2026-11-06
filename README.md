# 🎬 Movie Organizer — Desktop Application & Interactive Presentation

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![GUI Framework](https://img.shields.io/badge/GUI-PyQt5-41CD52?style=for-the-badge&logo=qt&logoColor=white)](https://riverbankcomputing.com/software/pyqt/)
[![Database](https://img.shields.io/badge/Database-SQLite3-003B57?style=for-the-badge&logo=sqlite&logoColor=white)](https://www.sqlite.org/)
[![Presentation](https://img.shields.io/badge/Interactive%20Web-Presentation-orange?style=for-the-badge&logo=html5&logoColor=white)](https://abdulqader-alshihabi.github.io/Movie-Organizer-Desktop-App/)

A full-featured desktop media management software built with **Python**, **PyQt5**, and **SQLite**. Designed with a modular architecture featuring secure user authentication, CRUD operations for movie archives, custom poster management, and dynamic filtering.

---

## 🌟 Key Features

- **🔐 Secure User Authentication:** Multi-user architecture with SHA-256 password hashing and individual user profiles.
- **🎥 Movie Catalog Management:** Full CRUD operations to add, view, update, and delete movies with metadata (Title, Genre, Year, Rating, Custom Poster).
- **🔍 Search & Multi-Criteria Filtering:** Instant search by title and filter by genre, rating, and release date.
- **🖼️ Poster & Asset Storage:** Automated poster image handling and thumbnail rendering in the UI.
- **📊 Interactive Web Presentation:** Includes an interactive web-based presentation viewer in the `presentation/` folder for browser demos.

---

## 🏛️ Architecture & Database Schema

The application follows a clean separation of concerns:
- **`AuthManager`**: Manages secure password hashing, registration, and session state.
- **`DatabaseManager`**: Encapsulates SQLite connection lifecycle and query execution.
- **`UI Layer`**: Qt Designer XML `.ui` templates dynamically loaded and styled via PyQt5.

### Database Tables (`movies.db`):
- `users`: `id`, `password` (SHA-256), `fullname`, `email`, `profile_pic`, `created_at`
- `movies`: `id`, `title`, `genre`, `year`, `rating`, `poster`, `user_id` (Foreign Key referencing `users.id`)

---

## 🚀 Getting Started

### Prerequisites
- Python 3.9 or higher
- `pip` package manager

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Abdulqader-Alshihabi/Movie-Organizer-Desktop-App.git
   cd Movie-Organizer-Desktop-App
   ```

2. **Create and activate a virtual environment (optional but recommended):**
   ```bash
   python -m venv venv
   # On Windows:
   .\venv\Scripts\activate
   # On macOS/Linux:
   source venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application:**
   ```bash
   python movie_organizer.py
   ```

---

## 🌐 Interactive Presentation

The repository includes a web presentation viewer in the `presentation/` directory.  
To view the presentation locally:
- Open `presentation/index.html` in any modern web browser.
- Or visit the live GitHub Pages demo: **[Live Presentation Demo](https://abdulqader-alshihabi.github.io/Movie-Organizer-Desktop-App/)**

---

## 👨‍💻 Author

**Abdulqader Alshihabi**  
- GitHub: [@Abdulqader-Alshihabi](https://github.com/Abdulqader-Alshihabi)  
- Email: [abdulqader.moh.2003@gmail.com](mailto:abdulqader.moh.2003@gmail.com)  
