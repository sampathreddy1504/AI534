# Use official Python 3.11 slim image
FROM python:3.11.9-slim

# Set working directory
WORKDIR /app

# Avoid running as root (optional but safer)
RUN useradd --create-home appuser
USER appuser
ENV HOME=/home/appuser

# Copy and install dependencies first for caching
COPY --chown=appuser:appuser requirements.txt .

# Upgrade pip and install dependencies without cache to save space
RUN python -m pip install --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY --chown=appuser:appuser . .

# Ensure environment variables are available inside the container
# (optional: only if you have a .env file locally)
COPY --chown=appuser:appuser .env .env

# Expose FastAPI port
EXPOSE 5000

# Use a single worker for low-memory environments
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "5000", "--workers", "1", "--reload"]
