# Emífono — Analog Intercom

> Diseño e implementación de un intercomunicador de audio basado en electrónica analógica discreta.

**Proyecto final — Electrónica Análoga I | Laboratorio G7**  
**Universidad Nacional de Colombia — Bogotá**

## Descripción

Emífono es un intercomunicador analógico de dos nodos diseñado para transmitir y reproducir señales de voz mediante un canal compartido. El sistema integra amplificación BJT, filtrado pasivo, adaptación de impedancias y una etapa de potencia para un parlante de 8 Ω.

El diseño parte de una señal de micrófono de baja amplitud y la acondiciona mediante una arquitectura de amplificación en cascada. La primera etapa realiza la amplificación de voltaje y la etapa de salida utiliza un par Darlington para proporcionar el acople de impedancias y la corriente necesaria para la carga.

## Características

- Intercomunicador de **dos nodos** con canal físico compartido.
- Micrófono **electret** caracterizado experimentalmente.
- Preamplificación mediante **BJT en emisor común**.
- Ganancia de preamplificación del orden de **×10**.
- Filtros RC pasivos para acondicionar la banda de voz.
- Banda de trabajo aproximada de **300 Hz a 3.4 kHz**.
- Etapa de salida basada en **par Darlington**.
- Carga de salida: **8 Ω**.
- Potencia calculada de aproximadamente **176 mW**, superior al mínimo requerido de 0.125 W.
- Selección del nodo transmisor mediante **pulsador mecánico**.
- **Vúmetro analógico** implementado con BJT y LEDs.
- Control de volumen mediante **potenciómetro logarítmico de 22 kΩ**.
- Segundo dispositivo con efecto de voz tipo **Fuzz** mediante saturación deliberada de una etapa BJT.
- Simulación de las etapas mediante **LTspice**.

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

El pulsador selecciona qué señal llega al canal compartido, evitando la superposición simultánea de las dos transmisiones.

## Etapas de diseño

### Caracterización del micrófono

Se caracterizó experimentalmente un micrófono electret comercial. Se obtuvo una corriente de polarización cercana a **0.2 mA** y una impedancia de salida aproximada de **4.85 kΩ**.

### Preamplificación

Se evaluaron las configuraciones fundamentales del BJT y se seleccionó el **emisor común sin bypass** para la etapa de ganancia de voltaje.

### Filtrado

Se implementaron filtros RC pasivos:

- Pasa-altos: aproximadamente **300 Hz**.
- Pasa-bajos: aproximadamente **3.4 kHz**.

### Amplificación de potencia

Se seleccionó un **par Darlington** por su elevada ganancia de corriente, alta impedancia de entrada y baja impedancia de salida. El análisis del diseño reporta aproximadamente **176 mW** sobre la carga de 8 Ω.

### Canal compartido

Los dos nodos utilizan un único canal de transmisión. Un pulsador mecánico selecciona cuál de las señales es enviada al canal.

### Módulos adicionales

- Vúmetro analógico con BJT y LEDs.
- Control de volumen logarítmico.
- Efecto Fuzz mediante saturación deliberada.
- Alimentación externa y punto medio virtual de polarización.

## Simulación

Las simulaciones se realizaron en LTspice para estudiar las diferentes etapas. El análisis incluye el comportamiento del vúmetro como indicador de sobrecarga y el recorte de la señal producido por el bloque Fuzz.

## Construcción y aprendizajes

Durante la construcción física se identificaron diferencias entre el modelo ideal y el circuito real, incluyendo la influencia de tolerancias sobre el punto Q, ruido asociado a determinadas configuraciones de bypass y la necesidad de utilizar resistencias con potencia nominal suficiente.

También se comprobó la importancia de verificar los datasheets y la distribución física de pines antes del montaje.

## Estructura

```text
emifonoIntercomunicador/
├── README.md
├── .gitignore
├── docs/
├── schematics/
│   ├── canal-1/
│   ├── canal-2/
│   └── sistema-completo/
├── simulation/
│   ├── canal-1/
│   ├── canal-2/
│   └── fuzz/
├── pcb/
├── measurements/
└── images/
    ├── prototype/
    ├── schematics/
    └── results/
```

## Autores

- Sofia Molano Martínez
- Edwin David Figueroa García
- Juan Sebastián Nieto Cruz

**Universidad Nacional de Colombia — Bogotá**  
**Electrónica Análoga I**
