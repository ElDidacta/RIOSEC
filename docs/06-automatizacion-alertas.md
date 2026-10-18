# 06 — Automatización y Notificaciones de Alertas

## 🤖 1. Propósito de la Automatización
Para reducir el tiempo de respuesta ante incidentes y evitar la supervisión manual constante del Dashboard, **RIOSEC** incorpora un sistema de automatización que procesa las alertas generadas por el SIEM (Wazuh) y las transmite en tiempo real hacia canales de mensajería instantánea.

---

## 🐍 2. Integración con la API de Wazuh (Python)
* **Consulta de Alertas:** Se desarrollan scripts en **Python** ubicados en la ruta de código del proyecto para interactuar directamente con la API REST de Wazuh.
* **Procesamiento:** Los scripts realizan consultas programadas o mediante webhooks para filtrar eventos según su nivel de severidad y extraer los campos críticos (origen, regla activada, usuario y host afectado).

---

## ⚡ 3. Orquestación con n8n
* **Flujo Sanitizado:** Se implementa un flujo de trabajo en **n8n** (exportado de forma segura en `n8n/riosec-alert-workflow-sanitized.json` sin credenciales sensibles).
* **Comportamiento del Flujo:** El orquestador recibe el evento procesado, formatea la estructura del mensaje de seguridad y lo canaliza de forma automatizada.

---

## 📲 4. Entrega de Alertas en Tiempo Real (Telegram)
* **Notificaciones Operativas:** El nodo final del flujo de n8n se comunica con la API de Bot de Telegram para enviar notificaciones inmediatas al analista.
* **Resultado:** Cada vez que Wazuh detecta un evento anómalo que cumple con los umbrales definidos, el sistema emite una alerta directa al dispositivo móvil con el contexto técnico del incidente.
