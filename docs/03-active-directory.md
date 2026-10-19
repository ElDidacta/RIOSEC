# 03 — Active Directory y Gestión de Identidades

## 🏢 1. Descripción del Dominio
El laboratorio implementa un servicio de directorio centralizado bajo el dominio lógico **`riosec.local`**, desplegado sobre una máquina virtual con **Windows Server 2022**. Este componente cumple el rol de Controlador de Dominio (Domain Controller), gestionando la autenticación de usuarios, la resolución de nombres (DNS) y la pertenencia de equipos a la red corporativa simulada.

---

## 📂 2. Estructura Lógica (Unidades Organizativas - OUs)
Para emular un entorno corporativo estructurado, se organizaron los objetos de Active Directory mediante Unidades Organizativas (OUs):
- **`riosec.local`**
  * **`Agro_y_Servicios/`** — Contenedor principal para las áreas operativas de negocio:
    * `Administracion/` — Gestión administrativa general.
      * `Gerencia/` — Subunidad para la dirección y alta gerencia.
    * `Agronomia/` — Operaciones técnicas agropecuarias.
    * `Agroquimicos/` — Control y manejo de insumos químicos.
    * `Carniceria/` — Unidad de negocio cárnico.
    * `Freteria/` — Gestión del área de ferretería.
    * `Forrajeria/` — Operaciones de forrajes.
    * **`Departamento IT/`** — Segmentación lógica orientada a la gestión técnica:
      * `Ciberseguridad/` — Recursos y controles de seguridad defensiva.
      * `Infraestructura/` — Administración de servidores y red.
      * `Soporte/` — Asistencia a usuarios y resolución de incidencias.
    * `Supermercado/` — Unidad de gestión comercial minorista.
    * `Verduleria/` — Operaciones del sector verdulería.
    * `Veterinaria/` — Área de servicios veterinarios.
    * `YPF/` — Sector de estación de servicios y combustibles.

---

## 💻 3. Integración de Estaciones de Trabajo
- **Cliente de Dominio:** Se integró exitosamente una máquina virtual con **Windows 10** al dominio `riosec.local`, validando la conectividad de red interna (`riosec-lan`) y la correcta resolución contra el Controlador de Dominio.
- **Pruebas de Autenticación:** Se realizaron inicios de sesión en el equipo cliente utilizando credenciales de cuentas de usuario creadas en el directorio activo.

---

## 📌 4. Gestión de Políticas y Evidencias de Configuración

### Evidencia AD-01 — Estructura de Unidades Organizativas (OUs)
- **Objetivo:** Documentar la organización jerárquica y lógica del dominio de laboratorio (`riosec.local`).
- **Procedimiento:** Apertura de la consola de *Usuarios y equipos de Active Directory* (`dsa.msc`) en Windows Server 2022.
- **Evidencia:**

  <img width="845" height="621" alt="Captura de pantalla de OUs" src="[https://github.com/user-attachments/assets/05dcffe4-890c-41a6-b11b-d2680c3d07cd](https://github.com/user-attachments/assets/05dcffe4-890c-41a6-b11b-d2680c3d07cd)" />

- **Resultado observado:** Se aprecia el despliegue detallado de las unidades organizativas y la jerarquía de subunidades por áreas de negocio e infraestructura técnica en el directorio.

### Evidencia AD-02 — Aplicación de Directiva de Grupo (GPO)
- **Objetivo:** Documentar el endurecimiento (*hardening*) inicial del entorno mediante la restricción de configuraciones del sistema a los usuarios del dominio.
- **Procedimiento:** Configuración de una GPO (`Política_General`) desde el Editor de administración de directivas de grupo (`gpmc.msc`), aplicando la regla de prohibición de acceso al Panel de control y Configuración de PC.
- **Evidencia:** 

  <img width="826" height="672" alt="image GPO" src="[https://github.com/user-attachments/assets/564fe7ea-b6ee-4018-9ced-8040a79a4c47](https://github.com/user-attachments/assets/564fe7ea-b6ee-4018-9ced-8040a79a4c47)" />

- **Resultado observado:** Se observa la directiva activa aplicada sobre los contenedores para restringir el cambio de parámetros del sistema operativo.

### Evidencia AD-03 — Auditoría de Puertos y Servicios de Red (Nmap)
- **Objetivo:** Identificar y documentar los puertos y servicios expuestos en el Controlador de Dominio (`192.168.1.13`) mediante un escaneo de enumeración de red.
- **Procedimiento:** Ejecución de escaneo avanzado de puertos y detección de versiones con Nmap desde la máquina de auditoría Debian:

      nmap -sC -sV -Pn --open 192.168.1.13  <--- la IP de Windwos Server 2022

- **Evidencia:**

---

<img width="1920" height="1053" alt="imagen" src="https://github.com/user-attachments/assets/1e16b41b-ac6b-4988-8f28-4366d6362b4b" />


**Resultado observado:** El escaneo confirma la correcta exposición y estado operativo de los puertos y servicios esenciales del Controlador de Dominio:
  - **`21/tcp` (FTP):** Servicio *Microsoft ftpd* con soporte de acceso anónimo habilitado (`anonymous`).
  - **`53/tcp` (DNS):** Servicio *Simple DNS Plus* para la resolución de nombres en el dominio `riosec.local`.
  - **`80/tcp` (HTTP):** Servidor web *Microsoft IIS httpd 10.0*.
  - **`88/tcp` (Kerberos):** Servicio *Microsoft Windows Kerberos* para la autenticación centralizada (KDC).
  - **`135/tcp` (MSRPC):** Asignador de extremos de llamada a procedimiento remoto de Windows.
  - **`139/tcp` y `445/tcp` (NetBIOS / SMB):** Servicios de compartición de archivos y recursos de red, con la firma SMB requerida y habilitada por seguridad.
  - **`389/tcp` y `636/tcp` (LDAP / LDAPS):** Protocolo de acceso al directorio activo de Windows.
  - **`464/tcp` (kpasswd5):** Servicio para el cambio y actualización de contraseñas de Kerberos.
  - **`593/tcp` (ncacn_http):** RPC sobre protocolo HTTP.
  - **`3268/tcp` y `3269/tcp` (Global Catalog):** Catálogo global de Active Directory para búsquedas en todo el bosque.
  - **`5985/tcp` (WinRM):** Interfaz *Microsoft HTTPAPI httpd 2.0* para la administración remota mediante PowerShell.

### Evidencia AD-04 — Verificación de Servicios Críticos en Ejecución (Windows Server 2022)
- **Objetivo:** Validar localmente en el servidor que los servicios fundamentales del Controlador de Dominio y de red se encuentran activos (`Running`).
- **Procedimiento:** Consulta de servicios mediante PowerShell en el Windows Server 2022.
- **Evidencia:**
---

<img width="922" height="632" alt="Captura de pantalla 2026-10-18 233143" src="https://github.com/user-attachments/assets/9bf6a2c9-cfdb-42c7-bf29-2d6cc0bdc775" />

---
<img width="947" height="682" alt="Captura de pantalla 2026-10-18 233242" src="https://github.com/user-attachments/assets/98d91dd2-46cf-4695-a6fd-9fb614c6f228" />

---
<img width="957" height="682" alt="Captura de pantalla 2026-10-18 233306" src="https://github.com/user-attachments/assets/dc18257e-6a59-4f6d-9610-445837746043" />

---
  

- **Resultado observado:** Se confirma la correcta ejecución de los servicios esenciales del ecosistema en el servidor:
  - **`NTDS`:** Servicios de dominio de Active Directory.
  - **`DNS`:** Servidor de resolución de nombres.
  - **`Kdc`:** Centro de distribución de claves Kerberos.
  - **`LanmanServer`:** Servicio de compartición de archivos y recursos mediante SMB.
  - **`ftpsvc`:** Servicio FTP de Microsoft.
  - **`WinRM`:** Administración remota de Windows.
  - **`WazuhSvc`:** Agente de monitoreo y seguridad integrado en la infraestructura.
  
