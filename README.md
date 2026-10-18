# Urd

Monitor del tanque de agua de la casa: un Arduino conectado por USB al appliance de red (midgard)
mide el nivel con un sensor de ultrasonido y la temperatura con un DHT11. Un servicio en Python
convierte esas lecturas en litros, consumo por minuto y llegadas de agua desde la calle, las guarda
en SQLite y las muestra en Hlidskjalf, el tablero de pared de
[Yggdrasil](https://github.com/higerotech/yggdrasil). Documentación bajo la metodología AI-DLC.

En la mitología nórdica, Urðarbrunnr es el pozo que está bajo una de las raíces de Yggdrasil. Las
Nornas sacan agua de él cada día para regar el árbol. Urd sigue la convención de nombres de
Yggdrasil (`docs/00-project/naming.md`) y, como Bragi, vive en su propio repositorio.

## Estado

| Gate | Estado |
|---|---|
| 0 Requirements | En curso |
| 1–5 | Pendientes |

## Anonimización

Repositorio público. No contiene IPs, MACs, hostnames ni credenciales reales: los ejemplos usan
el rango de documentación RFC 5737 (`192.0.2.0/24`) y `example.com`. Los valores reales viven solo
en el `.env` del servidor, que está en `.gitignore`.

## Licencia

GPL-3.0.
