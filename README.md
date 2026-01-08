# Reporte Semanal de Sucursales – n8n

## Descripción general

Este proyecto corresponde a **mi primer proyecto desarrollado en n8n**.  
Es una automatización simple pero funcional cuyo objetivo es **analizar reportes semanales de sucursales** cargados en Google Sheets y **enviar un resumen automático por email** utilizando un agente de IA.

Al tratarse de mi **primer workflow**, la solución es **básica**, con lógica lineal y **sin optimizaciones avanzadas**, pero cumple correctamente su propósito y sirvió como punto de partida para entender la orquestación, automatización y uso de IA dentro de n8n.

![Workflow WhatsApp Bot](.png)
---

## Objetivo del workflow

- Ejecutarse automáticamente una vez por semana.
- Leer datos operativos de sucursales desde Google Sheets.
- Analizar la información de los últimos 7 días.
- Detectar problemas recurrentes.
- Generar un resumen ejecutivo con sugerencias de mejora usando IA.
- Enviar el reporte por correo electrónico a supervisores.

---

## Tecnologías utilizadas

- **n8n** (orquestador de la automatización)
- **Google Sheets** (fuente de datos)
- **OpenAI (GPT-4.1-mini)** mediante LangChain
- **Gmail API** para envío de reportes
- **JavaScript (Code Node)** para normalización de datos

---

## Flujo general de la automatización

### 1. Disparador programado
- Nodo: `Schedule Trigger`
- Configuración:
  - Ejecución cada 7 días
  - Día: sábado
  - Hora: 21:00

Este nodo inicia automáticamente el proceso semanal.

---

### 2. Lectura de datos
- Nodo: `Google Sheets`
- Fuente:
  - Formulario de Google con reportes de sucursales
- Se leen todas las filas disponibles del sheet.

---

### 3. Normalización de información
- Nodo: `Code`
- Función:
  - Agrupa todos los registros en un único objeto (`allData`)
  - Evita múltiples salidas hacia el agente de IA

---

### 4. Análisis con IA
- Nodo: `AI Agent`
- Rol:
  - Supervisor de sucursales (“TAMARA”)
- Tareas:
  - Analizar los reportes de los últimos 7 días (campo `FECHA`)
  - Detectar problemas generales
  - Proponer mejoras operativas
  - Generar un único resumen consolidado
- Output:
  - Texto listo para enviar por email, con formato legible

---

### 5. Envío del reporte
- Nodo: `Gmail`
- Asunto:
  - `Reporte semanal de Supervisión`
- Destinatarios:
  - Múltiples correos de supervisión
- Contenido:
  - Resumen generado por la IA

---

## Limitaciones del proyecto

Al ser mi primer proyecto en n8n, presenta varias limitaciones claras:

- Lógica lineal y poco modular.
- Dependencia directa de un único Google Sheet.
- No hay validaciones avanzadas de datos.
- Manejo de errores casi inexistente.
- Prompt hardcodeado dentro del nodo.
- No hay control de versiones ni testing.
- Arquitectura no pensada para escalar.

---

## Qué sí aporta este proyecto

- Primer contacto real con:
  - Automatizaciones en n8n
  - Integración de IA en flujos productivos
  - Uso de cron jobs
  - Orquestación de datos + IA + email
- Base conceptual para proyectos más complejos posteriores.
- Validación de que n8n puede resolver tareas reales de negocio.

---

## Posibles mejoras futuras

- Modularizar el flujo en sub-workflows.
- Separar prompts y lógica de negocio.
- Agregar validaciones y control de errores.
- Implementar métricas y logs.
- Soportar múltiples sucursales o fuentes.
- Persistir históricos de reportes.
- Escalar el análisis con embeddings o clasificación automática.

---

## Estado actual

🟢 Funcional  
🟡 Básico  
🔵 Proyecto inicial / formativo  

---

**Autor:** Santiago Perez Kay  
**Contexto:** Primer proyecto desarrollado en n8n
