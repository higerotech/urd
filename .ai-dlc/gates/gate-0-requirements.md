# Gate 0 — Requirements

- [x] PRD con objetivos y no-objetivos (`docs/01-requirements/monitor-tanque.md`)
- [x] Límites físicos de la medida documentados (13,3 L/cm, hombro no lineal, balance neto,
      flotador, compensación térmica, alcance del HC-SR04, enlace de 9 m)
- [x] Escenarios de abuso y de fallo documentados (AB01–AB09)
- [x] Requisitos de seguridad mapeados a OWASP ASVS L1 (RS01–RS07)
- [x] Threat assessment inicial (DFD + quadrant DREAD)
- [x] Clasificación de datos (`docs/00-project/data-classification.md`)
- [x] Charter + glosario (lenguaje ubicuo)
- [x] Decisiones de hardware tomadas por Jeremi el 2026-10-18 (USB, DHT11, ultrasonido, flecha
      de tres estados), con sus riesgos aceptados
- [x] **HITL**: alcance y no-scope validados: en esta etapa Urd solo mide (Jeremi, 2026-10-18)
- [x] **HITL**: umbrales iniciales aceptados tal como se propusieron: error ≤ 3 % tras calibrar;
      llegada con ≥ 3 L/min durante 3 min y reflejada en ≤ 5 min; tanque bajo < 20 %; fuga
      ≥ 0,5 L/min durante 60 min entre las 02:00 y las 05:00; retención de muestras por minuto de
      400 días. Se revisan con datos reales en el Gate 5
- [x] **HITL**: Arduino Mega 2560 y sensor HC-SR04 (trigger y echo)
- [x] **HITL**: distancia confirmada: el tanque está a ~9 m de midgard. Supera los 5 m del USB 2.0
      pasivo; queda como RNF08 y AB09, y el enlace y el recorrido del cable pasan a un ADR del
      Gate 1

Evidencia: journey + requirementDiagram + DFD/quadrant en el PRD.
Aprobado el 2026-10-18: `[Unreleased]` → `0.1.0`; charter, glosario, clasificación y PRD en
`approved`.
