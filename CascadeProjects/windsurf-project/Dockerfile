# Base image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy requirements file
COPY requirements.txt ./

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Set the default script to run
ENV SCRIPT=feature_pipelines/technical_indicators.py

# Command to run the application
CMD ["python", "$SCRIPT"]# Base image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy requirements file
COPY requirements.txt ./

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Command to run the application (placeholder)
CMD ["python", "feature_pipelines/technical_indicators.py"]
