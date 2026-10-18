# 03 — Active Directory y Gestión de Identidades

## 🏢 1. Descripción del Dominio
El laboratorio implementa un servicio de directorio centralizado bajo el dominio lógico **`riosec.local`**, desplegado sobre una máquina virtual con **Windows Server 2022**. Este componente cumple el rol de Controlador de Dominio (Domain Controller), gestionando la autenticación de usuarios, la resolución de nombres (DNS) y la pertenencia de equipos a la red corporativa simulada.

---

## 📂 2. Estructura Lógica (Unidades Organizativas - OUs)
Para emular un entorno corporativo estructurado, se organizaron los objetos de Active Directory mediante Unidades Organizativas (OUs):
- **`riosec.local`**
  * `Usuarios/` — Contenedor para cuentas de usuario estándar y de prueba.
  * `Equipos/` — Contenedor para las estaciones de trabajo integradas al dominio.
  * `Departamentos/` — Segmentación lógica orientada a simular áreas de una organización.

---

## 💻 3. Integración de Estaciones de Trabajo
- **Cliente de Dominio:** Se integró exitosamente una máquina virtual con **Windows 10** al dominio `riosec.local`, validando la conectividad de red interna (`riosec-lan`) y la correcta resolución contra el Controlador de Dominio.
- **Pruebas de Autenticación:** Se realizaron inicios de sesión en el equipo cliente utilizando credenciales de cuentas de usuario creadas en el directorio activo.

---

## 📌 4. Gestión de Políticas y Evidencias de Configuración

### Evidencia AD-01 — Estructura de Unidades Organizativas (OUs)
* **Objetivo:** Documentar la organización jerárquica y lógica del dominio de laboratorio (`riosec.local`).
* **Procedimiento:** Apertura de la consola de *Usuarios y equipos de Active Directory* (`dsa.msc`) en Windows Server 2022.
* **Evidencia:** 
  *(Arrastrá acá la captura de las OUs de Active Directory)*
* **Resultado observado:** Se aprecia el despliegue de las unidades organizativas y la correcta asignación de cuentas de usuario en el directorio.

### Evidencia AD-02 — Aplicación de Directiva de Grupo (GPO)
* **Objetivo:** Documentar el endurecimiento (*hardening*) inicial del entorno mediante la restricción de configuraciones del sistema a los usuarios del dominio.
* **Procedimiento:** Configuración de una GPO (`Política_General`) desde el Editor de administración de directivas de grupo (`gpmc.msc`), aplicando la regla de prohibición de acceso al Panel de control y Configuración de PC.
* **Evidencia:** 
  <img width="1107" height="731" alt="Captura de pantalla 2026-10-16 004514" src="https://github.com/user-attachments/assets/c1c8ab61-9ed8-47a7-a6e7-48c50427d772" />

* **Resultado observado:** Se observa la directiva activa aplicada sobre los contenedores para restringir el cambio de parámetros del sistema operativo[cite: 25].
