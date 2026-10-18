# Gate 1 — Design

Pendiente. Se abre al cerrar el gate anterior.

Previsto: C4 Container (firmware, servicio, SQLite, integración con Yggdrasil), contrato de la
trama serie, `erDiagram` de muestras, llegadas y consumos diarios, `stateDiagram` del estado de
entrada, secuencia de la llegada de agua, threat model STRIDE con DREAD residual, procedimiento
de calibración y ADRs: placement en midgard, SQLite como fuente de verdad junto a `/metrics`,
integración en Hlidskjalf, el riesgo AB04 (reprogramación por el puerto serie) y el enlace de
~9 m entre el tanque y midgard (RNF08, AB09): tipo de enlace, aislamiento galvánico, alimentación
del Mega y recorrido del cable.

Hecho (draft): conexión de los sensores por Cat6 (`docs/02-design/conexion-sensores.md`).

Registrar Urd en `docs/00-project/naming.md` de Yggdrasil, como se hizo con Bragi.
