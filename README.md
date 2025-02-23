# Automate_Hubspot_Auth
Here is the answer to your query in English:

---

### Automate HubSpot Authentication Setup and Usage

This project allows you to automate the authentication process with HubSpot using a Python-based backend, a Node.js frontend, and a Redis database for caching. Below are the complete instructions to set up and run the project on your system.

#### Prerequisites

Before you begin, ensure the following are installed:
- **Python 3.9**: For the backend service.
- **Node.js**: For the frontend interface.
- **Docker Desktop**: For running the Redis database. Make sure Docker Desktop is running before proceeding.

#### Installation Steps

Follow these steps to install and configure the project:

1. **Clone the Repository**  
   Open your terminal and run:
   ```bash
   git clone https://github.com/LuniaKunal/Automate_Hubspot_Auth.git
   cd Automate_Hubspot_Auth
   ```

2. **Create a Redis Data Directory**  
   In the project root directory, create a folder to store Redis data:
   ```bash
   mkdir redis-data
   ```

3. **Set Up the Redis Database**  
   Open a Command Prompt (CMD) and run this command in the project root directory:
   ```cmd
   docker run -d --name redis-stack -p 6379:6379 -p 8001:8001 -v %cd%/redis-data:/data redis/redis-stack
   ```
   This starts a Redis container in the background, mapping ports 6379 and 8001, and storing data in the `redis-data` folder.

4. **Install Backend Dependencies**  
   In a PowerShell terminal, run:
   ```powershell
   cd backend
   pip install -r requirements.txt
   cd ..
   ```

5. **Install Frontend Dependencies**  
   In a PowerShell terminal, run:
   ```powershell
   cd frontend
   npm install
   cd ..
   ```

#### Starting the Services

To run the application, you need to start the Redis database, backend, and frontend services in separate terminals.

1. **Ensure Redis is Running**  
   If the Redis container isn’t already running, start it with:
   ```cmd
   docker start redis-stack
   ```
   Verify it’s working by running:
   ```cmd
   docker exec -it redis-stack redis-cli ping
   ```
   If you see "PONG", Redis is operational.

2. **Start the Backend Service**  
   Open a new PowerShell terminal and run:
   ```powershell
   cd backend
   uvicorn main:app --reload
   ```
   This launches the backend server at `http://localhost:8000` with auto-reload for development.

3. **Start the Frontend Service**  
   Open another PowerShell terminal and run:
   ```powershell
   cd frontend
   npm run start
   ```
   This starts the frontend server, typically at `http://localhost:3000` (check your frontend configuration for the exact port).

#### Using the Application

Once all services are running:
- Access the **frontend interface** at `http://localhost:3000` (or the configured port).
- Access the **backend API** at `http://localhost:8000`.
- Follow the instructions on the frontend interface to authenticate with HubSpot.

#### Stopping the Services

To shut down the application:
- **Stop Backend and Frontend**: Press `Ctrl+C` in the terminals running each service.
- **Stop Redis**: In CMD, run:
   ```cmd
   docker stop redis-stack
   ```
- **(Optional) Remove Redis Container**: If you want to delete the container (you’ll need to recreate it later), run:
   ```cmd
   docker rm redis-stack
   ```

---

This guide provides everything you need to set up, run, and stop the Automate HubSpot Authentication project. Follow the steps carefully, and you’ll have the application up and running in no time!
