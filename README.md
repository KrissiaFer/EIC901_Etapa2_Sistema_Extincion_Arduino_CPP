# EIC901 · Etapa 2 — Sistema de extinción por votación 2 de 3 (Arduino C++)

Sistema de extinción de incendios basado en lógica de votación implementado en **Arduino UNO R3** con **C++**. Tres sensores (interruptores A, B y C) se evalúan mediante una función booleana; cuando se cumple la condición, se activa un **motor DC** (bomba/extintor) a través de un transistor NPN y un **LED** indicador.

## Función lógica

```
F = (A && B) || (!C && (A || B))
```

| A | B | C | F | LED | Motor |
|:-:|:-:|:-:|:-:|---|---|
| 0 | 0 | 0 | 0 | Apagado | Detenido |
| 0 | 0 | 1 | 0 | Apagado | Detenido |
| 0 | 1 | 0 | 1 | Encendido | Girando |
| 0 | 1 | 1 | 0 | Apagado | Detenido |
| 1 | 0 | 0 | 1 | Encendido | Girando |
| 1 | 0 | 1 | 0 | Apagado | Detenido |
| 1 | 1 | 0 | 1 | Encendido | Girando |
| 1 | 1 | 1 | 1 | Encendido | Girando |

**Resultado de validación: 8/8 combinaciones correctas.** Detalle y evidencias en [pruebas/tabla_verdad.md](pruebas/tabla_verdad.md).

## Hardware

| Elemento | Pin / conexión |
|---|---|
| Entrada A | D2 |
| Entrada B | D3 |
| Entrada C | D4 |
| Motor DC (vía transistor NPN + resistencia de base) | D8 |
| LED indicador | D9 |
| Alimentación del motor | Fuente independiente de 5 V, tierra común |
| Protección | Diodo flyback en paralelo con el motor |

## Estructura del repositorio

```
├── Codigo fuente/        Sketch de Arduino (.ino)
├── Documento/            Informe de la segunda entrega (PDF)
├── Proyecto/             Enlace a la simulación en Tinkercad
├── Video explicativo/    Enlace al video explicativo
├── capturas/             Capturas de entradas, programa, etapa de potencia y pruebas
└── pruebas/              Tabla de verdad y registro de avances
```

## Uso

1. Abrir [Codigo fuente/EIC901_Etapa2_Arduino_CPP.ino](Codigo%20fuente/EIC901_Etapa2_Arduino_CPP.ino) en el Arduino IDE.
2. Seleccionar la placa **Arduino UNO** y cargar el programa.
3. Abrir el Monitor Serial a **115200 baudios** para ver el estado de `A`, `B`, `C` y `F` cada 500 ms.

## Simulación

- Circuito en Tinkercad: [abrir simulación](https://www.tinkercad.com/things/4VEX9vVvEAo-eic901etapa2sistemaextincionarduinocpp?sharecode=oYl9HFb9AblIeLe8uCefzoiCKroxj-k_aQ0VEF1MGRA)
- Video explicativo: [Google Drive](https://drive.google.com/file/d/1qmc9fi7ZOSwv25klmq6QZZaIjMEIDyaI/view?usp=sharing)

### Mediciones (simulación)

- Fuente regulada: 5,00 V
- Motor apagado: ≈ 0,00 A, 0 rpm
- Motor encendido: ≈ 79,3 mA

> Las lecturas provienen de la simulación y no sustituyen la verificación de la corriente de arranque en un montaje real.

## Integrantes

| Nombre | Carné |
|---|---|
| Oscar Danilo Rivera Bernal | RB130430 |
| Moises David Garcia Casco | GC251462 |
| Daniela Fernanda Tamayo Jovel | TJ231470 |
| Cesar Ernesto Perdomo Guerrero | PG241690 |
| Krissia Lissette Eguizabal Fernandez | EF251345 |

Universidad Don Bosco · Electrónica Aplicada al Internet de las Cosas (EIC901) · Docente: Ing. Eduardo Antonio Henriquez · 2026
