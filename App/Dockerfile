# Use the official Python image as a parent image
FROM python:3.8-slim

# Set the working directory to /app
WORKDIR /App

# Copy the current directory contents into the container at /app
COPY . /App

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 8081 available to the world outside this container
EXPOSE 8081

# Run app.py when the container launches
CMD ["python", "app.py"]
