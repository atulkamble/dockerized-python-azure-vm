# dockerized-python-azure-vm
A step-by-step project to Dockerize a Python Flask application and deploy it on an Azure Virtual Machine, featuring Docker, Docker Compose, and automation scripts.



Here's a step-by-step guide to Dockerize a Python application on an Azure Virtual Machine (VM):

---

### **Prerequisites**
1. **Azure VM**: Create an Azure VM (Ubuntu 20.04/22.04 recommended) with public IP.
2. **Docker Installed**: Install Docker on the VM.
   ```bash
   sudo apt update
   sudo apt install -y docker.io
   sudo usermod -aG docker $USER
   ```
   Log out and log back in for group changes to take effect.

3. **Docker Compose Installed**:
   ```bash
   sudo apt install -y docker-compose
   ```

---

### **Step 1: Write the Python Code**
Create a simple Python application. Example: a Flask app.

**`app.py`:**
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, Azure Dockerized Python App!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

---

### **Step 2: Create a Requirements File**
List Python dependencies in a `requirements.txt` file.

**`requirements.txt`:**
```
flask
```

---

### **Step 3: Create a Dockerfile**
Define the steps to containerize the Python application.

**`Dockerfile`:**
```dockerfile
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container
COPY . /app

# Install the dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Make port 5000 available to the outside world
EXPOSE 5000

# Run the application
CMD ["python", "app.py"]
```

---

### **Step 4: Build and Run Docker Container**
1. **Transfer Files to VM**: Use SCP or Filezilla to transfer `app.py`, `requirements.txt`, and `Dockerfile` to your VM.

2. **SSH into VM**:
   ```bash
   ssh <your_username>@<vm_public_ip>
   ```

3. **Build the Docker Image**:
   ```bash
   docker build -t flask-app .
   ```

4. **Run the Docker Container**:
   ```bash
   docker run -d -p 5000:5000 flask-app
   ```

5. **Test the Application**:
   Open your browser and go to `http://<vm_public_ip>:5000`. You should see "Hello, Azure Dockerized Python App!".

---

### **Step 5: Optional - Use Docker Compose**
If your project grows (e.g., with a database), use Docker Compose.

**`docker-compose.yml`:**
```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "5000:5000"
```

Run the application with:
```bash
docker-compose up -d
```

---

### **Step 6: Automate Deployment**
For automated deployment, create a Bash script or use CI/CD tools like GitHub Actions or Azure DevOps.

---

Let me know if you'd like further assistance with deploying this project!
