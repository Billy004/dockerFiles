# DevOps CI/CD Pipeline - Step by Step

## Step 1: Create Containers and Volumes

### What we're setting up:
- **GitLab** - Self-hosted Git repository (Port 8080)
- **GitLab Runner** - Executes CI/CD jobs
- **MySQL** - Database server (Port 3306)
- **Redis** - Cache server (Port 6379)
- **PHPMyAdmin** - Database management UI (Port 8081)

---

## 🚀 Let's Start!

### 1. Create the environment file

```powershell
# Navigate to devops folder
cd c:\wamp642\www\dockerFiles\devops

# Create .env file from example
copy env.example .env
```

You can edit `.env` to change passwords if you want.

### 2. Create directories for volumes

```powershell
# Create all necessary directories
mkdir gitlab\config
mkdir gitlab\logs
mkdir gitlab\data
mkdir runner\config
mkdir mysql_data
mkdir redis_data
```

### 3. Start all containers

```powershell
# Pull images and start containers
docker-compose up -d
```

This will download and start all containers. First time will take a few minutes.

### 4. Check if everything is running

```powershell
# Check container status
docker-compose ps

# Watch the logs (press Ctrl+C to exit)
docker-compose logs -f
```

All containers should show "Up" status.

---

## 📍 Access Points

Once containers are running, you can access:

- **GitLab**: http://localhost:8080
- **PHPMyAdmin**: http://localhost:8081
- **MySQL**: localhost:3306 (username: `express_user`, password: `userPassword123`)

---

## 🔑 Get GitLab Password

GitLab takes 2-3 minutes to fully start. Once it's ready, get the initial password:

```powershell
# Wait for GitLab to finish starting, then run:
docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```

**Login credentials:**
- Username: `root`
- Password: (from the command above)

---

## ✅ Verify Everything Works

### Test GitLab
- Open http://localhost:8080
- Login with root and the password
- You should see the GitLab dashboard

### Test PHPMyAdmin
- Open http://localhost:8081
- Server: `mysql`
- Username: `root`
- Password: `rootPassword123`
- You should see the database list

### Test MySQL Connection
```powershell
docker exec -it mysql mysql -u express_user -puserPassword123 -e "SHOW DATABASES;"
```

You should see the `express_db` database listed.

---

## 🛠️ Useful Commands

```powershell
# View all container status
docker-compose ps

# View logs from all containers
docker-compose logs -f

# View logs from specific container
docker-compose logs -f gitlab
docker-compose logs -f mysql

# Stop all containers
docker-compose stop

# Stop and remove containers
docker-compose down

# Restart a specific container
docker-compose restart gitlab
```

---

## 📊 Current Project Structure

```
devops/
├── docker-compose.yml    # Container definitions
├── env.example           # Environment template
├── .env                  # Your environment variables (you create this)
├── .gitignore           # Git ignore rules
│
├── gitlab/              # GitLab volumes (created by docker)
│   ├── config/
│   ├── logs/
│   └── data/
│
├── runner/              # GitLab Runner volume
│   └── config/
│
├── mysql_data/          # MySQL database files
└── redis_data/          # Redis data files
```

---

## ⚠️ Troubleshooting

### Containers won't start
```powershell
# Check if ports are already in use
netstat -ano | findstr "8080"
netstat -ano | findstr "3306"

# Check Docker is running
docker ps
```

### GitLab is slow or won't load
- GitLab needs at least 4GB RAM
- It takes 2-3 minutes to fully start
- Check logs: `docker-compose logs -f gitlab`

### Can't connect to MySQL
- Make sure container is running: `docker-compose ps mysql`
- Check password in `.env` file matches
- Try: `docker-compose restart mysql`

---

## 🎯 Next Steps

Once all containers are running successfully, we'll move to:
- **Step 2**: Configure GitLab Runner
- **Step 3**: Import your Express.js repository
- **Step 4**: Set up CI/CD pipeline
- **Step 5**: Automate deployment

**But first, make sure Step 1 is working perfectly! 🚀**

---

## 📝 Notes

- All data is stored in local volumes
- Containers will restart automatically if they crash
- You can stop/start containers without losing data
- To completely reset, delete the volume folders and run `docker-compose up -d` again
