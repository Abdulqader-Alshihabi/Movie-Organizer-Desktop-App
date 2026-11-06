# CineVault - Netflix-Inspired Movie Organizer & Profile Manager

[![Python Version](https://img.shields.io/badge/Python-3.10%2B-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![GUI Framework](https://img.shields.io/badge/GUI-PyQt5-green.svg?logo=qt&logoColor=white)](https://riverbankcomputing.com/software/pyqt/)
[![Database](https://img.shields.io/badge/Database-SQLite3-lightgrey.svg?logo=sqlite&logoColor=white)](https://www.sqlite.org/)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-orange.svg)](#)
[![Interactive Presentation](https://img.shields.io/badge/Presentation-Live%20Demo-red.svg)](https://abdulqader-alshihabi.github.io/Movie-Organizer-Desktop-App/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An interactive desktop movie catalog and collection organizer featuring a Netflix-inspired dark aesthetic, multi-profile management, flexible authentication, and fluid card animations.

Built with Python, PyQt5, and SQLite3, CineVault delivers a modern streaming-style experience directly to the desktop.

---

## Key Features

### Multi-Profile Management (Netflix-Style)
- **Who's Watching Selection Screen**: Profile selection screen with smooth hover transitions and cinema-style aesthetics.
- **Interactive Avatar Scaling**: Avatars smoothly expand (`QPropertyAnimation` with cubic easing) and illuminate with a clean border and ambient drop shadow on hover.
- **Profile Management**: Full CRUD capabilities for profiles—create, edit display name, upload custom profile pictures, or delete profiles (with cascading movie cleanup).

### Flexible and Secure Authentication
- **Optional Password Protection**: Choose whether to secure individual profiles with a password or keep them open for frictionless access.
- **SHA-256 Cryptographic Hashing**: Secure password hashing ensures credentials are never stored in plaintext.
- **Passwordless One-Click Login**: Profiles without passwords open a dedicated confirmation dialog with "Continue watching" to log in instantly.
- **Dynamic Password Controls**: Add a password to a previously unprotected account, change existing passwords, or remove passwords with one click in the profile editor.

### Interactive Movie Catalog
- **Carousel & Grid Display**: Browse movies with custom poster artwork, title, genre chips, and star ratings.
- **Interactive Card Hover and Lift**: Hovering over a movie card elevates it with an accent border, deep drop shadow, and a smooth play overlay.
- **Selection State**: Clicking a movie highlights it with a focused outline and displays detailed metadata in the inspection panel.
- **Full Movie CRUD**: Add, edit, or delete movies with real-time collection updates.

### Real-Time Search, Filtering, and Sorting
- **Instant Search**: Search movies by title with real-time feedback.
- **Dynamic Multi-Genre Filter**: Automatically extracts unique genres from your collection into a dropdown filter.
- **Multi-Parameter Sorting**:
  - Title (A-Z)
  - Year (Newest first / Oldest first)
  - Rating (Highest first / Lowest first)

---

## Tech Stack and Architecture

| Layer | Technology | Purpose |
| :--- | :--- | :--- |
| **Language** | Python 3 | Core application logic and data processing |
| **GUI Framework** | PyQt5 (Qt Designer) | Native desktop UI, animations, and event handling |
| **Styling** | Qt Style Sheets (QSS) | Custom dark-theme styling inspired by streaming services |
| **Database** | SQLite3 | Local embedded relational database |
| **Security** | `hashlib` (SHA-256) | Password hashing and validation |

### Architecture Highlights
- **Decoupled Architecture**: Business logic (`AuthManager`, `DatabaseManager`) is decoupled from presentation widgets (`ProfileSelectionDialog`, `MovieCarousel`).
- **Declarative Qt UI Files**: UI layouts designed in Qt Designer (`.ui` files) loaded dynamically via `PyQt5.uic`, allowing seamless design iteration.
- **Hardware-Accelerated Effects**: Leveraged `QGraphicsDropShadowEffect` and `QPropertyAnimation` for smooth 60fps card hover animations without layout reflow jitter.

---

## Project Structure

```
Movie-Organizer-Desktop-App/
├── movie_organizer.py      # Main application controller and GUI classes
├── db..py                  # Database schema initialization script
├── movies.db               # SQLite database file
├── requirements.txt        # Python dependency declarations
├── README.md               # Project documentation
│
├── *.ui                    # Qt Designer declarative UI templates
│   ├── welcome.ui          # Netflix-style profile selector screen
│   ├── movie_organizer.ui  # Main catalog and carousel window
│   ├── register.ui         # Profile registration and edit dialog
│   ├── password_entry.ui   # Password unlock dialog
│   ├── confirm_login.ui    # Passwordless Continue watching dialog
│   └── add_movie.ui        # Movie creation and editing dialog
│
├── movie_posters/          # Sample movie poster images
├── users/                  # User avatar images
└── presentation/           # Interactive web-based presentation viewer
    ├── index.html
    ├── style.css
    ├── script.js
    └── presentation.pptx
```

---

## Database Schema

The SQLite relational database maintains referential integrity between users and their personal movie libraries:

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    password TEXT DEFAULT '',
    fullname TEXT NOT NULL,
    email TEXT UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    profile_pic TEXT
);

CREATE TABLE movies (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT,
    genre TEXT,
    year INTEGER,
    rating REAL,
    poster TEXT,
    user_id INTEGER,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

---

## Getting Started

### Prerequisites
- Python 3.8 or higher installed on your system.
- Git installed.

### Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/Abdulqader-Alshihabi/Movie-Organizer-Desktop-App.git
   cd Movie-Organizer-Desktop-App
   ```

2. **Create and Activate a Virtual Environment** (Recommended):
   ```bash
   # Windows
   python -m venv venv
   .\venv\Scripts\activate

   # macOS / Linux
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Launch the Application**:
   ```bash
   python movie_organizer.py
   ```

---

## Engineering Highlights and Design Decisions

1. **Anti-Jitter Geometry Animation**:
   Profile avatars scale smoothly using a fixed-dimension bounding container (`picContainer`) enclosing an inner animated frame (`avatarBox`). This guarantees that expanding an avatar on hover never shifts neighboring grid items.

2. **Non-Blocking Modal Windows**:
   Dialog workflows (Profile Selection, Authentication, Movie Management) properly manage Qt event loop lifecycles, ensuring smooth transitions without orphaned windows or memory leaks.

3. **Graceful Database Constraint Handling**:
   Implemented support for optional passwords while preserving backward compatibility with existing SQLite schema constraints using empty string hashes and robust `NOT NULL` fallback checks.

4. **Layered Dynamic CSS State Management**:
   Applied Qt dynamic properties (`[selected="true"]`, `[hovered="true"]`) combined with `unpolish()` / `polish()` calls to dynamically update widget stylesheets without resetting entire window hierarchies.

---

## Interactive Web Presentation

An interactive browser-based presentation is included in the `presentation/` directory:
- **Live Presentation Demo**: [https://abdulqader-alshihabi.github.io/Movie-Organizer-Desktop-App/](https://abdulqader-alshihabi.github.io/Movie-Organizer-Desktop-App/)

---

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## Author

**Abdulqader Alshihabi**  
- GitHub: [@Abdulqader-Alshihabi](https://github.com/Abdulqader-Alshihabi)  
- Email: [abdulqader.moh.2003@gmail.com](mailto:abdulqader.moh.2003@gmail.com)  
- Portfolio: [https://abdulqader-alshihabi.github.io/](https://abdulqader-alshihabi.github.io/)
