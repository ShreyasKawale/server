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
### CORS Configuration:

```bash
# Add 'corsheaders' to INSTALLED_APPS to enable CORS functionality in Django
INSTALLED_APPS = [
    ...
    'corsheaders',  # Required for handling CORS
    ...
]

# Add 'CorsMiddleware' near the top of the MIDDLEWARE list to intercept and handle CORS requests properly
MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',  # Required to process CORS headers
    ...
]

# Determines whether to allow requests from all origins (True) or restrict them (False)
# Setting to True is useful in development for open access, but False is recommended in production for security
CORS_ALLOW_ALL_ORIGINS = False  # Optional, but should be False in production to limit access

# List of allowed origins if CORS_ALLOW_ALL_ORIGINS is False; 
# Only requests from these domains will be allowed to access your Django API
CORS_ALLOWED_ORIGINS = [
    'https://example.com',
    'https://another-example.com',
]  # Optional, but important if restricting access to specific origins

# Regular expressions to match allowed origins dynamically; useful for more flexible domain matching
# E.g., allowing subdomains
CORS_ALLOWED_ORIGIN_REGEXES = [
    r"^https://\w+\.example\.com$",  # Matches subdomains like "sub.example.com"
]  # Optional, but useful for matching patterns like subdomains

# Allow credentials (like cookies, HTTP authentication) in cross-origin requests
# Needed if your frontend and backend share session cookies or require login/authentication
CORS_ALLOW_CREDENTIALS = True  # Optional, but required if the frontend needs to send credentials

# Specifies how long the preflight OPTIONS response (which checks CORS permissions) can be cached by the browser
# In seconds; 86400 = 1 day
CORS_PREFLIGHT_MAX_AGE = 86400  # Optional, improves performance by reducing preflight requests

# List of HTTP methods that are allowed in CORS requests; limits the methods clients can use
CORS_ALLOW_METHODS = [
    'DELETE',
    'GET',
    'OPTIONS',
    'PATCH',
    'POST',
    'PUT',
]  # Optional, but useful to control which methods are allowed

# List of HTTP headers allowed in CORS requests; limits the headers that can be sent by the client
CORS_ALLOW_HEADERS = [
    'accept',
    'authorization',
    'content-type',
    'origin',
    'user-agent',
    'x-csrftoken',
    'x-requested-with',
]  # Optional, but necessary if you're using custom headers or authentication

# List of response headers to expose to the client; limits the headers clients can see in the response
CORS_EXPOSE_HEADERS = [
    'Content-Type',
    'X-CSRFToken',
]  # Optional, useful if you need the client to see specific headers

# List of trusted origins for CSRF protection, typically needed if CSRF is enabled and you're accepting requests from external domains
# Requests from these domains will bypass the CSRF check
CSRF_TRUSTED_ORIGINS = [
    'https://example.com',
    'https://sub.example.com',
]  # Optional, but required if using CSRF protection and allowing CORS with specific domains
```
