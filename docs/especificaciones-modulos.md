# 📋 Especificación del Sistema y Módulos - SAP-Lite ERP

Este documento detalla la arquitectura global, la especificación de módulos y el flujo de información del sistema **SAP-Lite**. Este ERP modular simula el comportamiento de transacciones estándar de SAP para la gestión corporativa, integrando una capa de servidor de alto rendimiento y una interfaz de usuario moderna e intuitiva.

---

## 🏗️ 1. Arquitectura General del Proyecto

El sistema está dividido en dos capas principales totalmente independientes que se comunican mediante una API RESTful, además de una infraestructura de base de datos contenedorizada:

1. **Backend (Capa Servidor):** Construido con **FastAPI** y **SQLAlchemy ORM**, implementando un patrón de *Arquitectura Limpia* (Clean Architecture) basado en capas de responsabilidad aisladas.
2. **Frontend (Capa Cliente):** Construido con **React 19** y **Vite 8**, estructurado por componentes modulares reutilizables y vistas de transacciones específicas que emulan el diseño limpio de **SAP Fiori**.
3. **Database (Capa de Datos):** Motor **PostgreSQL 15** corriendo de forma aislada en un contenedor de **Docker**, inicializado mediante scripts automatizados.

---

## 🐍 2. Especificación del Backend (`backend/`)

La lógica de la API de Python se organiza bajo un flujo de datos unidireccional y estricto para asegurar la mantenibilidad del código:
`Petición HTTP ➡️ API (Ruta) ➡️ Schema (Validación) ➡️ Service (Negocio) ➡️ Repository (SQL) ➡️ Model (BD)`

### 📁 Desglose de Carpetas y Responsabilidades:

* **`backend/main.py`**
    * **Función:** Punto de entrada del servidor FastAPI.
    * **Responsabilidad:** Inicializa la aplicación, configura los middlewares globales (como CORS para permitir conexiones desde el Frontend) e inyecta los enrutadores principales de la API.
* **`backend/app/api/` (Controladores y Endpoints)**
    * **Función:** Exponer los puntos de acceso de la API (BAPIs simuladas).
    * **Archivos:**
        * `auth.py`: Rutas para el inicio de sesión de empleados y renovación de credenciales.
        * `clientes.py`: Endpoints del módulo SD para consultar datos maestros y registrar clientes nuevos.
        * `inventario.py`: Endpoints del módulo MM para verificar niveles de stock y registrar entradas de mercancía.
        * `ventas.py`: Endpoints del módulo SD para procesar y listar órdenes de venta comerciales.
        * `deps.py`: Proveedor de dependencias inyectables (como las sesiones activas de la base de datos).
* **`backend/app/core/` (Seguridad Corporativa)**
    * **Función:** Administrar la criptografía y configuraciones globales del sistema.
    * **Archivos:**
        * `security.py`: Implementa algoritmos de hashing seguro (como Passlib/Bcrypt) para almacenar contraseñas de los operarios y la lógica de generación/verificación de tokens JWT.
* **`backend/app/db/` (Conectividad)**
    * **Función:** Administrar la persistencia de datos.
    * **Archivos:**
        * `database.py`: Declara el *Engine* de conexión hacia PostgreSQL utilizando variables de entorno y define la clase base `Base` para el mapeo relacional de objetos.
* **`backend/app/models/` (Modelos ORM - Estructura de Tablas)**
    * **Función:** Mapear los objetos de Python directamente a tablas relacionales de la base de datos.
    * **Archivos:**
        * `usuarios.py`: Estructura de la tabla de empleados (ID, legajo, contraseña hasheada, rol y centro de costo).
        * `main_models.py`: Estructura de las tablas de negocio (Clientes, Materiales en Stock, Órdenes de Venta e Ítems de Órdenes).
* **`backend/app/repositories/` (Capa de Persistencia Limpia)**
    * **Función:** Ejecutar consultas SQL directas y operaciones CRUD de forma aislada (Simulando ABAP OpenSQL).
    * **Archivos:**
        * `inventario_repo.py`: Consultas específicas para actualizar cantidades en almacén y leer códigos de materiales.
        * `ventas_repo.py`: Consultas complejas para guardar estructuras de documentos comerciales (cabecera y posición de ventas).
* **`backend/app/schemas/` (Validación de Datos con Pydantic)**
    * **Función:** Validar que los datos que entran y salen de la API tengan el formato corporativo obligatorio, impidiendo datos corruptos.
    * **Archivos:**
        * `cliente_schema.py`, `material_schema.py`, `venta_schema.py`: Reglas de tipos de datos, longitudes obligatorias y estructuras JSON de entrada/salida.
* **`backend/app/services/` (Cerebro del ERP - Lógica de Negocio)**
    * **Función:** Orquestar las reglas y validaciones complejas del negocio antes de impactar la base de datos.
    * **Archivos:**
        * `inventario_service.py`: Controla recepciones y auditorías de existencias.
        * `ventas_service.py`: **Regla Crítica:** Verifica la disponibilidad de stock en el almacén (módulo MM) antes de autorizar la creación de una factura contable y registrar una orden de venta (módulo SD). Si no hay existencias, bloquea la transacción y lanza una excepción.

---

## ⚛️ 3. Especificación del Frontend (`frontend/`)

El cliente está estructurado como una Single Page Application (SPA) optimizada, enfocada en la experiencia de usuario del operario de planta y del administrador comercial.

### 📁 Desglose de Carpetas y Responsabilidades:

* **`frontend/src/App.jsx`**
    * **Función:** Enrutador central del sistema.
    * **Responsabilidad:** Protege las rutas privadas (las transacciones del ERP) verificando que el usuario tenga un token válido. Si no está logueado, lo redirige al Login.
* **`frontend/src/AuthContext.jsx`**
    * **Función:** Manejo del estado global de autenticación.
    * **Responsabilidad:** Guarda en memoria el estado del empleado activo, su rol y los datos del Centro de Costo asignado, distribuyendo esta información a todas las pantallas de React.
* **`frontend/src/components/` (Componentes de Interfaz Estilo SAP Fiori)**
    * **Función:** Bloques visuales modulares reutilizables.
    * **Archivos:**
        * `MainLayout.jsx`: Contenedor principal del sistema que dibuja el panel lateral (Sidebar) con el menú o árbol de transacciones disponibles.
        * `Navbar.jsx`: Barra superior corporativa que muestra notificaciones del sistema y los datos del operario logueado.
        * `StockAlertPanel.jsx`: Widget interactivo que parpadea o muestra alertas visuales en tiempo real cuando un material crítico desciende de su stock mínimo de seguridad.
* **`frontend/src/pages/` (Vistas de Transacciones del ERP)**
    * **Función:** Pantallas completas con las que interactúa el usuario final.
    * **Archivos:**
        * `Login/`: Formulario de acceso con validación de credenciales corporativas.
        * `ModuloInventario/ (Simulación Transacción SAP MM01)`: Panel de control visual para examinar los materiales del almacén, buscar existencias por lote y registrar entradas de mercancía de proveedores.
        * `ModuloVentas/ (Simulación Transacción SAP VA01)`: Formulario dinámico interactivo para emitir órdenes de venta en tiempo real. Permite buscar clientes, añadir artículos al carrito y enviar los datos al Backend para procesar la venta.
        * `DashboardCorporativo/`: Vista gerencial con reportes e indicadores clave de rendimiento (KPIs) gráficos sobre ventas totales y movimientos de inventario del mes.
* **`frontend/src/services/` (Capa de Peticiones HTTP)**
    * **Función:** Centralizar todas las conexiones hacia el servidor Backend.
    * **Archivos:**
        * `inventarioService.js`: Funciones con `fetch`/`axios` para mandar peticiones a `/api/inventario`.
        * `ventasService.js`: Funciones para mandar peticiones a `/api/ventas` adjuntando automáticamente los encabezados de autorización JWT.

---

## 🗄️ 4. Infraestructura de Datos y Docker (`database/`)

* **`docker-compose.yml`**
    * **Responsabilidad:** Levanta el servidor de bases de datos PostgreSQL aislado de la máquina host, exponiendo el puerto estándar `5432` y persistiendo la información local en el volumen `postgres_data`.
* **`database/schema_init.sql`**
    * **Responsabilidad:** Contiene los scripts SQL puros de inicialización. Define la arquitectura de tablas relacionales originales, los campos obligatorios, las restricciones de llaves foráneas (`FOREIGN KEY`) y los inserts iniciales de prueba (maestros de artículos y usuarios semilla).

---

## 🔄 5. Flujo de una Transacción Ejemplo (Creación de Orden de Venta)

Para entender cómo interactúan los componentes creados en todo el proyecto de extremo a extremo, este es el camino que sigue la información:

1. El operario ingresa a la página `ModuloVentas` (VA01) en el **Frontend**, selecciona un cliente y agrega un artículo.
2. Al hacer clic en "Confirmar Orden", la vista llama a la función en `services/ventasService.js`.
3. El servicio dispara una petición HTTP `POST` hacia la ruta del **Backend** expuesta en `app/api/ventas.py`.
4. La API recibe el cuerpo de la petición y lo valida sintácticamente usando el esquema de `app/schemas/venta_schema.py`.
5. Si los tipos son correctos, se transfiere el control a `app/services/ventas_service.py`.
6. Este servicio realiza una llamada interna a `app/repositories/inventario_repo.py` para consultar si hay suficiente stock físico.
7. **Resultado Exitoso:** Si hay stock disponible, el servicio descuenta las unidades mediante el repositorio de inventario, registra la cabecera y posiciones de la orden a través de `app/repositories/ventas_repo.py` impactando los modelos en la Base de Datos, y finalmente retorna un código de éxito `201` al Frontend con el número de documento SAP generado.