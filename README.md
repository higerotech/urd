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
| 0 Requirements | Aprobado (0.1.0) |
| 1–5 | Pendientes |

## Números que mandan el diseño

Del tanque, un Q'Botella 3200 (Ø 1,30 × 2,60 m, 3100 L útiles):

- El cuerpo guarda **13,3 L por cm**: un centímetro de error son 13 L.
- La parte alta no es cilíndrica (un cilindro tendría 3451 L): el volumen se calibra en sitio.
- Una ducha baja el nivel ~0,7 cm/min y se mide bien; 2 L sueltos (1,5 mm) quedan bajo el ruido.
- Entre 20 y 40 °C, sin compensación térmica, el ultrasonido se desvía ~7 cm (~94 L) a 2 m.

## Estructura

```
docs/
  00-project/           # charter, glosario, clasificación de datos y ADRs
  01-requirements/      # PRD con límites físicos, abuso, ASVS y threat assessment
  02-design/            # diseño: conexión de los sensores y contrato serie
.ai-dlc/gates/          # checklists de gates
```

## Anonimización

Repositorio público. No contiene IPs, MACs, hostnames ni credenciales reales: los ejemplos usan
el rango de documentación RFC 5737 (`192.0.2.0/24`) y `example.com`. Los valores reales viven solo
en el `.env` del servidor, que está en `.gitignore`.

## Licencia

GPL-3.0.
