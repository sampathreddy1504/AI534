# Use official Python 3.11 slim image
FROM python:3.11.9-slim

WORKDIR /app

RUN useradd --create-home appuser
USER appuser
ENV HOME=/home/appuser

COPY --chown=appuser:appuser requirements.txt .
RUN python -m pip install --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

COPY --chown=appuser:appuser . .
COPY --chown=appuser:appuser .env .env

# Add user-local bin to PATH to remove warnings
ENV PATH=$HOME/.local/bin:$PATH

EXPOSE 5000

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "5000", "--workers", "1", "--reload"]
