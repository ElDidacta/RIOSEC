# 06 — Automatización y Notificaciones de Alertas

## 🤖 1. Propósito de la Automatización
Para reducir el tiempo de respuesta ante incidentes y evitar la supervisión manual constante del Dashboard, **RIOSEC** incorpora un sistema de automatización que procesa las alertas generadas por el SIEM (Wazuh) y las transmite en tiempo real hacia canales de mensajería instantánea.

---

## 🐍 2. Servicio de Inventario de Agentes (Python & Flask)

* **Propósito del Servicio:** Este componente actúa como un servicio auxiliar en el ecosistema RIOSEC. Mientras que **n8n** gestiona de forma nativa la recepción de alertas de Wazuh y su envío a Telegram, este script en Python proporciona un inventario centralizado de los hosts del laboratorio.
* **Procesamiento Local:** El servicio expone un endpoint centralizado (`/agentes`) que realiza lecturas optimizadas sobre la base de datos interna de Wazuh (`global.db`) mediante SQLite, entregando la lista de agentes registrados en formato JSON para el consumo del flujo de automatización.

## 📄 Código Fuente del Servicio (`riosec_api.py`):

```python
import sqlite3
from flask import Flask, jsonify

app = Flask(__name__)

@app.route("/agentes", methods=["GET"])
def obtener_agentes():
    db_path = "/var/ossec/queue/db/global.db"
    agentes_lista = []

    try:
        conn = sqlite3.connect(db_path)
        cursor = conn.cursor()

        # Consultamos únicamente ID y nombre que sabemos que existen seguros
        cursor.execute("SELECT id, name FROM agent")
        agentes = cursor.fetchall()

        for a in agentes:
            agentes_lista.append({
                "id": a[0],
                "name": a[1] or "N/A",
                "status": "active",  # Valor por defecto estandarizado para el laboratorio
            })

        conn.close()
        return jsonify({"status": "success", "agents": agentes_lista})

    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

## ⚡ 3. Orquestación con n8n
* **Flujo Sanitizado:** Se implementa un flujo de trabajo en **n8n** (exportado de forma segura en `n8n/riosec-alert-workflow-sanitized.json` sin credenciales sensibles).
* **Comportamiento del Flujo:** El orquestador recibe el evento procesado, formatea la estructura del mensaje de seguridad y lo canaliza de forma automatizada.

<img src="Captura de pantalla 2026-10-18 022326.png" alt="Flujo de Trabajo Logístico y Orquestación en n8n" width="600">

---
## 📲 4. Entrega de Alertas en Tiempo Real (Telegram)

* **Notificaciones Operativas:** El nodo final del flujo de n8n se comunica con la API del Bot de Telegram para enviar notificaciones inmediatas al analista.
* **Resultado:** Cada vez que Wazuh detecta un evento anómalo que cumple con los umbrales definidos, el sistema emite una alerta directa al dispositivo móvil con el contexto técnico del incidente.

### Evidencias de la Notificación

<p align="center">
  <img src="Captura de pantalla 2026-10-18 032427.png" alt="Alerta de Seguridad Recibida en Telegram" width="350">
  <br>
  <em>Figura 4.1: Notificación de alerta recibida en el dispositivo móvil.</em>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/4036fa6c-f39e-4c5f-835c-9ce7bd47a5c1" alt="Flujo de Notificación en n8n" width="700">
  <br>
  <em>Figura 4.2: Configuración del flujo de automatización y envío en n8n.</em>
</p>

