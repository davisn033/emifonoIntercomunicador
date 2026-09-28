# Emífono — Analog Intercom

> Diseño e implementación de un intercomunicador de audio basado en electrónica analógica discreta.

**Proyecto final — Electrónica Análoga I | Laboratorio G7**  
**Universidad Nacional de Colombia — Bogotá**

## Descripción

Emífono es un intercomunicador analógico de dos nodos diseñado para transmitir y reproducir señales de voz mediante un canal compartido. El sistema integra amplificación BJT, filtrado pasivo, adaptación de impedancias y una etapa de potencia para un parlante de 8 Ω.

El diseño parte de una señal de micrófono de baja amplitud y la acondiciona mediante una arquitectura de amplificación en cascada. La primera etapa realiza la amplificación de voltaje y la etapa de salida utiliza un par Darlington para proporcionar el acople de impedancias y la corriente necesaria para la carga.

## Datos principales del proyecto

| Parámetro | Dato reportado |
|---|---:|
| Alimentación | 9 V |
| Micrófono | Electret |
| Tensión de operación del micrófono | 2.02 V |
| Corriente de polarización | 0.2 mA |
| Impedancia de salida del micrófono | 4.85 kΩ |
| Banda de voz | 300 Hz – 3.4 kHz |
| Preamplificación base | ≈ ×10 |
| Carga | 8 Ω |
| Potencia calculada al parlante | ≈ 176 mW |
| Entrada usada en simulaciones | 20 mVpp, 1 kHz |

## Características

- Intercomunicador de **dos nodos** con canal físico compartido.
- Micrófono **electret** caracterizado experimentalmente.
- Preamplificación mediante **BJT en emisor común**.
- Filtros RC pasivos para acondicionar la banda de voz.
- Etapa de salida basada en **par Darlington**.
- Selección del nodo transmisor mediante **pulsador**.
- **Vúmetro/indicador de sobrecarga** con BJT y LEDs.
- Control de volumen mediante **potenciómetro logarítmico**.
- Segundo dispositivo con efecto de voz tipo **Fuzz** mediante saturación deliberada de una etapa BJT.
- Simulación en **LTspice**.

## Arquitectura

```text
Micrófono 1 ──> Preamplificador ──> Filtro ──┐
                                               │
                                               ▼
                                          Selector
                                               │
                                               ▼
                                      Canal compartido
                                               │
                                               ▼
                                      Filtro de entrada
                                               │
                                               ▼
                                     Amplificación potencia
                                               │
                                               ▼
                                            Parlante

Micrófono 2 ──> Preamplificador ──> Filtro ──┘
```

El pulsador selecciona qué señal llega al canal compartido.

## Diseño y resultados

### 1. Micrófono electret

El micrófono adquirido no tenía una referencia identificable, por lo que se caracterizó experimentalmente. El informe registra 2.02 V de operación, 0.2 mA de corriente de polarización y aproximadamente 4.85 kΩ de impedancia de salida.

### 2. Preamplificador

Se evaluaron las configuraciones fundamentales del BJT y se seleccionó el **emisor común sin bypass** para la amplificación de voltaje. El diseño base reporta aproximadamente:

- (R_C=2.4,kΩ)
- (R_E=220,Ω)
- (I_C=1.264,mA)
- (A_v≈-9.98,V/V)
- (Z_{in}≈6.5,kΩ)
- (Z_{out}=2.4,kΩ)

### 3. Filtrado

La señal se acondiciona mediante filtros RC pasivos con una banda de trabajo aproximada de **300 Hz a 3.4 kHz**.

### 4. Salida de potencia

El par Darlington adapta la impedancia hacia el parlante de 8 Ω. El cálculo reportado da una potencia aproximada de **176 mW**, superior al mínimo requerido de 0.125 W.

### 5. Dispositivo 1

El primer dispositivo incorpora control de volumen y un vúmetro/indicador de sobrecarga. La etapa adicional de amplificación se calculó con (A_v≈-19.27), (Z_{in}≈7.77,kΩ) y (Z_{out}≈3.3,kΩ).

En la simulación con 20 mVpp a 1 kHz, el informe reporta una ganancia práctica máxima de aproximadamente **7.49 V/V** debido a la limitación del potenciómetro.

### 6. Dispositivo 2 — Fuzz

El segundo dispositivo incorpora un bloque Fuzz basado en saturación intencional de una etapa BJT. El informe reporta aproximadamente (V_{CE}=1.645,V) para Q12 y una ganancia calculada de (-29.27,V/V) antes de considerar el recorte no lineal.

Después del Fuzz se añadió un atenuador fijo de 2 kΩ/47 kΩ (≈ −27.4 dB), y la preamplificación del dispositivo 2 se ajustó a aproximadamente **−14.13 V/V**.

### 7. Evidencia visual del informe

Las figuras del informe se conservaron como fuente de evidencia para los esquemas, modelos, gráficas y resultados. Consulta:

- [Índice de figuras](docs/figure-index.md)
- [Datos y mediciones](docs/measurements.md)
- [Notas de diseño](docs/design-notes.md)
- [Resultados de simulación](docs/simulation.md)

El informe original contiene las figuras numeradas 1–39, incluyendo los circuitos, modelos de Fuzz, esquemas completos, gráficas del vúmetro y la salida del Fuzz.

## Construcción y aprendizajes

La bitácora registra problemas reales de montaje: ruido asociado a algunas configuraciones de bypass, necesidad de añadir resistencias para estabilizar el punto de operación, una resistencia que se quemó por una selección insuficiente de potencia y la importancia de verificar los pinouts de los componentes antes del montaje.

## Estructura

```text
emifonoIntercomunicador/
├── README.md
├── .gitignore
├── docs/
│   ├── design-notes.md
│   ├── measurements.md
│   ├── simulation.md
│   └── figure-index.md
├── schematics/
├── simulation/
├── pcb/
├── measurements/
└── images/
```

## Autores

- Sofia Molano Martínez
- Edwin David Figueroa García
- Juan Sebastián Nieto Cruz

**Universidad Nacional de Colombia — Bogotá**  
**Electrónica Análoga I**
