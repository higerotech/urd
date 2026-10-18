# ADR-0001: Enlace al tanque: Mega junto a midgard y sensores por Cat6

* **Estado:** proposed
* **Fecha:** 2026-10-18
* **Decisores:** Jeremi
* **Fase AI-DLC:** 02-design
* **Versión:** 0.1.0
* **ID:** ADR-0001
* **Supersede / Superseded-by:** —
* **Requisitos:** RNF01, RNF02, RNF08, AB07, AB09
* **Controles OWASP afectados:** A06 (diseño inseguro: un cable exterior que llega al router)

## Contexto
- El tanque está a **~9 m** de midgard. El cable va bajo techo por el perímetro exterior de la casa.
  Junto al tanque hay un enchufe.
- Un cable **USB 2.0 pasivo admite 5 m**.
- midgard es el router de la casa y no tiene UPS: una sobretensión que llegue por el cable lo deja
  sin red (AB09).
- Hardware elegido por Jeremi en el Gate 0: **Arduino Mega 2560 original**, HC-SR04 y DHT11, por
  USB a midgard. El chip USB del Mega original (ATmega16U2 en la R3, ATmega8U2 en las
  revisiones anteriores) se anuncia con el fabricante `2341` y un **número de serie único**, y va
  a full speed (12 Mbit/s).
- Jeremi propuso el 2026-10-18 llevar Cat6 hasta los sensores y alimentar el Arduino desde el USB
  de midgard.

## Decisión
1. **El Mega queda junto a midgard**, dentro de la casa. Se conecta con un USB corto que pasa por
   un **aislador ADuM3160 en modo full speed**, y se alimenta de ese mismo puerto, sin otra
   fuente.
2. **Hasta el tanque solo van los sensores**, por un **Cat6 UTP de cobre sólido de ~9 m**, con un
   par trenzado por señal y su retorno, borneras en los dos extremos y protecciones del lado del
   Mega. El detalle de pines, cable, protecciones y materiales está en
   [conexión de los sensores](../../02-design/conexion-sensores.md).
3. **El nombre fijo del puerto (RNF01) se ata al número de serie** del chip USB del Mega:
   `SUBSYSTEM=="tty", ATTRS{idVendor}=="2341", ATTRS{serial}=="<serie>", SYMLINK+="urd"`. La regla
   no depende del `idProduct`, que cambia según la revisión de la placa. El número de serie es un
   dato de la instalación (RS05): no va al repositorio. El bootstrap del Gate 4 lo lee en midgard
   con `udevadm info` y escribe allí la regla.
4. **Antes de instalar, una prueba en banco** con ~10 m del mismo Cat6 (Gate 3, criterios en el
   documento de conexión). Si no la pasa, se aplica la alternativa RS-485 de abajo.

## Alternativas consideradas
| Opción | Pros | Contras |
|---|---|---|
| **Mega junto a midgard, sensores por Cat6** (elegida) | Un solo dominio eléctrico, aislado del router; el Mega queda bajo techo y se reprograma sin ir al tanque; no hace falta el enchufe del tanque; materiales baratos | Las señales del HC-SR04 viajan 9 m, algo que su hoja de datos no cubre: se valida en banco |
| Mega en el tanque con cable USB activo de 10 m | Los sensores quedan a centímetros | El repetidor también se alimenta del puerto y aprieta el presupuesto del ADuM3160; el Mega queda a la intemperie; para reprogramarlo hay que ir al tanque |
| Mega en el tanque con RS-485 sobre el mismo Cat6 | Muy robusto, hasta 1200 m; los sensores quedan a centímetros | Necesita fuente junto al tanque, que es un segundo dominio eléctrico; adaptador USB a RS-485 aislado en midgard; el Mega a la intemperie. **Plan B** si falla la prueba en banco |
| Extensor USB sobre Cat6 | Sin cambios en el firmware | Una caja negra más, que suele pedir fuente en el extremo remoto y no aísla |
| ESP32 por WiFi a Ratatosk | Sin cable | Descartado en el Gate 0: depende del WiFi y necesita fuente en el tanque |

## Consecuencias
- **Positivas:**
  - Todo lo que está más allá del aislador comparte una sola tierra flotante, así que un pico en el
    cable exterior se queda de ese lado (RNF08).
  - Si se va la luz, midgard y Urd se apagan y arrancan juntos (RNF02).
  - El número de serie mantiene `/dev/urd` aunque el Mega cambie de puerto (RNF01).
- **Negativas:**
  - Un corto en el cable deja a Urd sin sensores. El PTC protege al Mega, que sigue vivo para
    contar el fallo (RS07), pero no hay medida hasta que se repare.
  - Abrir el puerto serie reinicia el Mega original (DTR). El contrato de la trama serie (Gate 1)
    debe esperar el arranque y descartar lo que llegue antes de la primera trama válida.
  - El aislamiento es frágil: se rompe si alguien alimenta el Mega por el jack o conecta la caja
    del tanque a tierra. Queda rotulado en las cajas.
- **Condiciones de revisión:**
  - Si la prueba en banco del Gate 3 no cumple (ecos perdidos > 1 % o dispersión > ±3 mm), se pasa
    a RS-485.
  - Si en operación los contadores de fallo de sensor (RS07) muestran errores sostenidos que no se
    explican por la condensación, también se pasa a RS-485.
