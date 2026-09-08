# Portafolio de QA Manual: Estrategia de Pruebas y Trazabilidad para Tablero de Tareas (Trello Clone)

## Descripción del Proyecto
Este repositorio contiene la documentación completa del ciclo de pruebas de software diseñado para validar el módulo de tarjetas de un tablero de tareas basado en Trello. El objetivo principal es demostrar un enfoque riguroso de ingeniería de calidad (QA) mediante la creación de artefactos de prueba estructurados, el análisis exhaustivo de requerimientos y la trazabilidad de punta a punta.

El alcance del proyecto abarca tres Historias de Usuario (Épica-gestión-de-tarjetas):
1. **HU-001:** Creación de Tarjetas (Camino feliz y restricciones de límites).
2. **HU-002:** Modificación de detalles (Edición rápida, autoguardado, atajos de teclado y descarte de edición).
3. **HU-003:** Archivado y Eliminación Definitiva (Flujos de persistencia, restauración y confirmaciones visuales).

---

## Herramientas Utilizadas
* **Documentación y Matrices:** Google Sheets / Google Docs / Microsoft Excel.
* **Gestión de Versiones:** Git & GitHub.
* **Técnicas de Caja Negra:** Partición de Equivalencia, Análisis de Valores Límite, Pruebas de Transición de Estados.
* **Testing de API & Automatización: Postman (Collection Runner, JavaScript Assertions, Environment Variables)
---

## Estructura del Repositorio
El proyecto está organizado de la siguiente manera para facilitar su revisión:

* **`00-Épica-gestión-de-tarjetas.pdf`:** Documento de especificación de requerimientos de negocio que detalla la Épica y las tres Historias de Usuario con sus respectivos Criterios de Aceptación. 
* **`01-Test-Plan.pdf`:** Plan de pruebas formal que define el alcance, estrategia, criterios de aceptación/rechazo y los entornos de prueba.
* **`02-Matriz-Trazabilidad.xlsx`:** Matriz que vincula cada escenario de negocio extraído de las Historias de Usuario con sus respectivos Casos de Prueba (TC), garantizando una cobertura del 100%.
* **`03-Casos-de-pruebas.xlsx`:** Set completo de Casos de Prueba detallados con precondiciones, pasos secuenciales, datos de prueba y resultados esperados.
* **`04-Reporte-de-defecto.xlsx`:** Plantilla formal de reporte de bug que detalla un defecto crítico encontrado en el flujo de autoguardado de la interfaz.

---

## Resumen Ejecutivo del Ciclo de Pruebas (Test Summary)
Durante la ejecución del ciclo de pruebas sobre la versión 1.0 del entorno de Testing (Windows 10 / Google Chrome), se obtuvieron las siguientes métricas de calidad:

* **Casos de Prueba Totales:** 35
* **Casos Ejecutados:** 35 (100%)
* **Casos Exitosos (Pass):** 34 (97.1%)
* **Casos Fallidos (Fail):** 1 (2.9%)
* **Bloqueos (Blocked):** 0

### Defectos Detectados
* **`04-Reporte-de-defecto/RD-001` (Severidad: Alta | Prioridad: Alta):** El título modificado de una tarjeta no se guarda automáticamente al perder el foco (hacer clic fuera del modal) o al cerrarlo con la "X", provocando la pérdida de la información editada. *Asociado al TC-007/HU-002*.

---

## Criterios de Diseño Destacados
* **Mapeo por Escenarios de Comportamiento:** La matriz de trazabilidad no se limita a listar criterios genéricos; agrupa los casos de prueba por escenarios específicos de la interfaz (como la combinación de mouse y atajos de teclado para la edición rápida), permitiendo una lectura fluida de la cobertura de pruebas.
* **Robustez en Edge Cases:** Se incluyeron validaciones críticas de entrada de datos (campos vacíos, inyección de espacios en blanco, caracteres especiales) para asegurar la integridad de la base de datos y la estabilidad de la UI.

