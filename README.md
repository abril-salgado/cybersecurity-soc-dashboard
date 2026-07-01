# SOC Cybersecurity Dashboard - Monitoreo de Amenazas 🛡️📊

Un tablero de Business Intelligence de nivel profesional desarrollado en Power BI para la centralización, análisis estructural y mitigación de incidentes de seguridad informática en tiempo real dentro de una infraestructura corporativa.

## 📌 Objetivos del Proyecto
* **Visibilidad Operativa:** Consolidar eventos de red para identificar patrones de ataque y vectores de amenaza.
* **Auditoría de Severidad (CVSS):** Clasificar y priorizar incidentes críticos según la escala estandarizada *Common Vulnerability Scoring System* (CVSS).
* **Control de SLAs:** Monitorear el porcentaje de resolución y mitigación (Tasa de Éxito) por parte de los analistas de seguridad del SOC.

## 📊 Vista Previa del Dashboard
*(Para subir tu imagen: una vez creado el repositorio, arrastrá tu captura de pantalla en esta línea para que se visualice la interfaz)*

---

## 🛠️ Aspectos Técnicos e Ingeniería de Datos

### 1. Extracción y Preparación (Power Query)
* **Ingeniería de Características:** Limpieza profunda de un dataset transaccional con más de 1,000 registros de logs simulados.
* **Tipado y Normalización:** Configuración estricta de formatos temporales para análisis cronológico, tipado numérico decimal para el índice CVSS y estructuración de variables categóricas.

### 2. Modelado de Datos (Arquitectura)
El proyecto implementa un enfoque de mejores prácticas mediante un **Modelo en Estrella (Star Schema)**. Esto optimiza el rendimiento de la memoria del motor y garantiza la velocidad de las consultas al separar las transacciones físicas (Hechos) de las tablas maestras de control (Dimensiones):
* `Fact_Incidentes` (Logs relacionales de ataques)
* `Dim_TiposAtaque` (Categorías y taxonomía de amenazas)
* `Dim_Calendario` (Estructura temporal para análisis de tendencias)

### 3. Fórmulas y Métricas Avanzadas (Lenguaje DAX)
Se desarrollaron medidas calculadas optimizadas para auditar el rendimiento del equipo:
* **Volumen General de Operaciones:** `Total_Incidentes = COUNT(logs_ciberseguridad[ID_Incidente])`
* **Aislamiento de Amenazas Críticas:** `Incidentes_Criticos = CALCULATE([Total_Incidentes], logs_ciberseguridad[Puntuacion_CVSS] >= 9.0)`
* **Métrica de Eficiencia de Mitigación (SLA):** `%_Mitigados = DIVIDE(CALCULATE([Total_Incidentes], logs_ciberseguridad[Estado] = "Mitigado"), [Total_Incidentes], 0)`

---

## 🚀 Cómo Explorar el Proyecto
1. Descarga el archivo `SOC_Dashboard.pbix` presente en este repositorio.
2. Ábrelo utilizando **Power BI Desktop** para auditar el modelo de datos, las relaciones jerárquicas, las fórmulas DAX implementadas y la interactividad completa de los filtros dinámicos.
