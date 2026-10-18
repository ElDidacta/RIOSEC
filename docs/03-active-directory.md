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

  <img width="845" height="621" alt="Captura de pantalla de OUs" src="https://github.com/user-attachments/assets/05dcffe4-890c-41a6-b11b-d2680c3d07cd" />

- **Resultado observado:** Se aprecia el despliegue detallado de las unidades organizativas y la jerarquía de subunidades por áreas de negocio e infraestructura técnica en el directorio.

### Evidencia AD-02 — Aplicación de Directiva de Grupo (GPO)
- **Objetivo:** Documentar el endurecimiento (*hardening*) inicial del entorno mediante la restricción de configuraciones del sistema a los usuarios del dominio.
- **Procedimiento:** Configuración de una GPO (`Política_General`) desde el Editor de administración de directivas de grupo (`gpmc.msc`), aplicando la regla de prohibición de acceso al Panel de control y Configuración de PC.
- **Evidencia:** 

 <img width="826" height="672" alt="image GPO" src="https://github.com/user-attachments/assets/564fe7ea-b6ee-4018-9ced-8040a79a4c47" />

- **Resultado observado:** Se observa la directiva activa aplicada sobre los contenedores para restringir el cambio de parámetros del sistema operativo.
