# Portafolio QA Trello: Estrategia de Pruebas y Trazabilidad para Tablero de Tareas (Trello Clone)

## Descripción del Proyecto

Este repositorio contiene la documentación completa del ciclo de pruebas de software diseñado para validar el módulo de tarjetas de un tablero de tareas basado en Trello. El objetivo principal es demostrar un enfoque riguroso de ingeniería de calidad (QA) mediante la creación de artefactos de prueba estructurados, el análisis exhaustivo de requerimientos y la trazabilidad de punta a punta.

El alcance del proyecto abarca tres Historias de Usuario principales (**Épica-gestión-de-tarjetas**):
* **HU-001:** Creación de Tarjetas (Camino feliz y restricciones de límites).
* **HU-002:** Modificación de detalles (Edición rápida, autoguardado, atajos de teclado y descartado de edición).
* **HU-003:** Archivado y Eliminación Definitiva (Flujos de persistencia, restauración y confirmaciones visuales).

Adicionalmente, el proyecto integra una suite de **Testing de API REST con Postman** para validar la capa de servicios e integración del sistema, asegurando que la lógica de negocio (reglas de validación, estados HTTP, persistencia y manejo de errores) se cumpla rigurosamente a nivel de backend.

---

## Herramientas Utilizadas

* **Documentación y Matrices:** Google Sheets / Google Docs / Microsoft Excel.
* **Gestión de Versiones:** Git & GitHub.
* **Técnicas de Caja Negra:** Partición de Equivalencia, Análisis de Valores Límite, Pruebas de Transición de Estados.
* **Testing de API & Automatización:** Postman (Collection Runner, JavaScript Assertions, Environment Variables).

---

## Estructura del Repositorio

El proyecto está organizado de la siguiente manera para facilitar su revisión:

* `00-Épica-gestión-de-tarjetas.pdf`: Documento de especificación de requisitos de negocio que detalla la Épica y las tres Historias de Usuario con sus respectivos Criterios de Aceptación.
* `01-Test-plan.pdf`: Plan de pruebas formales que define el alcance, estrategia, criterios de aceptación/rechazo y los entornos de prueba.
* `02-Matriz-de-trazabilidad.xlsx`: Matriz que vincula cada etapa de negocio extraída de las Historias de Usuario con sus respectivos Casos de Prueba (TC), garantizando una cobertura del 100%.
* `03-Casos-de-pruebas.xlsx`: Conjunto completo de Casos de Prueba detallados con precondiciones, pasos secuenciales, datos de prueba y resultados esperados.
* `04-Reporte-de-defecto.xlsx`: Plantilla formal de informe de error que detalla un defecto crítico encontrado en el flujo de autoguardado de la interfaz.
* `05-Postman-API-Tests/`: Colección exportada (`Trello-API-Testing.json`) y archivo de variables de entorno (`Trello-Environment.json`). Incluye pruebas de integración para endpoints de tarjetas y listas (POST, PUT, DELETE, GET), aserciones dinámicas y scripts de manejo de datos.

---

## Pruebas de API & Automatización (Postman)

Como complemento a las pruebas manuales de UI, se diseñó e implementó una colección en Postman (`05-Postman-API-Tests/`) para auditar los endpoints de la API v1 que soportan la gestión de tableros, listas y tarjetas.

### Alcance de las Pruebas de API
* **Operaciones CRUD:** Cobertura de solicitudes `POST`, `GET`, `PUT` y `DELETE` para el ciclo de vida completo de tarjetas y listas.
* **Validación de Criterios de Aceptación (Caja Negra):** Pruebas de límites y casos negativos para asegurar que la API reaccione adecuadamente ante entradas inválidas (ej. intentos de creación de tarjetas sin título o modificación de recursos inexistentes).
* **Verificación de Persistencia:** Comprobación del estado final de los recursos tras operaciones de archivado (`closed=true`) y eliminación definitiva.

### Aspectos Técnicos e Implementación
* **Aserciones Automáticas (JavaScript):** Cada request incluye scripts en la pestaña *Tests* para validar automáticamente:
  * Códigos de respuesta HTTP (`200 OK`, `400 Bad Request`, `404 Not Found`).
  * Estructura y esquema de la respuesta JSON (presencia de IDs, nombres de campos y tipos de datos correctos).
* **Gestión Dinámica de Variables:**
  * **Uso de Environment Variables (`Trello-Environment.json`):** Centralización de la `Url-Base`, la `Key` de API y el `Token` de autenticación para evitar la exposición de credenciales sensibles.
  * **Captura Dinámica de IDs:** Uso de `pm.environment.set()` en scripts *Post-response* para almacenar IDs generados en peticiones `POST` y reutilizarlos automáticamente en las solicitudes subsecuentes de modificación (`PUT`) y borrado (`DELETE`).
* **Ejecución de Suites:** Suite preparada para ejecución masiva en bloque mediante el **Collection Runner** de Postman y preparada para integración CI/CD con **Newman**.

---

## Resumen Ejecutivo del Ciclo de Pruebas

Durante la ejecución del ciclo de pruebas sobre la versión 1.0 del entorno de Testing (Windows 10 / Google Chrome), se obtuvieron las siguientes métricas de calidad:

| Capa de Pruebas | Casos Totales | Aprobados | Fallidos | % Éxito |
| :--- | :---: | :---: | :---: | :---: |
| **Manual (UI / Frontend)** | 35 | 34 | 1 | 97.1% |
| **API (Backend / Postman)** | 12 | 8 | 4 | 66.7% |
| **TOTAL COMBINADO** | **47** | **42** | **5** | **89.4%** |

### Defectos Detectados

* **`RD-001` (Severidad: Alta | Prioridad: Alta):** El título modificado de una tarjeta no se guarda automáticamente al perder el foco (hacer clic fuera del modal) o al cerrarlo con la "X", provocando la pérdida de la información editada. Asociado al `TC-007` / `HU-002`.
* **Fallos en Suite de API (4 Aserciones Fallidas):** Las pruebas negativas arrojaron incoherencias respecto a los criterios de aceptación esperados, destacando la falta de validación de entradas a nivel de backend (como permitir la creación de tarjetas sin título devolviendo `HTTP 200` en lugar de `HTTP 400`).

---

## Criterios de Diseño Destacados

* **Mapeo por Escenarios de Comportamiento:** La matriz de trazabilidad no se limita a listar criterios genéricos; agrupa los casos de prueba por escenarios específicos de la interfaz (como la combinación de mouse y atajos de teclado para la edición rápida), permitiendo una lectura fluida de la cobertura de pruebas.
* **Robustez en Edge Cases:** Se incluyen validaciones críticas de entrada de datos (campos vacíos, inyección de espacios en blanco, caracteres especiales) para asegurar la integridad de la base de datos y la estabilidad de la UI.

