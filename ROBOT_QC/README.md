ROBOT QC - Sistema de Control de Calidad
=========================================

Sistema completo para control del robot SCORBOT-ER V plus con detección YOLO en tiempo real.

## Instalación Rápida

```bash
cd ROBOT_QC
python run.py
```

¡Eso es todo! El script `run.py` instalará automáticamente todas las dependencias si no las tienes.

## Requisitos Previos

- **Python 3.8+** (recomendado 3.10+)
- **Windows, Linux o macOS**
- Conexión **COM port** para el robot (COM6 por defecto)
- **Cámara USB** conectada
- Archivo **bestMH.pt** (modelo YOLO) en la carpeta ROBOT_QC

## Estructura

```
ROBOT_QC/
├── robot_qc_main.py         # Aplicación principal
├── robot_serial_handler.py  # Comunicación con robot
├── camera_detection.py      # Detección YOLO
├── robot_sequence_logic.py  # Lógica de secuencias
├── config.py                # Configuración centralizada
├── bestMH.pt                # Modelo YOLO ← AQUÍ
├── run.py                   # Script de inicio (RECOMENDADO)
├── requirements.txt         # Dependencias Python
├── README.md                # Este archivo
```

## Uso

###  Inicio Automático (RECOMENDADO)
```bash
python run.py
```
- ✓ Verifica e instala dependencias automáticamente
- ✓ Valida configuración
- ✓ Inicia la aplicación
```
```

## Funcionalidades

✓ **Control de Robot SCORBOT-ER V plus**
- Conecta automáticamente a puerto COM configurable
- Envío de comandos y programas
- Monitoreo de estado

✓ **Detección de Objetos en Tiempo Real**
- Modelo YOLO (bestMH.pt)
- Identificación macho/hembra

✓ **Secuencia Automática**
- 9 pasos coordenados robot + cámara
- Control de gripper
- Posicionamiento automático

✓ **Interfaz Gráfica Completa**
- Panel de control del robot
- Vista en vivo de cámara
- Registro de eventos
- Manejo de puertos COM dinámico

## Configuración

### Puerto COM del Robot
Por defecto: **COM6**

Cambiar en `config.py` o seleccionar desde dropdown en la UI

### Cámara
- Índice: Seleccionable (0, 1, 2...)
- Modelo YOLO: bestMH.pt

### YOLO (Detección)
- Input size: 640x480
- Confianza mínima: 0.5
- GPU: Disponible (si está instalada)

## Troubleshooting

### "No se pudo abrir la cámara"
- Verifica que la cámara esté conectada
- Intenta cambiar el índice (0 → 1, etc.)
- En `robot_qc_main.py`: Cambia `cv2.CAP_DSHOW` a `cv2.CAP_V4L2` en Linux

### "Puerto COM no encontrado"
- Verifica conexión del robot
- Asegúrate de tener permisos en el puerto
- En Windows: Abre Device Manager y busca el puerto

### "Modelo YOLO no encontrado"
- Copia `bestMH.pt` a la carpeta ROBOT_QC:
  ```
  ROBOT_QC/
  ├── bestMH.pt     ← Aquí (recomendado)
  ├── robot_qc_main.py
  └── ...
  ```
- O en la carpeta padre (fallback):
  ```
  Nueva carpeta/
  ├── bestMH.pt     ← También funciona aquí
  └── ROBOT_QC/
  ```

### La cámara va lenta
- Reduce CAMERA_YOLO_INPUT_SIZE en config.py: (480, 360)
- Aumenta confianza YOLO: conf=0.6
- Habilita GPU si está disponible

## Notas Técnicas

- **Threading**: Captura de video y procesamiento YOLO en threads separados
- **Optimización**: CAP_DSHOW + root.after() para máxima suavidad
- **Cola de comandos**: Evita bloqueos del robot
- **Caché de detecciones**: Detecciones estables sin parpadeos

Ver `OPTIMIZATION_NOTES.txt` para detalles técnicos.

## Dependencias Principales

```
ultralytics>=8.0.0      # YOLO
opencv-python>=4.8.0    # Visión computacional
numpy>=1.24.0           # Computación numérica
Pillow>=10.0.0          # Procesamiento de imágenes
pyserial>=3.5           # Comunicación serial
tkinter                 # UI (incluido en Python)
```
```
