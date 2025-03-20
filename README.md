# 🚀 Docker Compose Guide

## 1️⃣ What is Docker Compose?
Docker Compose allows you to define and run multiple containers using a single YAML file (`docker-compose.yml`). Instead of running separate `docker run` commands, you define services, networks, and volumes in one file, making setup and management easier.

### Key Benefits:
✅ Runs multiple containers with a single command  
✅ Ensures all containers are on the same network  
✅ Manages container dependencies (e.g., Adminer starts only after MySQL is ready)  
✅ Keeps configurations in one place

---

## 2️⃣ Installing Docker Compose
If you have Docker Desktop, you already have Docker Compose installed! 🎉

To check, open the Docker Desktop terminal (or Command Prompt / PowerShell) and run:

```sh
docker-compose --version
```

If you see a version number, you're good to go! 🚀

---

## 3️⃣ Writing a `docker-compose.yml` File
Let's create a `docker-compose.yml` file to run MySQL and Adminer together.

### Step 1: Open Docker Desktop Terminal
You can use:
- Docker Desktop terminal (Click on the Terminal button)
- Windows PowerShell or Command Prompt
- VS Code Terminal

### Step 2: Create a Project Folder
Navigate to your desired location and create a new directory:

```sh
mkdir my-database
cd my-database
```

### Step 3: Create and Edit `docker-compose.yml`
Create a `docker-compose.yml` file in the `my-database` folder:

```sh
notepad docker-compose.yml
```

Now, paste the following configuration:

```yaml
version: '3.8'
services:
  mysql:
    image: mysql:8
    container_name: mysql_container
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: mydb
      MYSQL_USER: user
      MYSQL_PASSWORD: password
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql
    networks:
      - my_network

  adminer:
    image: adminer
    container_name: adminer_container
    restart: always
    ports:
      - "8080:8080"
    depends_on:
      - mysql
    networks:
      - my_network

volumes:
  mysql_data:

networks:
  my_network:
```

---

## 4️⃣ Running Docker Compose
Once the file is created, run the following command from the same directory:

```sh
docker-compose up -d
```

🚀 This will:
- Pull the MySQL and Adminer images if not already available.
- Start the containers.
- Keep MySQL and Adminer in the same custom network (`my_network`).
- Store MySQL data in a Docker volume (`mysql_data`), so your database isn’t lost when the container restarts.

---

## 5️⃣ Accessing Adminer
Once running, open your browser and go to:

🔗 [http://localhost:8080](http://localhost:8080)

💾 Use these credentials to log in:
- **System**: MySQL
- **Server**: mysql
- **Username**: root
- **Password**: root
- **Database**: mydb

---

## 6️⃣ Stopping and Managing Containers

### Check Running Containers:
```sh
docker ps
```

### Stop Containers:
```sh
docker-compose down
```

### Restart Containers:
```sh
docker-compose restart
```

### View Logs:
```sh
docker-compose logs -f
```

---

## 7️⃣ Next Steps
✅ Your MySQL + Adminer setup is now running!
