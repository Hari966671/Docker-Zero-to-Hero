# Use the latest Ubuntu as the base image
FROM ubuntu:22.04

# Set non-interactive mode for APT
ENV DEBIAN_FRONTEND=noninteractive

# Set the working directory
WORKDIR /app

# Copy application files
COPY requirements.txt /app
COPY devops /app

# Install system dependencies and Python
RUN apt-get update && \
    apt-get install -y --no-install-recommends python3 python3-pip python3-venv && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Create and use a virtual environment for Python dependencies
RUN python3 -m venv /opt/venv && \
    /opt/venv/bin/python -m pip install --upgrade pip setuptools wheel && \
    /opt/venv/bin/python -m pip install -r requirements.txt

# Update PATH to include the virtual environment
ENV PATH="/opt/venv/bin:$PATH"

# Expose the application port
EXPOSE 8000

# Set the entry point and default command for the container
ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]
