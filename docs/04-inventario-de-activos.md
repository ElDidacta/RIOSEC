# 04 — Inventario de Activos y Diseño de Red

## 📋 1. Inventario de Activos
El laboratorio RIOSEC se compone de recursos físicos y virtualizados interconectados para simular un entorno corporativo y de monitoreo de seguridad:

| Activo / Host | Sistema Operativo | Función en el Laboratorio | Estado de Implementación |
| :--- | :--- | :--- | :--- |
| **ThinkPad E15** | Windows (Host) | Anfitrión principal, ejecución del hipervisor VirtualBox. | Operativo |
| **HP Físico** | Debian Linux | Servidor de monitoreo SOC, backend de Wazuh y automatización. | Operativo |
| **Windows Server 2022** | Windows Server | Controlador de Dominio principal (`riosec.local`), DNS y Active Directory. | Operativo |
| **Windows 10** | Windows 10 | Estación de trabajo cliente integrada al dominio de laboratorio. | Operativo |
| **Linux Mint** | Linux | Entornos virtuales para pruebas controladas y validación de agentes. | Operativo |

---

## 🌐 2. Diseño y Segmentación de Red
- **Red Física (LAN Doméstica):** Utiliza un esquema de direccionamiento local gestionado por el router del entorno, interconectando la ThinkPad y el equipo HP mediante Ethernet/LAN.
- **Red Interna Virtual (`riosec-lan`):** Segmento virtualizado y aislado dentro de VirtualBox que permite la comunicación exclusiva y segura entre el Controlador de Dominio y el cliente Windows 10, evitando la exposición directa al exterior.

---

## 🔒 3. Matriz de Conectividad (Resumen)
- **Endpoints (Windows/Linux) ➔ Wazuh Manager (Debian):** Conexión cifrada a través de los puertos de agentes de Wazuh para el reporte de telemetría y eventos de seguridad.
- **Controlador de Dominio ➔ Cliente Windows 10:** Tráfico de autenticación Kerberos/LDAP y resolución de nombres mediante DNS interno de Active Directory.
