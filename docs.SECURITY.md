---

### 2. `docker-compose.yml`
*(Click **"Add file"** → **"Create new file"**, name it `docker-compose.yml`, and paste this).*

```yaml
version: '3.8'

services:
  n8n:
    image: docker.n8n.io/n8nio/n8n:latest
    container_name: omnera_n8n
    restart: unless-stopped
    ports:
      - "5678:5678"
    environment:
      - N8N_HOST=${N8N_HOST:-localhost}
      - N8N_PORT=5678
      - N8N_PROTOCOL=http
      - WEBHOOK_URL=http://${N8N_HOST:-localhost}:5678/
      - GENERIC_TIMEZONE=Asia/Kolkata
    volumes:
      - n8n_data:/home/node/.n8n
    networks:
      - omnera_network
    depends_on:
      - poster-service

  poster-service:
    build:
      context: ./facebook-poster
      dockerfile: Dockerfile
    container_name: omnera_poster_service
    restart: unless-stopped
    ports:
      - "5000:5000"
    environment:
      - PORT=5000
      - PYTHONUNBUFFERED=1
    networks:
      - omnera_network

networks:
  omnera_network:
    driver: bridge

volumes:
  n8n_data:
