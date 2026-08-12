# 01 — Pulsador → Lámpara

Lógica combinacional: la salida es función directa de la entrada, recalculada en cada ciclo de scan. **Sin memoria** — la lámpara sigue al pulsador y se apaga en cuanto se suelta.

## Entradas / Salidas

| Señal | Nombre | Tipo | Descripción |
|---|---|---|---|
| Entrada | `xPulsador` | BOOL | Pulsador de mando (NA) |
| Salida | `xLampara` | BOOL | Lámpara de señalización |

## Lógica (Ladder)

```
 ───┤ xPulsador ├───────────( xLampara )───
```

## Probar en simulación

Abrir `plc/01_Pulsador_Lampara.project`, compilar (F11), `Online → Simulación`, login (Alt+F8), Start (F5). Forzar `xPulsador` a TRUE (Ctrl+F7) enciende la lámpara; a FALSE la apaga.
