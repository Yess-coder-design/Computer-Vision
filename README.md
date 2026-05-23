# Proyecto 6: Computer Vision — Reconocimiento facial para un hogar inteligente

Sistema de **reconocimiento facial en tiempo real** que identifica a la persona frente a
la cámara y, según quién sea, ejecuta acciones simuladas de un hogar inteligente. Usa
**DeepFace** con modelos preentrenados (VGG-Face), por lo que **no se entrena ninguna red
desde cero**: solo se reutiliza un modelo ya entrenado con millones de rostros.

## ¿Qué hace?

- Captura video de la webcam con **OpenCV**.
- Compara cada rostro contra una base de personas conocidas (`database_faces/`).
- Aplica la lógica del hogar según la categoría detectada:
  - **Adulto** → luces en modo relajante + música suave
  - **Niño** → modo infantil + contenido educativo
  - **Desconocido** → alerta de seguridad
- Dibuja un recuadro y etiqueta sobre cada rostro (verde = conocido, rojo = desconocido).
- Corre en bucle continuo; se sale con la tecla **`q`**.
- Maneja errores para no detenerse si no hay rostro o falla DeepFace.

## Estructura

```
.
├── reconocimiento_facial_hogar_inteligente.ipynb   # Notebook principal (paso a paso)
├── database_faces/                                  # Rostros conocidos (1 imagen por persona)
│   ├── juan.jpg     -> adulto
│   ├── maria.jpg    -> adulto
│   ├── sofia.jpg    -> niño
│   └── diego.jpg    -> niño
├── requirements.txt
└── README.md
```

## Cómo utilizarlo

### 1. Crear y activar un entorno virtual

> ⚠️ Requiere **Python 3.10–3.12** (TensorFlow aún no soporta Python 3.13+).

**macOS / Linux:**
```bash
python3.12 -m venv .venv
source .venv/bin/activate
```

**Windows (PowerShell / CMD):**
```bash
python -m venv .venv
.venv\Scripts\activate
```

Aislar el proyecto en un entorno virtual evita conflictos de versiones (DeepFace y
TensorFlow son sensibles a esto) y hace el proyecto reproducible.

### 2. Instalar dependencias

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 3. Ejecutar

1. Abre `reconocimiento_facial_hogar_inteligente.ipynb` en **VS Code** o **Jupyter** y
   selecciona el kernel del entorno virtual que creaste.
2. Agrega fotos de personas conocidas en `database_faces/` (el nombre del archivo es el
   identificador, ej. `ana.jpg`).
3. Ajusta el diccionario `PERSONAS` del notebook para mapear cada nombre a `adulto` o `nino`.
4. Ejecuta las celdas en orden. Se abrirá la webcam; sal con la tecla **`q`**.

> La primera ejecución descarga los pesos de VGG-Face (~553 MB) a `~/.deepface/weights/`.
> Es normal que tarde; las siguientes corridas son rápidas.

## Notas

- Las imágenes de `database_faces/` son rostros de prueba del dataset público de DeepFace,
  usados solo para validar el funcionamiento. Reemplázalas por tus propias fotos (con
  consentimiento) para una demo real.
- 🔐 El reconocimiento facial trata datos biométricos sensibles. Úsalo solo con el
  consentimiento de las personas involucradas y con fines educativos o legítimos.
