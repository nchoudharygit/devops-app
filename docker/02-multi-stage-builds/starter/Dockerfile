# TODO: This single-stage Dockerfile produces a ~900MB image because it uses the full
# Python image and includes build tools in the final artifact.
# Rewrite it as a multi-stage build to get the final image under 200MB.
#
# Hint:
#   Stage 1 (builder): Use python:3.11 to install deps and build wheels
#     RUN pip wheel --no-cache-dir -r requirements.txt -w /wheels
#   Stage 2 (runtime): Use python:3.11-slim, copy wheels from stage 1, install them
#     COPY --from=builder /wheels /wheels
#     RUN pip install --no-cache-dir --find-links=/wheels -r requirements.txt

#stage 1: builder
FROM python:3.11 AS builder

WORKDIR /app

COPY requirements.txt .
RUN pip wheel --no-cache-dir -r requirements.txt -w /wheels

#stage 2: runtime
FROM python:3.11-slim  AS runtime

WORKDIR /app

COPY requirements.txt .
COPY --from=builder /wheels /wheels
RUN pip install --no-cache-dir --find-links=/wheels -r requirements.txt

COPY . .

EXPOSE 5000
CMD ["python", "app.py"]