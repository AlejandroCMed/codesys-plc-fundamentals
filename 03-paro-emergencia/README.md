# 03 — Paro de emergencia con prioridad

Añade una seta de emergencia al marcha-paro con **seguridad positiva**. La seta se cablea como contacto NC: en reposo la señal vale 1 ("todo sano") y se lee con un contacto NA en el programa. Accionar la seta —o un fallo de cableado— lleva la señal a 0 y detiene la máquina. El fallo actúa a favor de la seguridad.

## Entradas / Salidas

| Señal | Nombre | Tipo | Cableado | Autoriza marcha cuando |
|---|---|---|---|---|
| Entrada | `xMarcha` | BOOL | NA | (pulsar) |
| Entrada | `xParo` | BOOL | NA | `xParo` = FALSE |
| Entrada | `xSeta` | BOOL | NC | `xSeta` = TRUE |
| Salida | `xMotor` | BOOL | — | — |

## Lógica (Ladder)

```
 ┌──┤ xMarcha ├──┬───┤/ xParo ├───┤ xSeta ├───( xMotor )───
 │  ┤ xMotor ├   │
 └───────────────┘
```

`(xMarcha OR xMotor) AND (NOT xParo) AND xSeta → xMotor`

## Probar en simulación

`xSeta` debe estar en TRUE (sano) para poder arrancar. Forzarla a FALSE emula tanto la seta pulsada como un cable cortado: en ambos casos el motor se detiene.
