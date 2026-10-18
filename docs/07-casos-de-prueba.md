# 07 — Casos de Prueba Controlados

## 🎯 1. Objetivo de las Pruebas
Validar que el entorno de infraestructura y monitoreo de **RIOSEC** reacciona correctamente ante eventos simulados de seguridad, verificando la generación de alertas en el SIEM y el flujo automatizado de notificaciones.

---

## 🧪 2. Escenario de Prueba 01 — Autenticación Fallida en Active Directory
* **Identificador:** `TEST-AD-01`
* **Objetivo:** Comprobar la detección de múltiples intentos de inicio de sesión fallidos contra el Controlador de Dominio (`riosec.local`).
* **Procedimiento:** Desde la estación de trabajo cliente o un entorno de pruebas, se ejecutan intentos deliberados de autenticación con credenciales inválidas contra un usuario del dominio.
* **Resultado Esperado:** Que el sistema operativo registre el evento de fallo de seguridad (ID de evento en Windows) y que Wazuh active una regla de severidad media/alta por fuerza bruta o credenciales incorrectas.
* **Resultado Observado:** El agente de Wazuh instalado en el servidor Active Directory capturó el evento y emitió la alerta correspondiente en el Dashboard, la cual fue procesada para su posterior notificación.
* **Conclusión:** La telemetría del directorio activo se integra correctamente con el motor de análisis de eventos.

---

## 🧪 3. Escenario de Prueba 02 — Control de Integridad de Archivos (FIM)
* **Identificador:** `TEST-FIM-02`
* **Objetivo:** Verificar la detección de modificaciones no autorizadas en archivos críticos del sistema operativo monitorizado.
* **Procedimiento:** Modificación controlada de un archivo dentro de una ruta protegida en el entorno Linux o Windows vigilado por el agente.
* **Resultado Esperado:** Alerta inmediata de Wazuh por cambio de hash o modificación de permisos (FIM - File Integrity Monitoring).
* **Resultado Observado:** El agente detectó la alteración del archivo en tiempo real y generó un registro de alerta detallando el cambio exacto.
* **Conclusión:** El monitoreo de integridad funciona de manera óptima para la detección temprana de modificaciones maliciosas.

---

<img width="1577" height="861" alt="alertas" src="https://github.com/user-attachments/assets/3cb3c0c6-dad9-4741-9f13-9c9f7a7e6fdd" />



