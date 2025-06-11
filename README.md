# RiskRadar System 🚗🔍

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/downloads/)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.5%2B-green.svg)](https://opencv.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-1.9%2B-red.svg)](https://pytorch.org/)
[![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-yellow.svg)](https://github.com/ultralytics/ultralytics)
[![License](https://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-success.svg)]()

## 📖 Descripción

**RiskRadar System** es un sistema avanzado de análisis de riesgo en tiempo real que utiliza visión por computadora, detección de objetos con YOLO y estimación de profundidad 3D para evaluar situaciones peligrosas en videos de tráfico vehicular.

### ✨ Características Principales

- 🎯 **Detección Multi-Modelo**: Combina YOLOv8 personalizado y COCO para máxima precisión
- 🌊 **Análisis de Profundidad 3D**: Integración con MiDaS para estimación de distancias
- 🔥 **Mapa de Calor Dinámico**: Visualización en tiempo real de zonas de riesgo
- 📊 **Seguimiento de Objetos**: Sistema de tracking CSRT para continuidad temporal
- 📈 **Reportes Automáticos**: Generación de estadísticas y visualizaciones
- ⚡ **Optimización GPU**: Soporte completo para aceleración CUDA

## 🚀 Instalación

### Prerrequisitos

```bash
Python >= 3.8
CUDA >= 11.0 (opcional, para aceleración GPU)
```

### Dependencias

```bash
pip install torch torchvision
pip install ultralytics
pip install opencv-python
pip install numpy matplotlib
pip install timm  # Para MiDaS
```

### Instalación Rápida

```bash
git clone https://github.com/tu-usuario/DepthRiskRadar.git
cd riskradar-system
pip install -r requirements.txt
```

## 🎮 Uso

### Configuración Básica

1. **Preparar Modelos**:
   - Coloca tu modelo YOLOv8 personalizado en la ruta especificada
   - El modelo COCO se descarga automáticamente

2. **Configurar Rutas**:
```python
config = {
    'MODEL_PATH_VEHICLES': 'ruta/a/tu/modelo.pt',
    'VIDEO_INPUT_PATH': 'ruta/a/tu/video.mp4',
    'OUTPUT_DIR': 'resultados/'
}
```

3. **Ejecutar**:
```bash
python risk_radar.py
```

### Ejemplo de Uso

```python
from risk_radar import RiskRadarSystem

# Configuración personalizada
config = {
    'YOLO_CONFIDENCE_THRESHOLD': 0.40,
    'PROCESS_EVERY_N_FRAMES': 5,
    'HEAT_THRESHOLD_HIGH': 80.0
}

# Inicializar y procesar
radar = RiskRadarSystem('output/', config)
radar.process_video()
```

## 📊 Salidas del Sistema

### Archivos Generados

| Archivo | Descripción |
|---------|-------------|
| `output_risk_radar.mp4` | Video procesado con anotaciones |
| `detections_raw.json` | Datos completos de detecciones |
| `detections_raw.csv` | Detecciones en formato tabular |
| `statistics_report.json` | Estadísticas detalladas |
| `analysis_charts.png` | Gráficos de análisis |
| `processing_log.txt` | Log completo del procesamiento |

### Métricas de Riesgo

- 🟢 **Riesgo Bajo**: Objetos distantes (>4m)
- 🟡 **Riesgo Medio**: Objetos cercanos (1.5-4m)
- 🔴 **Riesgo Alto**: Objetos muy cercanos (<1.5m)

## ⚙️ Configuración Avanzada

### Parámetros Principales

```python
config = {
    # Modelos y entrada
    'MODEL_PATH_VEHICLES': 'modelo_personalizado.pt',
    'VIDEO_INPUT_PATH': 'video.mp4',
    
    # Procesamiento
    'PROCESS_EVERY_N_FRAMES': 5,  # Procesar cada N frames
    'PROCESSING_RESOLUTION': (960, 540),  # Resolución de procesamiento
    
    # Detección
    'YOLO_CONFIDENCE_THRESHOLD': 0.40,
    'NMS_IOU_THRESHOLD': 0.6,
    
    # Análisis 3D
    'CALIBRATION_DISTANCE_METERS': 2.5,
    'RISK_ZONES_METERS': {'HIGH': 1.5, 'MEDIUM': 4.0},
    
    # Mapa de calor
    'HEAT_THRESHOLD_HIGH': 80.0,
    'HEATMAP_DECAY_RATE': 0.90
}
```

### Clases Detectadas

- **Vehículos**: car, bus, truck, van, motorbike, threewheel
- **COCO**: person, bicycle, dog

## 🏗️ Arquitectura

```
RiskRadarSystem
├── Detección (YOLO + COCO)
├── Tracking (CSRT)
├── Estimación 3D (MiDaS)
├── Análisis de Riesgo
│   ├── Mapa de Calor
│   ├── Zona de Interés (Cono)
│   └── Clasificación de Riesgo
└── Visualización y Reportes
```

## 📈 Rendimiento

| Métrica | Valor Típico |
|---------|--------------|
| FPS (GPU) | 15-25 FPS |
| FPS (CPU) | 3-8 FPS |
| Precisión | >85% |
| Resolución Soportada | Hasta 4K |

## 🤝 Contribuciones

¡Las contribuciones son bienvenidas! Por favor:

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📝 Roadmap

- [ ] Soporte para múltiples cámaras
- [ ] Integración con bases de datos
- [ ] API REST
- [ ] Detección de eventos específicos
- [ ] Optimización para edge computing

## 🐛 Issues Conocidos

- Requiere calibración manual para diferentes tipos de cámara
- El modelo MiDaS puede ser lento en CPUs antiguos
- Sensible a condiciones de iluminación extremas

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para detalles.

## 🙏 Agradecimientos

- [Ultralytics](https://github.com/ultralytics/ultralytics) por YOLOv8
- [Intel ISL](https://github.com/intel-isl/MiDaS) por MiDaS
- Comunidad OpenCV por las herramientas de visión por computadora

## 📞 Contacto

- **Autor**: Jorge Ortiz
- **GitHub**: [@ocjorge](https://github.com/ocjorge)

---

⭐ **¡Si este proyecto te resulta útil, no olvides darle una estrella!** ⭐
