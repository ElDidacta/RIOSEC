# 09 — Instalación, Operación y Mantenimiento

## 🛠️ 1. Requisitos y Dependencias
* **Infraestructura Requerida:** 
  * Host con hipervisor VirtualBox (mínimo 16 GB de RAM recomendados para soportar las VMs de Active Directory y estaciones cliente).
  * Equipo dedicado o servidor local con distribución Linux (Debian) para el despliegue del stack de Wazuh.
* **Dependencias de Software:**
  * Python 3.x para los scripts de integración con la API del SIEM.
  * n8n para la orquestación y reenvío de flujos de eventos.

---

## 🚀 2. Guía de Puesta en Marcha
1. **Despliegue de Redes Virtuales:** Configurar la red interna `riosec-lan` en VirtualBox para aislar de forma segura el Controlador de Dominio y los clientes.
2. **Inicialización del Directorio Activo:** Levantar la máquina virtual con Windows Server 2022, promover el rol de Active Directory y configurar el dominio corporativo `riosec.local`.
3. **Instalación del SIEM:** Desplegar Wazuh Manager, Indexer y Dashboard en el servidor Debian, asegurando la conectividad de red con los endpoints.
4. **Enrolamiento de Agentes:** Instalar y registrar los agentes de Wazuh en los equipos Windows y Linux mediante las claves de autenticación del manager.
5. **Activación de Automatizaciones:** Cargar el flujo sanitizado en n8n (`n8n/riosec-alert-workflow-sanitized.json`) y configurar las credenciales del bot de Telegram de forma segura mediante variables de entorno.

---

## 🔒 3. Buenas Prácticas de Seguridad Operativa
* **Gestión de Secretos:** Nunca incluir tokens de API, contraseñas de cuentas de dominio, claves privadas de SSH o tokens de Telegram en texto plano dentro del código fuente. Utilizar siempre archivos de configuración locales excluidos mediante `.gitignore`.
* **Control de Puertos:** Mantener los servicios de administración expuestos únicamente dentro de la red interna o protegidos mediante reglas estrictas de firewall.
