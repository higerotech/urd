# Gate 0 — Requirements

- [x] PRD con objetivos y no-objetivos (`docs/01-requirements/monitor-tanque.md`)
- [x] Límites físicos de la medida documentados (13,3 L/cm, hombro no lineal, balance neto,
      flotador, compensación térmica, alcance del PING)))
- [x] Escenarios de abuso y de fallo documentados (AB01–AB08)
- [x] Requisitos de seguridad mapeados a OWASP ASVS L1 (RS01–RS07)
- [x] Threat assessment inicial (DFD + quadrant DREAD)
- [x] Clasificación de datos (`docs/00-project/data-classification.md`)
- [x] Charter + glosario (lenguaje ubicuo)
- [x] Decisiones de hardware tomadas por Jeremi el 2026-10-18 (USB, DHT11, PING))) o HC-SR04,
      flecha de tres estados), con sus riesgos aceptados
- [ ] **HITL**: validar alcance y no-scope (solo mide, sin caudalímetro, solo LAN, un tanque)
- [ ] **HITL**: confirmar los umbrales iniciales: error ≤ 3 % tras calibrar; llegada con
      ≥ 3 L/min durante 3 min y reflejada en ≤ 5 min; tanque bajo < 20 %; fuga ≥ 0,5 L/min
      durante 60 min entre las 02:00 y las 05:00; retención de muestras por minuto de 400 días
- [ ] **HITL**: modelo de Arduino (Uno, Nano o Mega) y sensor concreto: el PING))) usa un solo
      pin y el HC-SR04 dos (trigger y echo)
- [ ] **HITL**: confirmar que el tanque queda a menos de ~5 m de midgard y por dónde va el cable

Evidencia: journey + requirementDiagram + DFD/quadrant en el PRD.
Al aprobar: cortar `[Unreleased]` → `0.1.0` y pasar charter, glosario, clasificación y PRD a `approved`.
