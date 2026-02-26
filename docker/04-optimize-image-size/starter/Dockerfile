# TODO: This Dockerfile has multiple anti-patterns that produce a ~1.2GB image.
# Find and fix all of them. Target: final image under 150MB.
#
# Problems to find:
# 1. Wrong base image choice
# 2. Unnecessary packages installed
# 3. RUN steps not chained — breaks layer caching efficiently
# 4. No cleanup of package manager cache
# 5. Copying too much into the image (hint: create a .dockerignore)
# 6. pip installs without --no-cache-dir flag

FROM python:3.9-slim


WORKDIR /app

COPY requirements.txt .
RUN pip3 install --no-cache-dir -r requirements.txt

COPY app.py .
EXPOSE 5000

CMD ["python3", "app.py"]
