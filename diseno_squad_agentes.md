# Diseño de squad de agentes para análisis de planos, especificaciones y cronograma

## 1) Objetivo del squad
Diseñar un equipo de agentes de IA que trabaje de forma coordinada para:
- Analizar planos de **arquitectura**.
- Analizar planos de **estructura**.
- Analizar planos de **MEP** (mecánicas, eléctricas e hidrosanitarias).
- Revisar **especificaciones técnicas** y criterios de calidad.
- Validar consistencia con el **cronograma del proyecto**.
- Detectar interferencias, omisiones, riesgos y prioridades de ejecución.

---

## 2) Estructura recomendada del squad

### A. Agente Orquestador (PM de IA)
**Rol:** coordinar a todos los agentes, consolidar hallazgos y priorizar acciones.

**Entradas:**
- Planos y modelos (PDF, DWG, IFC, RVT exportado).
- Especificaciones técnicas.
- Cronograma (MS Project, Primavera, CSV).
- Matriz de riesgos y restricciones del proyecto.

**Salidas:**
- Reporte ejecutivo de incidencias priorizadas (críticas, medias, bajas).
- Lista de RFIs sugeridas.
- Backlog de acciones por disciplina y por frente.

---

### B. Agente de Arquitectura
**Rol:** validar cumplimiento arquitectónico y constructibilidad en arquitectura.

**Revisa:**
- Coherencia de plantas, cortes, elevaciones y detalles.
- Cuadros de áreas, ejes, niveles, accesibilidad, circulaciones y normativa.
- Correspondencia de acabados y especificaciones.

**Detecta:**
- Inconsistencias geométricas.
- Falta de cotas/niveles.
- Ambigüedades en detalles de encuentro entre elementos.

---

### C. Agente de Estructura
**Rol:** revisar integridad y coordinación estructural.

**Revisa:**
- Malla estructural, secciones, refuerzo, notas generales y detalles.
- Compatibilidad con arquitectura y MEP (huecos, pases, cargas, apoyos).
- Secuencias críticas para montaje/colado y restricciones temporales.

**Detecta:**
- Conflictos entre elementos estructurales y pasos de instalaciones.
- Riesgos por cambios de sección no reflejados en otras láminas.
- Dependencias constructivas no explicitadas.

---

### D. Agente MEP
**Rol:** validar diseño y coordinación de instalaciones.

**Revisa:**
- Rutas de ductos, tuberías, bandejas y canalizaciones.
- Equipos, capacidades, espacios de mantenimiento y accesos.
- Cumplimiento de criterios de seguridad, separación y pendientes.

**Detecta:**
- Colisiones MEP vs arquitectura/estructura.
- Falta de espacio técnico en plafones, shafts y cuartos técnicos.
- Omisiones de válvulas, registros, soportes o elementos de operación.

---

### E. Agente de Especificaciones Técnicas
**Rol:** asegurar que los planos respeten las especificaciones y normas del proyecto.

**Revisa:**
- Materiales, tolerancias, métodos de instalación, pruebas y aceptación.
- Requisitos normativos y códigos aplicables.
- Submittals, fichas técnicas y equivalencias permitidas.

**Detecta:**
- Discrepancias plano-especificación.
- Requisitos sin trazabilidad en planos.
- Riesgos de calidad por falta de criterios de inspección.

---

### F. Agente de Planificación / Cronograma (4D)
**Rol:** vincular entregables técnicos con secuencia de obra y hitos.

**Revisa:**
- Ruta crítica, hitos contractuales y ventanas de trabajo.
- Dependencias entre disciplinas.
- Restricciones logísticas y de abastecimiento.

**Detecta:**
- Actividades sin prerequisitos técnicos completos.
- Secuencias inviables por interferencias pendientes.
- Riesgo de retraso por aprobaciones tardías (RFI/submittals).

---

### G. Agente de Clash & Riesgos
**Rol:** cuantificar impactos y priorizar mitigaciones.

**Revisa:**
- Matriz de conflictos (clash hard/soft).
- Severidad (seguridad, costo, plazo, retrabajo).
- Probabilidad e impacto por frente de trabajo.

**Detecta:**
- “Top 10” riesgos semanales del proyecto.
- Paquetes de trabajo con mayor exposición.
- Acciones preventivas y responsables sugeridos.

---

## 3) Flujo operativo sugerido (semanal)
1. **Ingesta documental** (versionado y control de cambios).
2. **Preanálisis por disciplina** (arquitectura, estructura, MEP, specs).
3. **Cruce interdisciplinario** (detección de conflictos y dependencias).
4. **Análisis 4D** (impacto en cronograma y ruta crítica).
5. **Priorización** (criticidad + esfuerzo + plazo).
6. **Emisión de reporte** (hallazgos, RFIs, acciones y responsables).
7. **Cierre de ciclo** (validación de resoluciones y lecciones aprendidas).

---

## 4) Datos mínimos de entrada
- Planos disciplinarios actualizados por versión.
- Modelo BIM federado (ideal) o PDFs coordinados.
- Especificaciones técnicas vigentes.
- Cronograma con IDs de actividades y calendario.
- Catálogo de normas aplicables.
- Bitácora de RFIs, submittals y cambios aprobados.

---

## 5) Entregables del squad
- **Reporte ejecutivo** por semana con ranking de incidencias.
- **Matriz de coordinación** por disciplina (estado: abierto/en curso/cerrado).
- **Mapa de impacto en cronograma** (actividad afectada, días potenciales, mitigación).
- **Lista priorizada de RFIs**.
- **Tablero KPI** (clashes abiertos, tiempo medio de cierre, % impacto en ruta crítica).

---

## 6) KPI recomendados
- % de interferencias resueltas antes de obra por frente.
- Tiempo promedio de cierre de incidencias (días).
- % de actividades críticas liberadas “a tiempo” con información completa.
- Nº de RFIs por disciplina y tendencia semanal.
- Retrabajo evitado estimado (costo/plazo).

---

## 7) Stack tecnológico sugerido
- **Ingesta y OCR:** extracción de texto/cotas de planos y especificaciones.
- **BIM/Clash:** integración con motores de coordinación (IFC/BIM).
- **NLP técnico:** comparación plano vs especificación.
- **Motor de reglas:** validaciones normativas y de constructibilidad.
- **Analítica 4D:** conexión con cronograma para análisis de impacto.
- **Dashboard:** visualización de KPI y estado de incidencias.

---

## 8) Gobierno y calidad de datos
- Definir dueño de dato por disciplina.
- Control estricto de versiones (única fuente de verdad).
- Trazabilidad completa hallazgo → acción → cierre.
- Umbrales de confianza de IA y revisión humana obligatoria en hallazgos críticos.

---

## 9) Implementación por fases

### Fase 1 (2–4 semanas): Piloto
- Enfoque en 1 zona del proyecto y 1 ciclo semanal.
- Objetivo: detectar interferencias y riesgos de cronograma tempranos.

### Fase 2 (4–8 semanas): Escalamiento
- Incorporar validación completa de especificaciones y KPI.
- Integrar tablero de seguimiento con responsables.

### Fase 3 (continuo): Operación
- Integración total con proceso de coordinación técnica.
- Mejora continua con feedback de obra y supervisión.

---

## 10) Resultado esperado
Con este squad, el proyecto logra **menos retrabajos**, **menor riesgo de atrasos** y **mejor calidad documental**, al convertir revisiones aisladas en un proceso coordinado, trazable y orientado a decisiones.
