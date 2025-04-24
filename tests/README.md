# Testing Strynova Hot Reload

This directory contains a minimal Django project for testing the strynova_dj_hotreload package.

## Running the test server

To run the test server, navigate to the `tests` directory and run:

```bash
python manage.py runserver
```

## Testing the hot reload functionality

1. Start the test server as described above
2. Open your browser and navigate to http://127.0.0.1:8000/
3. You should see a welcome page with instructions
4. Make changes to the template file at `test_project/templates/base.html`
5. The browser should automatically reload to show your changes

## What to expect

When the server starts, you should see output including:

```
Starting Strynova Django Hot Reload...
Watching directories: [list of directories]
Watching file types: html, css, js
WebSocket server started at ws://127.0.0.1:8765
Hot reload server running at ws://127.0.0.1:8765
```

When you make changes to a watched file, you should see:

```
File changed: [path to file]
Sent reload notification to [number] clients
```

And your browser should automatically reload to show the changes.

## Troubleshooting

If hot reloading isn't working:

1. Make sure you're running the server with `python manage.py runserver` (not through a WSGI server)
2. Check the browser console for any WebSocket connection errors
3. Verify that the template includes the hot reload JavaScript: `{% load strynova_hot_reload %}{% hot_reload_js %}`
4. Check that the file you're modifying is in one of the watched directories
5. Ensure DEBUG=True in your settings.py

## Project Structure

- `manage.py` - Django management script
- `test_project/` - Django project directory
  - `settings.py` - Django settings (includes strynova_dj_hotreload in INSTALLED_APPS)
  - `urls.py` - URL configuration with a simple home view
  - `templates/` - Directory containing HTML templates
    - `base.html` - Example template with hot reload JavaScript included