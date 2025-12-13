# 🏃‍♂️ Detección y Seguimiento de Objetos en Video (SportsMOT)

**Trabajo 4 - Visión por Computador**  
**Universidad Nacional de Colombia - Facultad de Minas**

## 📋 Descripción del Proyecto

Pipeline de visión por computador que combina detección con YOLO y seguimiento multi-objeto con dos enfoques: IoU tracker y Optical Flow + asociación. Se trabaja sobre el dataset **SportsMOT** para ilustrar seguimiento en secuencias deportivas.

## 🎯 Objetivos

- Ejecutar detección de objetos en video con un modelo YOLO preentrenado.  
- Implementar trackers sencillos (IoU y flujo óptico) para mantener IDs entre frames.  
- **Analizar y visualizar trayectorias** de movimiento de jugadores y balón.
- Calcular **métricas de movimiento** (velocidad, distancia, aceleración).
- Generar **mapas de calor** de actividad en el campo.
- Evaluar cuantitativamente (MOT metrics) y comparar métodos de tracking.
- Documentar el proceso en notebooks reproducibles.

## 📊 Dataset

- **SportsMOT**.  
- Formato MOTChallenge: `img1/` con frames, `gt/gt.txt`, `seqinfo.ini`.  
- Descarga/organización esperada:
  ```
  data/
    dataset/
      train/val/test/<sequence>/img1
      train/val/test/<sequence>/gt/gt.txt
      train/val/test/<sequence>/seqinfo.ini
    detections_yolo/    # CSV de detecciones YOLO
    tracks_iou/         # CSV de tracks con IoU tracker
    tracks_of/          # CSV de tracks con Optical Flow
    splits_txt/         # Listas de secuencias por split
  ```
  La descarga puede hacerse manualmente desde el repo del dataset. Asegura suficiente espacio (~36 GB si se descargan los tres tars completos).

## 🏗️ Estructura del Proyecto

```
Deteccion_Seguimiento_Objetos_Video/
├── README.md
├── requirements.txt
├── data/
│   ├── dataset/            # Secuencias SportsMOT (MOT format)
│   ├── detections_yolo/    # Salidas de YOLO (*.csv)
│   ├── tracks_iou/         # Salidas tracker IoU (*.csv)
│   ├── tracks_of/          # Salidas tracker Optical Flow (*.csv)
│   ├── trajectories/       # Análisis de trayectorias y mapas de calor
│   └── splits_txt/         # Archivos de splits (train/val/test)
├── notebooks/
│   ├── 00_environment_check.ipynb
│   ├── 01_eda_sportsmot.ipynb
│   ├── 02_yolo_detection_baseline.ipynb
│   ├── 03_tracking_baseline_iou.ipynb
│   ├── 04_tracking_optical_flow.ipynb
│   └── 05_trajectory_comparison.ipynb
└── reports/                # Reporte técnico / figuras / video
```

## 🛠️ Instalación y Configuración

### Requisitos Previos

- **Python 3.10+** (recomendado 3.11 o 3.12)
- **Anaconda/Miniconda** (opcional)
- Cuenta de Hugging Face si usas descarga autenticada (para los tars grandes).

### macOS / Linux

```bash
git clone https://github.com/tu-usuario/Deteccion_Seguimiento_Objetos_Video.git
cd Deteccion_Seguimiento_Objetos_Video

python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

python -m ipykernel install --user --name=.venv --display-name "Python (SportsMOT)"
jupyter notebook  # o jupyter lab
```

### Windows

```cmd
git clone https://github.com/tu-usuario/Deteccion_Seguimiento_Objetos_Video.git
cd Deteccion_Seguimiento_Objetos_Video

python -m venv .venv
.venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt

python -m ipykernel install --user --name=.venv --display-name "Python (SportsMOT)"
jupyter notebook
```

## 🚀 Uso y orden de notebooks

1) `00_environment_check.ipynb` – Verifica versiones y dependencias.  
2) `01_eda_sportsmot.ipynb` – Explora estructura MOT, secuencias y anotaciones.  
3) `02_yolo_detection_baseline.ipynb` – Corre YOLOv8 preentrenado sobre una secuencia y guarda detecciones en `data/detections_yolo/`. Ajusta modelo, conf, iou, device si es necesario.  
4) `03_tracking_baseline_iou.ipynb` – Carga detecciones, aplica IoU tracker, guarda tracks en `data/tracks_iou/`, evalúa con motmetrics, visualiza y **analiza trayectorias**.  
5) `04_tracking_optical_flow.ipynb` – Combina detecciones + flujo óptico para asociación, guarda tracks en `data/tracks_of/`, compara métricas con IoU y **visualiza trayectorias avanzadas** con análisis de movimiento, mapas de calor y estadísticas.
6) `05_trajectory_comparison.ipynb` – **Comparación detallada** entre trayectorias de IoU y Optical Flow: análisis de fragmentación, suavidad, cobertura temporal y visualizaciones comparativas.

Notas:  
- Las notebooks asumen que existe al menos un CSV de detecciones en `data/detections_yolo/`.  
- Si quieres procesar múltiples secuencias, itera la celda de inferencia en `02_yolo_detection_baseline` y ejecuta 03/04 por cada CSV.  
- Asegura que los nombres de archivo sigan el patrón `<sequence>_<modelo>_<step>.csv` para que los notebooks deduzcan la secuencia.

## 📈 Resultados (pendiente de consolidar)

- Métricas MOT (MOTA, IDF1, FP/FN/IDs) para IoU vs Optical Flow en secuencias de train/val.  
- Ejemplos visuales de tracks e IDs sobre frames de SportsMOT.  
- (Próximo) Tabla agregada y figuras en `reports/`.

## 🧪 Tecnologías

| Categoría                 | Tecnologías                    |
|---------------------------|--------------------------------|
| Detección                 | Ultralytics YOLOv8             |
| Tracking                  | IoU tracker, Optical Flow (cv2)|
| Evaluación MOT            | motmetrics                     |
| Procesamiento / Datos     | OpenCV, NumPy, pandas          |
| Visualización             | matplotlib, seaborn            |
| Notebooks                 | Jupyter, IPython               |
| Descarga dataset          | huggingface_hub (opcional)     |

## 👥 Equipo
**Grupo:**  Grillo Digital
**Integrantes:**

Juan Pablo Palacio Pérez - juppalaciope@unal.edu.co
David Giraldo Valencia - dgiraldova@unal.edu.co
Andrés Felipe Moreno Calle - amorenocal@unal.edu.co
Víctor Manuel Velásquez Cabeza - vivelasquezc@unal.edu.co 

## 📄 Licencia y contexto académico

Proyecto académico para la asignatura Visión por Computador, Universidad Nacional de Colombia. Uso educativo. 
