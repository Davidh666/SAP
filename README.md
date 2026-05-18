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

## 🐳 Despliegue de la Base de Datos con Docker

Para levantar el contenedor de la base de datos relacional (PostgreSQL 16) que simulará las tablas estándar de datos maestros de SAP, sigue estos pasos desde tu terminal de PowerShell:

### 1. Iniciar el contenedor de Docker
Ejecuta el siguiente comando en la raíz del proyecto para descargar la imagen y levantar el servicio en segundo plano:
```bash
docker compose up -d