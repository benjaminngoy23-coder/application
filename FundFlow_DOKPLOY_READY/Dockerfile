FROM python:3.12-slim-bookworm

WORKDIR /app

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PORT=8000 \
    DATA_DIR=/app/data

# L'application utilise uniquement la bibliothèque standard Python.
# Aucun pip install ni build Nixpacks n'est nécessaire.
COPY app.py /app/app.py

RUN mkdir -p /app/data \
    && python -m py_compile /app/app.py

EXPOSE 8000

HEALTHCHECK --interval=30s --timeout=5s --start-period=15s --retries=3 \
  CMD python -c "import urllib.request; urllib.request.urlopen('http://127.0.0.1:8000/health', timeout=3)" || exit 1

CMD ["python", "-u", "/app/app.py", "--no-browser"]
