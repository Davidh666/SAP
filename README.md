# SAP Lite ERP - Simulador Académico 🚀

Este proyecto es un simulador liviano de un sistema ERP basado en los flujos de negocio de **SAP**, modelando específicamente los módulos **MM (Materials Management - Gestión de Stock)** y **SD (Sales and Distribution - Ventas)**. Desarrollado con una arquitectura desacoplada moderna: Backend en **FastAPI** y Frontend en **React**.

---

## 📂 Estructura de Seguridad del Entorno (.env)

Por motivos de seguridad y buenas prácticas de desarrollo, el archivo de configuración del entorno se maneja de la siguiente manera:
* **`.env.example`** (Ubicado en la raíz): Plantilla pública de referencia técnica.

---

## 🛠️ Requisitos Previos

Antes de arrancar el sistema, asegúrate de tener instalado:
* Docker Desktop v4+
* Python 3.10+
* Node.js v18+

---

## 📦 Gestión e Instalación de Dependencias Local

Si vas a desarrollar o ejecutar los servidores de forma local (fuera de Docker), debes reconstruir los entornos de ejecución instalando sus respectivas dependencias y levantando los servicios:

## 🐍 Backend (FastAPI)
La carpeta `.venv` está excluida del repositorio por seguridad y peso. Para recrear tu entorno, instalar las librerías necesarias mediante el archivo `requirements.txt` y levantar el servidor, ejecuta:


### 1. Navega a la carpeta del backend
```bash
cd backend
```

### 2. Instala los paquetes requeridos usando el archivo de requisitos
```bash
pip install -r requirements.txt
```

### 3. Levanta el servidor de desarrollo (FastAPI)
```bash
fastapi dev main.py
```


## ⚛️ Frontend (React)


### 1. Navega a la carpeta del frontend
```bash
cd frontend
```
### 2. Instala los paquetes requeridos usando el archivo de requisitos
```bash
npm install
```
### 3. Levanta el servidor de desarrollo (FastAPI)
```bash
npm run dev
```

## 🛑 Flujo de Trabajo en Git (Reglas del Repositorio)


### 1. Actualiza tu rama local: Antes de crear una rama, asegúrate de tener la última versión estable de la nube:
```bash
git checkout main
```
```bash
git pull origin main
```
### 2. Crea y muévete a tu nueva rama feature/: El nombre de la rama debe describir brevemente lo que vas a programar (usa minúsculas separadas por guiones):
```bash
git checkout -b feature/nombre-de-tu-caracteristica
```
### 3. Trabaja en tu código y haz commits locales: Sube tus cambios que hiciste.
```bash
git add .
```
```bash
git commit -m "feat: descripción corta de lo que añadiste o arreglaste"
```
### 4. Sube tus cambios a la rama remota: Sube tus cambios a la rama remota. Asegurate de estar en la rama nueva que creaste.
```bash
git push origin feature/nombre-de-tu-caracteristica
```
### 5. Entra a git hub verifica que se subio a la nueva rama (para ver en que rama estas a un costado sale principal eso cambialo a tu rama que creaste) una vez estando ahi se te saldra un pull request ,  luego agrega el comentario y presiona enviar y listo
<br>


# 🚀 Crear y administrar contenedor con Docker Compose

## 🔑 Pasos iniciales

1. **Descargar el repositorio**  
   Ya incluye el archivo `docker-compose.yml`.

2. **Abrir la carpeta en Visual Studio Code**  
   - Abre el proyecto en VS Code.  
   - Verifica que el archivo `docker-compose.yml` esté en la raíz.

3. **Abrir la terminal integrada en VS Code**  
   - Menú: *Ver → Terminal*.  
   - Asegúrate de estar en la carpeta raíz del proyecto.

4. **Encender el contenedor**  
   Ejecuta:

```bash
   docker-compose up -d
```
5. **Comprobar el estado del contenedor**  
   Ejecuta:
```bash
   docker-compose ps
```
6. **Detener el contenedor**
   Ejecuta:
```bash
   docker-compose down
```
7. **Reiniciar el contenedor**
   Ejecuta:
```bash
   docker-compose restart

```


# ⚙️ Configuración del archivo .env

## 📂 Creacion
Crea el archivo `.env` en la raíz del proyecto,  copia todo los datos de .env.example y modifica los datos como el user, pasword y el url usando los datos que esta en el docker-compose.yml.


