# TODO: Build a Docker image for the devops-sample-app
#
# Requirements:
# - Use an official Python base image
# - Set a working directory
# - Install dependencies from requirements.txt
# - Copy application source code
# - Expose port 5000
# - Define the command to start the app (python app.py)
#
# Hint: Copy requirements.txt BEFORE copying the rest of the code
# so Docker can cache the dependency installation layer.

FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt ./
RUN pip install -r requirements.txt 


COPY . .    
EXPOSE 7000 

CMD ["python", "app.py"]
