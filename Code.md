# CyberTalk Code Explanation

Welcome to the CyberTalk code explanation page. This document provides an overview of the main files, core logic, and important components that make up CyberTalk. If you’re interested in understanding how CyberTalk works under the hood, you’re in the right place.

---

## Project Structure

A typical CyberTalk project includes the following key files and directories:

```
project - cybertalk/
|
|-> IMAGES/
|-> flask_session/
|-> settings/
|-> static/
|   |
|   |-> profile_pics/
|   |   |
|   |   +-> default.png
|   |-> dark-mode.css
|   |-> favicon.ico
|   |-> logo-dark.png
|   |-> logo.png
|   |-> styles.css
|   +-> yellow-mode.css
|-> templates/
|   |
|   |-> admin.html
|   |-> chat.html
|   |-> chat_room.html
|   |-> error.html
|   |-> error2.html
|   |-> file_explorer.html
|   |-> file_viewer.html
|   |-> generate.html
|   |-> home1.html
|   |-> index.html
|   |-> layout.html
|   |-> login.html
|   |-> mod.html
|   |-> policy.html
|   |-> register.html
|   |-> settings.html
|   +-> timeout.html
|-> README.md
|-> app.py
|-> logins.db
|-> messages.json
+-> typing.json              
```

---

## Main Components

### 1. **User Authentication**
- **Registration & Login:**  
  - Usernames and hashed passwords are stored in `logins.db`.
  - Registration checks for duplicate usernames.
  - Login verifies the password hash.
- **Session Management:**  
  - Uses Flask-Login and Flask-Session for secure user sessions.

### 2. **Group Chat System**
- **Creating & Joining Chats:**  
  - Users can create group chats, which get a unique key.
  - Chats are stored in the database.
  - Users join by entering a valid key.
- **Messaging:**  
  - Messages are stored in `messages.json`, organized by group key.
  - Supports text, image attachments, mentions (`@username`, `@everyone`), and replies.
  - Typing status is tracked in `typing.json`.

### 3. **Image Uploads**
- **Image Handling:**  
  - Images are uploaded to an `IMAGES/` folder, organized by group chat key.
  - Images are auto-deleted after 5 minutes.
  - Profile pictures are saved to `static/profile_pics/`.

### 4. **Admin & Moderator Tools**
- **Admin Panel:**  
  - Access to user management, group chat deletion, image cleanup, and site stats.
  - File explorer for viewing/downloading files on the server (admin only).
- **Moderator Panel:**  
  - Ability to timeout users (temporary chat mute).
  - View current timeouts and cancel them.

### 5. **User Settings**
- **Personalization:**  
  - Profile picture, theme (light/dark/yellow), notification preferences, and panic URL are stored per user in the `settings/` directory.
- **Settings are loaded and saved as `.pkl` files (using Python’s `pickle` module).

### 6. **Security**
- **Role-based Access:**  
  - Certain routes and actions are restricted to admins or moderators.
- **Session Security:**  
  - Sessions are kept server-side and cookies are secured.
- **Image & File Safety:**  
  - Uploaded files use secure filenames.
  - Directories are checked to prevent path traversal attacks.

---

## How Routing Works

- **Flask Routes:**  
  - All functionality is defined in `app.py` as Flask route functions.
  - Each route handles GET/POST requests for pages like `/register`, `/login`, `/chat`, `/settings`, `/admin`, etc.
  - Most routes render HTML templates found in the `templates/` directory.

---

## Important Files Explained

- **app.py**:  
  The heart of CyberTalk. Contains all routes, logic for user authentication, group chat management, messaging, file handling, and more.
- **logins.db**:  
  SQLite database for user credentials and group chat keys.
- **messages.json**:  
  Stores all group chat messages as a dictionary mapping chat keys to lists of messages.
- **typing.json**:  
  Tracks which users are currently typing in which group chats.
- **settings/**:  
  Contains per-user settings files.
- **IMAGES/**:  
  Stores images uploaded to group chats (auto-deleted after 5 minutes).
- **static/profile_pics/**:  
  Stores user-uploaded profile pictures.

---

## Template Rendering

- Uses Jinja2 templating (via Flask) to dynamically generate HTML pages based on user data, messages, settings, and roles.

---

## Extending CyberTalk

If you want to add features or modify the platform:
- Start with `app.py`: add routes and logic as needed.
- Add/modify templates in the `templates/` directory for new pages or UI changes.
- Update the database (`logins.db`) schema if you need new user or chat attributes.
- Always use secure file handling and respect user roles for new features.

---
That is the backend, and frontend of the code for CyberTalk
[Go back to home](/Cybertalk_Wiki/)
