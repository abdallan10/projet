FROM python:3.11-slim

ENV PYTHONUNBUFFERED=1

WORKDIR /app

RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc libpq-dev python3-dev \
    nikto gobuster && \
    rm -rf /var/lib/apt/lists/*

COPY pyproject.toml poetry.lock* ./
RUN pip install poetry && poetry install --no-root

COPY . .

# Expose for API
EXPOSE 8000

# Default command for dev
CMD ["uvicorn", "pentestbox.api.main:app", "--host", "0.0.0.0", "--port", "8000"]