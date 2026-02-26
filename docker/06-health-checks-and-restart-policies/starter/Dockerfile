FROM python:3.11-slim

# Install system dependencies (curl needed for HEALTHCHECK)
RUN apt-get update \
    && apt-get install -y curl \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy requirements first (better layer caching)
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY app.py .

EXPOSE 5000

# TODO: Add a HEALTHCHECK instruction here.
# It should probe GET /health every 30 seconds,
# wait 10 seconds before the first check (start-period),
# timeout after 5 seconds, and retry 3 times before marking unhealthy.
# Hint: python:3.11-slim includes curl.

# Healthcheck
HEALTHCHECK --interval=30s --start-period=10s --timeout=5s --retries=3 \
CMD curl -f http://localhost:5000/health || exit 1



# Run app
CMD ["python", "app.py"]
