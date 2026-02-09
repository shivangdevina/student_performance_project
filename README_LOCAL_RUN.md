# How to Run Locally with Conda (Windows CMD)

Follow these steps to set up and run the project using **Conda** via the **Windows Command Prompt (cmd)**.

### 1. Open Command Prompt
Press `Win + R`, type `cmd`, and hit Enter. Navigate to your project directory:
```cmd
cd /d "c:\CODEBASE\DEPLOYED PROJECTS\student_performance_project"
```

### 2. Create the Conda Environment
Run the following command to create a new environment named `mlenv`:
```cmd
conda create -n mlenv python=3.8 -y
```

### 3. Activate the Environment
```cmd
conda activate mlenv
```

### 4. Install Dependencies
Install all required libraries using `pip`:
```cmd
pip install -r requirements.txt
```
*Note: If you get an error installing `gunicorn`, it's because gunicorn is for Linux. You can ignore it or delete it from requirements.txt; the app will still run fine on Windows for development.*

### 5. Start the Flask Server
Run the application:
```cmd
python app.py
```

### 6. Access the Application
Open your browser and visit:
[http://127.0.0.1:5000](http://127.0.0.1:5000)
