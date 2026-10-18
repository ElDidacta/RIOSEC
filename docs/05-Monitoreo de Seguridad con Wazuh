# 05 — Monitoreo de Seguridad con Wazuh

<img src="assets/wazuh_loading.jpeg" alt="Panel de Monitoreo Wazuh - Carga" width="700">

## 🛡️ 1. Arquitectura del SIEM
Para la recolección, evaluación y análisis de eventos de seguridad, **RIOSEC** implementa el stack de **Wazuh** alojado de manera centralizada en el equipo físico con **Debian Linux**. 
- **Wazuh Manager:** Recibe las conexiones de los agentes, procesa los registros (*logs*) y ejecuta el motor de reglas de detección.
- **Wazuh Indexer & Dashboard:** Componentes encargados del almacenamiento indexado de los eventos y de proporcionar la interfaz web de visualización y consulta para el analista.

---

## 🔗 2. Enrolamiento y Estado de Agentes
Los equipos del laboratorio (tanto virtuales como físicos) se comunican con el servidor central mediante agentes instalados en cada sistema operativo, permitiendo un monitoreo en tiempo real desde el dashboard central (`192.168.1.11`):

<img src="assets/wazuh_agents_list.jpeg" alt="Listado de Agentes Enrolados en Wazuh" width="700">

- **Controlador de Dominio (`DC-Server2022` / `WIN-F80AKID3RA`):** Windows Server 2022 encargado de reportar eventos críticos del sistema, cambios de políticas y registros de autenticación corporativa.
- **Estación Cliente (`DESKTOP-DG4EGDT`):** Windows 10 monitorizado para detectar ejecuciones de procesos sospechosos, conexiones de red e intentos de inicio de sesión.
- **Entorno Linux (`LinuxMint-WS01`):** Integrado mediante Linux Mint para control de integridad de archivos (FIM) y auditoría de comandos del sistema operativo.

---

## 📊 3. Recorrido de los Eventos y Alertas
<img src="assets/alertas.jpeg" alt="Panel de Alertas Generadas en Wazuh" width="700">

1. **Generación:** El sistema operativo o aplicación genera un registro de evento (ej. Event Viewer en Windows o syslog en Linux).
2. **Captura y Envío:** El agente de Wazuh reenvía la telemetría cifrada hacia el Wazuh Manager en el servidor Debian.
3. **Análisis:** El motor evalúa el evento contra las reglas de seguridad predeterminadas o personalizadas, generando un nivel de severidad (*alert level*).
4. **Visualización y Automatización:** La alerta es indexada para su consulta en el Dashboard y enviada hacia las capas de automatización mediante la API de Wazuh.
