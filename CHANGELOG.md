# Changelog

Todos los cambios notables de este proyecto se documentan en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/),
y este proyecto se adhiere a [Versionado Semántico](https://semver.org/lang/es/).

El cierre de cada gate AI-DLC corta versión (Gate 0 → 0.1.0, Gate 1 → 0.2.0, …).

## [Unreleased]

### Añadido
- Diseño de la conexión de los sensores (`docs/02-design/conexion-sensores.md`): Mega 2560 junto
  a midgard por USB con aislador ADuM3160, Cat6 de ~9 m hasta el tanque con un par por señal,
  pines, mapa del cable T568B, protecciones, dominio aislado, presupuesto de energía, lista de
  materiales y prueba en banco.
- ADR-0001 (proposed): enlace al tanque con el Mega junto a midgard, aislador ADuM3160 y sensores
  por Cat6; `/dev/urd` atado al número de serie del Mega original; RS-485 como plan B si falla la
  prueba en banco.
- Contrato de la trama serie URD1 (`docs/02-design/contrato-serie.md`): unidireccional, líneas
  ASCII con versión y suma XOR, tramas de arranque (H), nivel (M, cinco ecos crudos por segundo) y
  ambiente (A, DHT11 cada 10 s), validación en seis pasos con 14 vectores de prueba, estados del
  enlace, reinicio por DTR en lugar de watchdog y métricas del enlace.

## [0.1.0] - 2026-10-18

Gate 0 aprobado por Jeremi: en esta etapa Urd solo mide, con los umbrales iniciales propuestos,
un Arduino Mega 2560 y un HC-SR04, y el tanque a ~9 m de midgard.

### Añadido
- Arranque del repositorio: README, licencia GPL-3.0, `.gitattributes` (LF) y guardia de GitFlow
  hacia `main`.
- Gate 0: charter (con mapa mental del alcance), glosario y clasificación de datos.
- PRD `monitor-tanque` (URD-001) con los límites físicos de la medida, requisitos funcionales,
  RNF, requisitos de seguridad ASVS L1, escenarios de abuso y de fallo, C4 de contexto, journey,
  requirementDiagram, DFD y DREAD inicial.
- Registro de las decisiones de hardware del 2026-10-18 (Arduino Mega 2560 por USB, DHT11,
  HC-SR04 y flecha de tres estados) con sus riesgos aceptados.
- RNF08 y AB09: los ~9 m entre el tanque y midgard superan los 5 m del USB 2.0 pasivo y el cable
  llega al router de la casa; el enlace, con aislamiento galvánico, se decide en el Gate 1.
- Checklists de gates 0–5.

[Unreleased]: https://github.com/higerotech/urd/compare/v0.1.0...develop
[0.1.0]: https://github.com/higerotech/urd/releases/tag/v0.1.0
