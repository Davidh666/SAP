# SAP Lite ERP - Simulador Académico
---
## 🎨 Especificaciones de Diseño para Figma (Prototipo Estático)

Para garantizar la consistencia visual del prototipo, todo el equipo debe trabajar bajo las mismas dimensiones, estructura de grilla y paleta de colores. El diseño está inspirado en la interfaz moderna **SAP Fiori**.

---

### 📐 Dimensiones del Lienzo (Frame)
* **Tamaño Único de Pantalla:** Desktop `1440 px` (Ancho) × `1024 px` (Alto).
* **Fondo General del Lienzo (`Canvas`):** `#F4F6F9` (Gris claro corporativo).

---

### 🧱 Estructura y Medidas de Componentes Fijos

#### 1. Barra Superior (Header)
* **Medidas:** `1440 px` de ancho × `80 px` de alto.
* **Posición:** Top `0`, Left `0` (Fijo en la parte superior).
* **Color de Fondo:** `#FFFFFF` (Blanco puro) con una línea de borde inferior de `1 px` de color `#E2E8F0`.
* **Elementos Internos:**
  * **Logo Corporativo:** Ubicado a la izquierda (dentro de los primeros `280 px`). Texto: `ERPSystem` en Negrita, tamaño `20 px`, color `#0A2540`.
  * **Barra de Búsqueda (`Buscar...`):** Rectángulo con esquinas redondeadas (`Corner Radius: 8 px`). Medidas sugeridas: `450 px` de ancho × `40 px` de alto. Color de fondo: `#EDF2F7`. Texto interno en gris `#A0AEC0`.
  * **Área de Usuario (Derecha):** Iconos de notificaciones `[🔔]`, configuración `[⚙️]` y el perfil de usuario a la derecha (`👤 D. Jesus`).

#### 2. Panel Lateral Izquierdo (Sidebar / Menú de Navegación)
* **Medidas:** `280 px` de ancho × `944 px` de alto (comienza justo debajo del Header, en Y: `80 px`).
* **Posición:** Top `80 px`, Left `0`.
* **Color de Fondo:** `#0A2540` (Azul Oscuro Corporativo).
* **Elementos Internos:**
  * **Texto de los Módulos:** Tamaño `16 px`, tipografía Regular/Medium. Color del texto inactivo: `#94A3B8` (Gris azulado).
  * **Estado Activo (Módulo seleccionado):** El módulo en el que se encuentra la pantalla actual debe llevar un fondo rectangular suave `#1E3A8A` detrás del texto o cambiar el texto a color `#FFFFFF` con un pequeño indicador al lado.

#### 3. Contenedor Central de Contenido (Main Content)
* **Medidas:** `1160 px` de ancho × `944 px` de alto.
* **Posición:** Top `80 px`, Left `280 px`.
* **Uso:** Aquí es donde cada integrante dibuja las tarjetas, tablas y gráficos estáticos de su vista correspondiente.

---

### 🎨 Paleta de Colores Oficial

| Elemento | Código HEX | Muestra Visual | Uso Principal |
| :--- | :--- | :--- | :--- |
| **Azul Corporativo** | `#0A2540` | 🟦 | Fondo del panel lateral e identidad de marca. |
| **Fondo General** | `#F4F6F9` | ⬜ | Fondo de la pantalla detrás de las tarjetas. |
| **Tarjetas / Header**| `#FFFFFF` | ⬜ | Rectángulos de módulos, tablas y barra superior. |
| **Texto Principal** | `#1A202C` | ⬛ | Títulos de tablas, nombres y datos macro. |
| **Texto Secundario**| `#718096` | 🟫 | Subtítulos, marcadores de posición (placeholders). |
| **Éxito / IA Activa** | `#48BB78` | 🟩 | Alertas positivas de IA, etiquetas "Stock Alto". |
| **Alerta / Crítico** | `#E53E3E` | 🟥 | Alertas de fraude, etiquetas "Stock Crítico". |

---

### ⚙️ Instrucciones para el Equipo
1. **No alterar el tamaño del Frame (`1440x1024`).**
2. Se recomienda que el **Integrante 2 (UI Principal)** cree el Header y el Sidebar como un **Componente Maestro** en Figma y lo comparta con los demás para que la barra de búsqueda, el logo y el menú lateral midan exactamente lo mismo en las 5 pantallas.