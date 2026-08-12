# 02 — Marcha-paro con enclavamiento

Lógica secuencial con memoria. Un pulsador de marcha momentáneo arranca el motor, que se mantiene solo por **enclavamiento**: un contacto de la propia salida, en paralelo con la marcha, realimenta el peldaño y sostiene el estado entre ciclos de scan. El paro, en serie (NC), rompe la cadena con prioridad.

## Entradas / Salidas

| Señal | Nombre | Tipo | Descripción |
|---|---|---|---|
| Entrada | `xMarcha` | BOOL | Pulsador de marcha (NA) |
| Entrada | `xParo` | BOOL | Pulsador de paro (NA) |
| Salida | `xMotor` | BOOL | Contactor del motor |

## Lógica (Ladder)

```
 ┌──┤ xMarcha ├──┬───┤/ xParo ├───( xMotor )───
 │  ┤ xMotor ├   │
 └───────────────┘
```

`(xMarcha OR xMotor) AND (NOT xParo) → xMotor`

## Probar en simulación

Forzar `xMarcha` a TRUE y volver a FALSE: el motor sigue en marcha (memoria). Forzar `xParo` a TRUE: se detiene.
