SAP_Lite_ERP/
│
├── README.md                          # Documentación para la defensa de clase
├── docker-compose.yml                 # Levanta Postgres 16 simulando las tablas ERP
├── .gitignore                         # Exclusiones de control de versiones
│
├── docs/                              # Sustento de la exposición
│   ├── arquitectura_sap.md            # Diagrama del flujo de datos del ERP
│   └── especificacion_modulos.md      # Explicación de los módulos simulados
│
├── backend/                           # Capa Servidor (FastAPI + SQLAlchemy)
│   ├── main.py                        # Inicialización del Servidor API SAP-Lite
│   ├── requirements.txt               # Dependencias del servidor Python
│   ├── .env.example                   # Variables de entorno locales
│   └── app/
│       ├── api/                       # Endpoints que simulan llamadas a SAP (BAPIs)
│       │   ├── auth.py                # Control de acceso de empleados (JWT)
│       │   ├── clientes.py            # Módulo SD: Registro y Datos Maestros de Clientes
│       │   ├── inventario.py          # Módulo MM: Gestión de Stock y Materiales
│       │   ├── deps.py                # Inyectores de sesiones de base de datos
│       │   └── ventas.py              # Módulo SD: Creación de Órdenes de Venta
│       ├── core/                      # Seguridad y Criptografía corporativa
│       │   └── security.py            # Hashing de contraseñas de operarios
│       ├── db/                        # Conexión local a la base de datos
│       │   └── database.py            # Configuración del Engine de SQLAlchemy
│       ├── models/                    # Modelos ORM (Mapeo a tablas estándar SAP)
│       │   ├── main_models.py         # Tablas de negocio (Ordenes, Facturas, Stock)
│       │   └── usuarios.py            # Tabla de empleados y roles del ERP
│       ├── repositories/              # Consultas SQL optimizadas (Simulando ABAP OpenSQL)
│       │   ├── inventario_repo.py     # Lógica directa sobre la tabla de Materiales
│       │   └── ventas_repo.py         # Lógica directa sobre la tabla de Órdenes
│       ├── schemas/                   # Esquemas Pydantic (Validación de carga útil)
│       │   ├── cliente_schema.py      # Estructura obligatoria del cliente
│       │   ├── material_schema.py     # Estructura obligatoria del producto en stock
│       │   └── venta_schema.py        # Estructura del documento comercial
│       └── services/                  # Cerebro del ERP (Lógica de Negocio)
│           ├── inventario_service.py  # Verifica si hay stock disponible antes de vender
│           └── ventas_service.py      # Resta del stock y genera la factura contable
│
├── frontend/                          # Capa Cliente (React 19 + Vite 8)
│   ├── vite.config.js                 # Configuración y Proxy al Backend
│   ├── src/
│   │   ├── App.jsx                    # Enrutador de las transacciones del ERP
│   │   ├── AuthContext.jsx            # Gestión de sesión del empleado logueado
│   │   ├── components/                # Componentes visuales estilo SAP Fiori (Legos)
│   │   │   ├── MainLayout.jsx         # Panel lateral con el árbol de transacciones
│   │   │   ├── Navbar.jsx             # Barra superior con datos del centro de costo
│   │   │   └── StockAlertPanel.jsx    # Alerta visual de productos con bajo inventario
│   │   ├── pages/                     # Transacciones del ERP (Vistas de usuario)
│   │   │   ├── Login/                 # Pantalla de acceso al sistema SAP
│   │   │   ├── ModuloInventario/      # Transacción MM01: Control y visualización de Stock
│   │   │   ├── ModuloVentas/          # Transacción VA01: Crear Orden de Venta en vivo
│   │   │   └── DashboardCorporativo/  # Reportes gráficos de rendimiento del negocio
│   │   └── services/                  # Capa de peticiones HTTP (Axios / Fetch)
│   │       ├── inventarioService.js   # Comunicación con /api/inventario
│   │       └── ventasService.js       # Comunicación con /api/ventas
│
└── database/                          # Definición del esquema inicial en Postgres
    └── schema_init.sql                # Tablas base con datos semilla cargados