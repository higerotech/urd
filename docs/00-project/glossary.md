# Glosario — lenguaje ubicuo de Urd

* **Estado:** approved
* **Fecha:** 2026-10-18
* **Decisores:** Jeremi
* **Fase AI-DLC:** 00-project
* **Versión:** 0.1.0

| Término | Definición |
|---|---|
| **Urd** | El sistema completo: el Arduino con sus sensores, el servicio en Python y su base SQLite. |
| **midgard** | El appliance de red de la casa (router con dos WAN) donde corre Urd. |
| **Tanque** | El Q'Botella 3200 de la casa: 3150 L totales, 3100 L útiles. |
| **Distancia** | Lo que mide el ultrasonido: del sensor, en la tapa, a la superficie del agua. |
| **Altura de agua** | Distancia del fondo a la superficie. Se obtiene restando la distancia de la distancia al fondo calibrada. |
| **Volumen** | Litros de agua en el tanque. Se obtiene de la altura con la tabla de calibración. |
| **Tabla de calibración** | Pares altura → volumen medidos en sitio. Hace falta porque el hombro y el cuello del tanque no son cilíndricos. |
| **Nivel** | Volumen como porcentaje del volumen útil. Es lo que pinta la silueta. |
| **Trama** | Una línea que el Arduino envía por el puerto serie con una lectura y su versión de firmware. |
| **Lectura** | Una medida cruda de los sensores. El Arduino envía varias por minuto. |
| **Muestra** | El resumen de un minuto (mediana de las lecturas válidas). Es lo que se guarda en SQLite. |
| **Compensación térmica** | Corregir la distancia con la velocidad del sonido a la temperatura del aire del tanque. |
| **Zona ciega** | Distancia mínima que el ultrasonido no puede medir (unos 2 cm en el HC-SR04). |
| **Balance neto** | Lo que entra menos lo que sale. El nivel solo mide esto: con agua entrando y saliendo a la vez, solo se ve la diferencia. |
| **Consumo** | Litros por minuto que salen del tanque cuando no entra agua. |
| **Entrada neta** | Litros por minuto que suben mientras entra agua. |
| **Llegada (de agua)** | Periodo con subida neta sostenida: el agua de la calle está entrando. Tiene inicio, fin y litros recibidos. |
| **Flotador** | La válvula de la entrada que cierra al llenarse el tanque. |
| **Tanque lleno** | Nivel en el que el flotador cierra. Por encima no puede entrar agua, así que no se sabe si la calle tiene. |
| **Estado de entrada** | **Entrando** (flecha verde), **sin entrada** (roja, el tanque no está lleno y no sube), **lleno** (gris, no se puede saber) o **sin datos**. |
| **Fuga** | Consumo sostenido en horas en que nadie usa agua (de madrugada). |
| **Hlidskjalf** | El tablero de pared de Yggdrasil (tablet kiosco), donde se ve el tanque. |
| **Mimir / Gjallarhorn / Nornas** | Prometheus, Alertmanager y Node-RED de Yggdrasil: guardan las métricas, deciden las alertas y mandan los avisos push. |
