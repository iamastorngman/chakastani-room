# Chakastani Room

A password-protected group chat built with Flask, SQLite, HTML, CSS, and JavaScript.

## Included features

- Password-protected room
- Choose a display name when signing in
- Shared group conversation for everyone using the same server
- Messages saved in SQLite
- Automatic message refresh every 1.8 seconds
- `+` attachment button for images, videos, and other files
- Images displayed inside the conversation
- Videos play inside the conversation with browser video controls
- Other attachments appear as download links
- Upload limit: 24 MB per file
- Responsive desktop and mobile layout
- Login-protected API and uploaded files

## Project files

```text
app.py
requirements.txt
Procfile
templates/
  index.html
  login.html
static/
  style.css
  app.js
uploads/       # created automatically when the app starts
chat.db        # created automatically when the app starts
```

## Run locally on Windows

1. Install Python 3.10 or newer.
2. Open Command Prompt in the project folder.
3. Install packages:

   ```bat
   py -m pip install -r requirements.txt
   ```

4. Start the app:

   ```bat
   py app.py
   ```

5. Visit http://127.0.0.1:5000

If no environment variables are configured, the starter defaults are:
- Room password: `wearebestfriends`
- Secret key: a development-only fallback (set a real secret before deployment)

## Configuration

Set these environment variables before running the app:

- `CHAT_PASSWORD`: the shared room password
- `SECRET_KEY`: a long, random secret used to sign login sessions

PowerShell example:

```powershell
$env:CHAT_PASSWORD = "your-private-room-password"
$env:SECRET_KEY = "put-a-long-random-secret-here"
py app.py
```

Never commit real passwords, secret keys, database files, or private uploads to GitHub.

## Deploy on PythonAnywhere

1. Create a Python web app on PythonAnywhere.
2. Clone this repository into your PythonAnywhere home folder, or upload the project files.
3. Open a Bash console and install dependencies in your web app's virtual environment:

   ```bash
   pip install -r requirements.txt
   ```

4. In the PythonAnywhere **Web** tab, set the source code directory to the folder containing `app.py`.
5. Edit the WSGI configuration file and add the project folder to Python's path. Set your own secrets there, then import the Flask app:

   ```python
   import os
   import sys

   project_home = "/home/YOUR_USERNAME/chakastani-room"
   if project_home not in sys.path:
       sys.path.insert(0, project_home)

   os.environ["CHAT_PASSWORD"] = "YOUR_PRIVATE_ROOM_PASSWORD"
   os.environ["SECRET_KEY"] = "YOUR_LONG_RANDOM_SECRET"

   from app import app as application
   ```

6. Select the virtual environment in the Web tab and click **Reload**.

Use your actual PythonAnywhere username and project folder. Do not publish your WSGI secrets.

## Important notes

- This is one shared group room, not individual accounts or private one-to-one chats.
- The SQLite database is stored in `chat.db` beside `app.py`. Back it up to preserve chat history.
- Uploaded files are stored in the local `uploads/` folder. Back it up too.
- On hosting platforms with temporary filesystems, local database and upload files may be lost after redeploys. Use persistent storage or a managed database/object-storage service for production.
- Use HTTPS and a strong password if the app is exposed to the internet.
