# 08 — Análisis de Incidentes y Triage

## 🔍 1. Metodología de Análisis
Ante una alerta generada por el SIEM, **RIOSEC** adopta un enfoque estructurado de análisis (*triage*) para clasificar el evento y determinar si se trata de una actividad legítima, un falso positivo, una conducta sospechosa o un incidente confirmado.

---

## 📊 2. Diferenciación de Eventos
* **Alerta Operativa:** Registro generado por reglas estándar del sistema (ej. aperturas de sesiones comunes, tareas programadas legítimas).
* **Actividad Sospechosa:** Patrones anómalos que escapan al comportamiento habitual (ej. conexiones en horarios fuera de lo común, ejecuciones de comandos de reconocimiento desde estaciones de trabajo estándar).
* **Incidente Confirmado:** Evidencia concluyente de una brecha de seguridad, compromiso de credenciales o ejecución de código malicioso comprobada mediante telemetría cruzada.

---

## 📝 3. Plantilla de Análisis de Alerta (Ejemplo de Guía)
Para cada incidente o alerta crítica investigada en el laboratorio, se documenta bajo los siguientes ejes:
1. **Regla de Wazuh:** Identificador y descripción de la regla disparada en el SIEM.
2. **Contexto del Endpoint:** Sistema operativo, dirección IP y usuario implicado.
3. **Hipótesis:** Evaluación inicial del origen del evento (¿es un falso positivo o una amenaza real?).
4. **Investigación:** Análisis de los logs crudos y correlación con eventos previos.
5. **Conclusión y Mitigación:** Acción tomada para resolver el evento o ajustar la regla de detección.
