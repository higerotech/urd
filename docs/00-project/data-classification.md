# Clasificación de datos — Urd

* **Estado:** approved
* **Fecha:** 2026-10-18
* **Decisores:** Jeremi
* **Fase AI-DLC:** 00-project
* **Versión:** 0.1.0

| Dato | Clase | Dónde vive | Protección | Tránsito | Retención |
|---|---|---|---|---|---|
| Muestras por minuto (nivel, volumen, consumo, temperatura, humedad) | **Interno (personal)**: el patrón de consumo revela cuándo hay gente en casa | SQLite en disco local de midgard, fuera del clon | Directorio del usuario del servicio; respaldo nocturno al NAS | Serie USB local; `/metrics` solo en la red Docker de Heimdall | `<TODO: confirmar>` propuesta: 400 días |
| Llegadas de agua (inicio, fin, litros) y consumo diario | **Interno (personal)** | SQLite | Igual | Igual | Indefinida |
| Tabla de calibración y distancia al fondo | **Interno** | Fichero de configuración del servidor, fuera del repo | Igual | — | Mientras exista la instalación |
| Texto de los avisos push («tanque bajo», «posible fuga»…) | **Interno** | Sale de la LAN por el canal de avisos de Nornas | Solo el resumen de la alerta, nunca el historial | HTTPS al servicio de avisos | La del servicio de avisos |
| Número de serie del Arduino (lo usa la regla udev) e IPs de la instalación | **Interno** | Solo en el servidor | El repo es público: ejemplos RFC 5737 y un serie ficticio | — | — |

Urd no tiene cuentas, contraseñas ni secretos propios: no hay ningún dato **Confidencial**. El
token del webhook de Nornas pertenece a Yggdrasil y Urd no lo usa.

## Reglas
1. Las muestras y las llegadas no salen de la LAN. La única excepción es el texto de los avisos.
2. La base SQLite nunca vive en NFS ni dentro del clon: el NFS no garantiza los bloqueos que
   SQLite necesita.
3. El repositorio solo lleva ejemplos de calibración y de regla udev, nunca los de la casa.
