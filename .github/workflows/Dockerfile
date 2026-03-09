# Use a lightweight Python base image
FROM python:3.11-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the requirements file needed to install dependencies
COPY requirements.txt .

# Install Flask from the requirements file
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application files into the container
COPY . .

# Expose port 5000 (the default port Flask uses)
EXPOSE 5000

# Command to run the Flask application
# We use python app/app.py because the app is inside the 'app' folder
CMD ["python", "app/app.py"]
