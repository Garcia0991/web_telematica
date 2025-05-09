# Despliegue Automático de Aplicación Web con Jenkins, Docker y GitHub

Este proyecto demuestra un flujo de trabajo de **Desarrollo Continuo (CI)** donde una aplicación web se despliega automáticamente en una máquina Linux (local o EC2) utilizando **Jenkins**, **Docker** y un repositorio en **GitHub**.

---

## 📦 Tecnologías utilizadas

- Jenkins
- Docker
- GitHub
- Ngrok (para exponer Jenkins públicamente)
- Ubuntu (máquina local o EC2)

---

## 🚀 Pasos para desplegar el servicio

### 1. Clonar el repositorio

```bash
git clone https://github.com/Garcia0991/web_telematica.git
cd web_telematica
##Crea un archivo llamado Dockerfile con el siguiente contenido:
FROM nginx:alpine
COPY . /usr/share/nginx/html
##Crea un archivo llamado deploy.sh:
#!/bin/bash
echo "Construyendo imagen Docker..."
docker build -t webtelematica .

echo "Eliminando contenedor anterior (si existe)..."
docker stop webtelematica || true
docker rm webtelematica || true

echo "Desplegando nuevo contenedor..."
docker run -d -p 80:80 --name webtelematica webtelematica
##Dale permisos de ejecución:
chmod +x deploy.sh
## Configurar Jenkins
## Crear un nuevo trabajo (Freestyle project)
Fuente del código: Git

URL del repositorio: https://github.com/Garcia0991/web_telematica.git

## Configurar el Disparador
Habilitar la opción: GitHub hook trigger for GITScm polling
## Paso de construcción
## Agregar un paso de tipo "Ejecutar línea de comandos (shell)" con:
./deploy.sh
##Exponer Jenkins usando Ngrok
Desde la terminal: ngrok http 8080
## Configurar Webhook en GitHub
En GitHub:

Repositorio → Settings → Webhooks → Add webhook

Payload URL: https://TU_URL_NGROK/github-webhook/

## Hacer un Commit de prueba
git add .
git commit -m "Prueba de despliegue automático"
git push origin main

