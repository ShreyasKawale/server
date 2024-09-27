### How to create the project

Creates the project by running:

```bash
docker compose up --build
```
### Include this database configuration in settings.py

```bash
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "your_project_name",
        "USER": "postgres",
        "PASSWORD": "postgres",
        "HOST": "db",
        "PORT": 5432,
    }
}
```
