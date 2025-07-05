# 🧰 My Daily Docker Toolbox

This repository is a personal collection of Dockerized tools that I use day-to-day for network utilities, testing, visualization, and self-hosted services. I'm making it public to help others who might find these tools useful in their own setups.

Each folder contains the Docker setup (Dockerfile or `docker-compose.yml`) needed to deploy the service quickly and reliably.

---

## 📁 Folder Descriptions

### `Grafana/`
Dashboard and visualization platform. Useful for graphing system metrics or integrating with Prometheus and other monitoring sources.

### `InternetTesting/`
Tools and scripts to test internet quality including speed, latency, and jitter. Great for checking connectivity and logging performance.

### `cloudflareTunnal/`
Configuration for setting up Cloudflare Tunnel (Argo Tunnel), which allows secure exposure of local services to the web without opening firewall ports.

### `it-tools/`
Self-hosted collection of browser-based tools for developers and network engineers. Includes encoders/decoders, ping, dig, and more.

### `nginxProxyManager/`
Web-based GUI to manage Nginx as a reverse proxy. Supports free Let's Encrypt SSL and is ideal for exposing local services securely.

### `pihole/`
Ad-blocking DNS server to improve privacy and reduce bandwidth usage on a local network.

### `rancher/`
Container management platform that simplifies deploying and managing Docker or Kubernetes environments.

### `uptimeKuma/`
Beautiful, self-hosted status page that monitors uptime of websites and services. Can notify via Telegram, Discord, email, and more.

---

## 🚀 Getting Started

1. **Clone the Repository**
   ```bash
   git clone https://github.com/Billy004/internet-monitoring.git
   cd internet-monitoring
