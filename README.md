# Web Telemática

Aplicación web simple desplegada con Docker y Jenkins.

## Cómo desplegar

```bash
docker build -t webtelematica .
docker run -d -p 80:80 webtelematica


---

### 🖼️ 5. Agregar una imagen
```bash
cd img
wget https://upload.wikimedia.org/wikipedia/commons/thumb/3/32/Logo_Telematica.png/320px-Logo_Telematica.png -O logo.png
cd ..
