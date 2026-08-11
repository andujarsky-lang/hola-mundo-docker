# 🐳 Hola Mundo Docker - CI/CD & Cloud Deployment

Una aplicación web minimalista desarrollada con Python y Flask, contenedorizada con Docker e integrada con un pipeline de CI/CD automatizado mediante GitHub Actions para su publicación en Docker Hub y despliegue automático en Render.

---

## 🎯 Objetivos del Proyecto

- **Contenedorización**: Embalar una aplicación web Python/Flask dentro de un contenedor Docker ligero, portátil y reproducible.
- **Automatización CI/CD**: Implementar un flujo de trabajo automatizado con GitHub Actions que se active con cada `push` a la rama `main`.
- **Registro de Imágenes**: Publicar imágenes Docker en Docker Hub de forma segura usando acciones oficiales (`docker/login-action` y `docker/build-push-action`).
- **Despliegue Continuo (CD)**: Notificar y desplegar la aplicación automáticamente en la nube (Render) tras cada actualización del código.

---

## 🛠️ Tecnologías Utilizadas

- **[Python 3.12](https://www.python.org/)**: Lenguaje de programación principal.
- **[Flask 3.1.3](https://flask.palletsprojects.com/)**: Microframework web ligero para Python.
- **[Docker](https://www.docker.com/)**: Plataforma de contenedorización para empaquetar la app y sus dependencias.
- **[GitHub Actions](https://github.com/features/actions)**: Sistema de integración y despliegue continuo (CI/CD).
- **[Docker Hub](https://hub.docker.com/)**: Registro en la nube para almacenar y gestionar imágenes de contenedores.
- **[Render](https://render.com/)**: Servicio Cloud para el alojamiento y despliegue automático de aplicaciones web.

---

## 💡 Lo que Aprendimos

1. **Creación y optimización de Dockerfiles**:
   - Uso de imágenes base ligeras (`python:3.12-slim`) para reducir el tamaño del contenedor.
   - Instalación eficiente de dependencias mediante `pip install --no-cache-dir`.
   - Mapeo y exposición de puertos (`EXPOSE 5000`).
2. **Construcción de Pipelines CI/CD en GitHub Actions**:
   - Configuración de disparadores por rama (`on: push: branches: [main]`).
   - Manejo seguro de credenciales mediante Secrets de GitHub (`DOCKERHUB_USERNAME`, `DOCKERHUB_TOKEN`, `RENDER_API_KEY`).
   - Estructuración de Jobs encadenados (`docker-login` $\rightarrow$ `build-and-push` $\rightarrow$ `deploy-render`).
3. **Despliegue Automático mediante Webhooks**:
   - Activación de despliegues en la nube usando solicitudes `cURL` tipo `POST` dirigidas al webhook de Render.

---

## 📁 Estructura del Proyecto

```text
hola-mundo-docker/
├── .github/
│   └── workflows/
│       └── deploy.yml          # Pipeline de CI/CD (GitHub Actions)
├── app.py                      # Código fuente de la aplicación Flask
├── Dockerfile                  # Instrucciones de construcción del contenedor
├── requirements.txt            # Dependencias del proyecto (Flask)
└── README.md                   # Documentación del proyecto
```

---

## 🚀 Cómo Descargar y Ejecutar Localmente

### Prerrequisitos

Asegúrate de tener instalados:
- [Git](https://git-scm.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (o Python 3.12 si deseas ejecutarlo localmente sin Docker)

### 1. Clonar el repositorio

```bash
git clone git@github.com:andujarsky-lang/hola-mundo-docker.git
cd hola-mundo-docker
```

### 2. Opción A: Ejecutar con Docker (Recomendado)

1. **Construir la imagen Docker**:
   ```bash
   docker build -t hola-mundo-docker .
   ```

2. **Ejecutar el contenedor**:
   ```bash
   docker run -d -p 5000:5000 --name app-hola-mundo hola-mundo-docker
   ```

3. **Probar la aplicación**:
   Abre tu navegador en `http://localhost:5000` para ver el mensaje de respuesta.

4. **Detener y limpiar el contenedor**:
   ```bash
   docker stop app-hola-mundo
   docker rm app-hola-mundo
   ```

### 3. Opción B: Ejecutar directamente con Python

1. **Crear y activar un entorno virtual**:
   ```bash
   python -m venv venv
   # En Windows PowerShell:
   .\venv\Scripts\activate
   # En Linux / macOS / WSL:
   source venv/bin/activate
   ```

2. **Instalar dependencias**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Ejecutar la aplicación**:
   ```bash
   python app.py
   ```

---

## ⚙️ Configuración de Secrets en GitHub

Para que el pipeline de GitHub Actions funcione sin errores al hacer `push` a `main`, debes configurar las siguientes variables en **Settings > Secrets and variables > Actions**:

- `DOCKERHUB_USERNAME`: Tu usuario de Docker Hub.
- `DOCKERHUB_TOKEN`: Tu Personal Access Token generado en Docker Hub.
- `RENDER_API_KEY`: URL del Webhook de despliegue (*Deploy Hook*) de Render.
