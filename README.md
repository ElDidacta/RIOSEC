# RIOSEC — Infraestructura IT, Directorio Activo y SOC
<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/cfec051d-009a-4c91-bf58-cde2d8ea6f68" />


<p align="center">
  <b>Laboratorio de ingeniería en ciberseguridad defensiva y automatización de eventos de seguridad.</b>
</p>

---

## 📋 Resumen Ejecutivo
**RIOSEC** es un entorno de infraestructura híbrida diseñado para simular un Centro de Operaciones de Seguridad (SOC) corporativo de baja complejidad. El proyecto integra la administración centralizada de identidades, la recolección y análisis de telemetría mediante un SIEM y la orquestación de flujos de respuesta automatizados para la notificación de incidentes en tiempo real.

---

## 🏛️ Arquitectura y Componentes
* **Servicios de Directorio:** Implementación de un Controlador de Dominio bajo Windows Server 2022 (`riosec.local`), estructurado con Unidades Organizativas (OUs) y políticas de grupo (GPO) para el control de acceso y endurecimiento de endpoints.
* **Monitoreo y SIEM:** Despliegue centralizado del stack de **Wazuh** sobre un nodo Linux (Debian), encargado del enrolamiento de agentes corporativos, análisis de integridad de ficheros (FIM) y evaluación de seguridad.
* **Automatización y Respuesta:** Interconexión mediante scripts de Python y flujos orquestados en **n8n** para la extracción de métricas de la API de Wazuh y su posterior canalización hacia notificaciones operativas en Telegram.

---

## 📂 Estructura de la Documentación
Toda la ingeniería, diseño de redes y especificaciones técnicas del laboratorio se encuentran detalladas en la carpeta [`documentos/`](docs/):
* `01-resumen-ejecutivo.md` — Visión general y alcance del proyecto.
* `02-arquitectura-general.md` — Topología física y esquemas lógicos.
* `03-active-directory.md` — Gestión de identidades, OUs y directivas de grupo.
* `04-inventario-de-activos.md` — Recursos de hardware, virtualización y matriz de red.
* `05-monitoreo-wazuh.md` — Configuración del SIEM y recolección de eventos.
* `06-automatizacion-alertas.md` — Integración de API, Python y orquestación.
* `07-casos-de-prueba.md` — Escenarios de validación controlada.
* `08-analisis-de-incidentes.md` — Metodología de análisis y triage.
* `09-instalacion-y-operacion.md` — Guía de despliegue y buenas prácticas.
