# CODESYS PLC — Fundamentos de automatismos

![Demo: marcha-paro con retardo TON en simulación](04-marcha-paro-ton/video/ton-demo.gif)

Automatismos básicos en lógica de contactos (Ladder, IEC 61131-3), programados y simulados en **CODESYS V3.5**. Del pulsador simple al marcha-paro con temporizador, aplicando criterio de **seguridad positiva** en las paradas de emergencia.

## Contenido

| # | Ejercicio | Concepto clave |
|---|-----------|----------------|
| 01 | [Pulsador → Lámpara](01-pulsador-lampara/) | Lógica combinacional (sin memoria) |
| 02 | [Marcha-paro con enclavamiento](02-marcha-paro/) | Memoria / realimentación (seal-in) |
| 03 | [Paro de emergencia con prioridad](03-paro-emergencia/) | Seguridad positiva (seta NC) |
| 04 | [Marcha-paro con retardo (TON)](04-marcha-paro-ton/) | Temporizador on-delay |

## Cómo abrir los programas

Cada ejercicio incluye dos formatos en su carpeta `plc/`:

- **`.project`** — formato nativo de CODESYS. Se abre directamente con CODESYS V3.5 o superior.
- **`.xml`** — exportación **PLCopen XML** (IEC 61131-3), formato neutro de fabricante: permite inspeccionar o importar la lógica desde otras herramientas compatibles sin necesidad de CODESYS.

Para probarlos: abrir el `.project`, compilar (F11), activar `Online → Simulación`, hacer login (Alt+F8) y arrancar (F5). No hace falta hardware: todo corre en el simulador integrado.

## Decisiones técnicas

- **Seguridad positiva en la parada de emergencia (ej. 03).** La seta se cablea como contacto NC (señal = 1 cuando todo está sano) y se lee con un contacto NA en el programa. Así, tanto accionar la seta como un fallo de cableado llevan la señal a 0 y detienen la máquina: el fallo actúa a favor de la seguridad.
- **Enclavamiento por realimentación (ej. 02 y 04).** La salida (o una marca interna) se realimenta con su propio contacto en paralelo con la marcha, manteniendo el estado entre ciclos de scan. El paro, en serie, tiene prioridad.
- **Memoria local, no global (ej. 04).** El retardo obliga a memorizar la orden de marcha en un bit auxiliar: se usa una variable local con nombre descriptivo (`xOrdenMarcha`), no una marca global anónima.
- **Una salida, un peldaño.** Ninguna salida se asigna en dos networks distintas; el scan sobrescribiría el valor.

## Entorno

CODESYS V3.5 SP22 · dispositivo *CODESYS Control Win V3 x64* en modo simulación · lógica de contactos (LD).

---

*Parte de mi formación práctica en automatización industrial. Perfil OT/IT: del SCADA al cuadro y vuelta.*
