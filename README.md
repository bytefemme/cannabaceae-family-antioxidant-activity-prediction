# Modelado QSAR para la Predicción de Actividad Antioxidante en Cannabaceae

Este repositorio contiene el desarrollo de modelos de Relación Estructura-Actividad Cuantitativa (QSAR) diseñados para predecir la actividad antioxidante ($Log_{10} EC_{50}$) de moléculas derivadas de la familia *Cannabaceae* y otros compuestos químicos.

## 📌 Descripción del Proyecto
El objetivo principal es implementar una estrategia de modelado basada en la segmentación de datos por niveles de potencia (Alta, Media y Baja actividad) y el uso de **Modelos de Mezcla Gaussiana (GMM)** para mejorar la precisión predictiva mediante sub-modelos especializados.

## 🛠️ Metodología y Tecnologías

### Herramientas Principales
- **RDKit**: Para el manejo de estructuras químicas y generación de descriptores.
- **Scikit-Learn**: Implementación de algoritmos de Machine Learning y preprocesamiento.
- **Gaussian Mixture Models (GMM)**: Utilizados para el clustering basado en la distribución de la actividad biológica.

### Descriptores Químicos Utilizados
Para capturar las características estructurales y fisicoquímicas se emplearon:
- Huellas moleculares (**Fingerprints**): ECFP4, ECFP6 y MACCS.
- Descriptores fisicoquímicos básicos.

### Algoritmos de Regresión
Se evaluaron y compararon diversos modelos ensemble:
- Random Forest (RF)
- Extra Trees (ET)
- Gradient Boosting (GB)
- Support Vector Regression (SVR)

## 📁 Estructura de los Notebooks

El proyecto se divide en tres flujos de trabajo principales según el umbral de actividad ($Log_{10} EC_{50}$ en nM):

1.  **Alta Actividad (`Alta_Actividad_reclasificado.ipynb`)**
    - **Umbral**: $Log_{10} \leq 4.5$.
    - **Estrategia**: Modelo ensemble directo (90.5% unimodal) tras eliminación de outliers.
    - **Clustering**: GMM con $n=3$ para análisis de densidad.

2.  **Media Actividad (`Media_Actividad_reclasificado.ipynb`)**
    - **Umbral**: $Log_{10} \leq 4.5$ (v3 con refinamiento GMM).
    - **Clustering**: Identificación de 3 clusters óptimos basados en el criterio BIC.

3.  **Baja Actividad (`Baja_Actividad_reclasificado.ipynb`)**
    - **Umbral**: $Log_{10} > 5.5$.
    - **Estrategia**: Creación de 2 sub-modelos específicos:
        - **Cluster 0**: Zona densa (5.5–6.3).
        - **Cluster 1**: Zona esparsa (6.3–7.8).

## 🚀 Resultados
Los modelos han demostrado un alto rendimiento, alcanzando coeficientes de determinación ($R^2$) globales de hasta **0.86** en conjuntos de prueba, lo que permite una identificación confiable de moléculas con potencial antioxidante.

## 📋 Requisitos
Para ejecutar los notebooks, asegúrate de tener instaladas las siguientes librerías:
```bash
pip install rdkit pandas numpy matplotlib seaborn scikit-learn
```

**Autora:** Nathalia Bonilla Lozada

**Institución:** Universidad Icesi

**Proyecto:** Tesis de Grado - Química Farmacéutica
