# 01 — Resumen Ejecutivo

## 📋 ¿Qué es RIOSEC?
**RIOSEC** es un proyecto de laboratorio de infraestructura y ciberseguridad defensiva diseñado para emular un Centro de Operaciones de Seguridad (SOC) y un entorno corporativo centralizado de baja complejidad. Su propósito principal es consolidar habilidades prácticas en administración de sistemas, despliegue de identidades, monitoreo de eventos de seguridad (SIEM) y automatización de flujos de notificación.

## 🎯 Problema de Aprendizaje y Enfoque
El laboratorio aborda el desafío de integrar tecnologías heterogéneas (sistemas operativos Windows y Linux, virtualización e interfaces de programación de aplicaciones) bajo una arquitectura cohesiva. En lugar de configuraciones aisladas, RIOSEC conecta la telemetría de los sistemas operativos directamente con una plataforma de análisis centralizada.

## 🚀 Estado Actual de Implementación
- **Infraestructura Virtual y Redes:** Despliegue de hipervisor y máquinas virtuales interconectadas mediante topología de laboratorio.
- **Directorio Activo y Hardening:** Configuración lógica del dominio `riosec.local`, creación de Unidades Organizativas (OUs), gestión de usuarios/grupos de prueba, unión exitosa de un equipo cliente Windows 10 y aplicación de Directivas de Grupo (GPO) iniciales.
- **Monitoreo de Seguridad (SIEM):** Instalación y configuración de Wazuh (Manager e Indexer/Dashboard) con agentes enrolados para la recolección de eventos.
- **Automatización y Alertas:** Procesamiento de telemetría mediante scripts de Python y flujos en n8n integrados para notificaciones operativas.

## 📌 Limitaciones y Próximos Pasos Planificados
- **Ampliación de Políticas:** Evolución del despliegue de GPO hacia esquemas avanzados de seguridad corporativa y restricciones de ejecución de software.
- **Casos de Prueba Avanzados:** Expansión de escenarios controlados de simulación de amenazas para la afinación de reglas de detección en el SIEM.
