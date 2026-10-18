# 02 — Arquitectura General

## 🏛️ Descripción General del Laboratorio
El diseño de **RIOSEC** se divide en una capa física (hardware local interconectado mediante un router doméstico) y una capa virtualizada (hipervisor VirtualBox que aloja los servicios de directorio y las estaciones de trabajo). 

---

## 🔌 1. Topología Física
La infraestructura física consta de dos equipos principales conectados a la red local (LAN) bajo asignación por DHCP y conectividad IP directa:
* **ThinkPad E15 (Host Principal):** Sistema operativo anfitrión en Windows, encargado de correr el hipervisor VirtualBox y las máquinas virtuales del dominio y pruebas.
* **HP con Debian Linux (Servidor de Monitoreo):** Equipo dedicado a alojar el backend de seguridad, recolectando la telemetría y ejecutando los flujos de automatización.

<img width="612" height="437" alt="image" src="https://github.com/user-attachments/assets/f7965f6c-5bdd-4ff2-8a7e-17387c65d0ac" />

---

## 💻 2. Arquitectura Virtual y Redes (VirtualBox)
Dentro del entorno virtualizado de la ThinkPad, los componentes se distribuyen de la siguiente manera:
* **Red Interna (`riosec-lan`):** Segmento de red aislado donde operan de forma segura el Controlador de Dominio y el equipo cliente.
* **Controlador de Dominio:** Windows Server 2022 gestionando el directorio activo `riosec.local`.
* **Estación Cliente:** Windows 10 unido al dominio corporativo de laboratorio.
* **Estaciones de Pruebas:** Entornos basados en Linux para simulación de escenarios y validaciones de red.

---

## 📊 3. Diagrama de Flujo y Componentes
El siguiente diagrama detalla cómo viaja la telemetría desde los sistemas operativos operativos (Windows y Linux) hacia el Wazuh Manager alojado en el equipo Debian, pasando por los motores de automatización en Python y n8n hasta las alertas en tiempo real en Telegram:
<img width="2166" height="1790" alt="mermaid-diagram" src="https://github.com/user-attachments/assets/62efaf6b-fae0-4aad-9e10-b7ca19f96136" />

