
# Telecom X – Parte 2: Predicción de Cancelación (Churn)

## 📌 Propósito del proyecto
Este proyecto tiene como objetivo construir un pipeline de Machine Learning para **predecir la cancelación de clientes (churn)** en Telecom X, identificando los factores más influyentes y proponiendo estrategias de retención basadas en datos.

---

## 🧠 Objetivo principal
- Predecir qué clientes tienen mayor probabilidad de cancelar (churn).
- Evaluar al menos dos modelos de clasificación.
- Interpretar variables relevantes (coeficientes / importancias).
- Proponer estrategias accionables de retención.

---

## 📂 Estructura del proyecto
- `TelecomX_Parte2_Churn.ipynb` → Notebook principal con todo el pipeline (preprocesamiento, modelos, evaluación e insights).
- `datos_tratados.csv` → Dataset tratado de la Parte 1 (limpio y estandarizado).  
  > Nota: si no está en el repositorio, ver sección “Datos”.
- `README.md` → Documentación del proyecto.
- (Opcional) `figures/` → Carpeta para guardar gráficos exportados (boxplots, correlación, etc.).

---

## 🧹 Preparación de datos
### Tipos de variables
- **Categóricas**: variables relacionadas con servicios, contrato, método de pago, etc.
- **Numéricas**: variables de antigüedad y cobros (por ejemplo: `tenure`, `MonthlyCharges`, `TotalCharges`).

### Etapas de preprocesamiento
1. **Limpieza**
   - Eliminación de columnas irrelevantes como identificadores (`customerID`).
   - Manejo de nulos (eliminación de filas sin etiqueta `churn_01`, si aplica).
2. **Codificación**
   - Variables categóricas → **One-Hot Encoding**.
3. **Estandarización / Normalización (según modelo)**
   - Modelos sensibles a escala (Regresión Logística / SVM / KNN) → **StandardScaler** en variables numéricas.
   - Modelos basados en árboles (Decision Tree / Random Forest) → no requieren escalado.
4. **Separación de datos**
   - División en entrenamiento y prueba con `train_test_split` (80/20), usando `stratify=y` para mantener la proporción de churn.

---

## 🤖 Modelización y justificaciones
Se entrenaron al menos dos modelos:

### 1) Regresión Logística (con estandarización)
- Justificación: modelo sensible a escala; el escalado evita que variables con magnitudes grandes dominen el entrenamiento.
- Ventaja: interpretabilidad mediante coeficientes (qué variables aumentan/reducen churn).

### 2) Random Forest (sin estandarización)
- Justificación: modelo basado en árboles; no depende de distancias ni escala.
- Ventaja: captura relaciones no lineales y ofrece importancia de variables.

> Nota: como el churn suele estar desbalanceado, se prioriza el análisis con métricas como Recall y F1, además de Accuracy.

---

## 📊 EDA y principales insights
Ejemplos de análisis exploratorio incluidos:
- **Matriz de correlación** (variables numéricas vs churn).
- **Boxplots** para analizar:
  - `tenure` vs churn
  - `TotalCharges` vs churn
- Tendencia típica: churn más alto en clientes con **tenure bajo** y/o **contratos mensuales (month-to-month)**.

---

## ✅ Evaluación de modelos
Métricas utilizadas:
- **Accuracy (Exactitud)**
- **Precision (Precisión)**
- **Recall**
- **F1-score**
- **Matriz de confusión**

Comparación crítica:
- Se analiza cuál modelo ofrece mejor rendimiento según el objetivo de negocio:
  - Mayor **Recall** si se busca detectar más churners (retención agresiva).
  - Mejor **F1** si se busca equilibrio entre capturar churn y reducir falsas alarmas.

---

## 🎯 Estrategias de retención propuestas
Basado en variables relevantes:
- Enfocar retención en clientes con **tenure bajo** (onboarding 30–90 días).
- Incentivar migración de **month-to-month** a contratos de 1–2 años.
- Ofrecer bundles de valor: **TechSupport + OnlineSecurity**.
- Revisar segmentación de precio para clientes con **MonthlyCharges altos**.
- Facilitar métodos de pago (incentivos para autopago).

---

## ▶️ Cómo ejecutar el proyecto
### Requisitos
En Google Colab o entorno local, instalar librerías principales:

```bash
pip install pandas numpy scikit-learn imbalanced-learn
