# IELE756 – Preparación y Análisis de Datos
## Proyecto Final: Una Anomalía, Defendida

**Equipo:** Camilo Selaive  · Martina Motta
**Curso:** IELE756 – Leo Ferres, PhD · Mayo 2026

---

## ¿Cuáles son nuestras comunas?

El análisis cubre las comunas de la **Región Metropolitana y Valparaíso** integradas en el pipeline de Tareas 0–3 (47 comunas válidas después de filtrar el outlier de Santiago). Las comunas protagonistas de la anomalía son aquellas con **pct_foreign > media + 2 SD**, es decir, con concentración de población extranjera cercana o superior al **45 %** del total comunal.

---

## ¿Cuál es la anomalía?

Las comunas con la **mayor concentración de población extranjera** de la región presentan una tasa de Enfermedades de Notificación Obligatoria (ENO) **promedio o inferior a la esperada**, rompiendo con el supuesto epidemiológico clásico de mayor vulnerabilidad en entornos de alta densidad migrante.

El modelo Binomial Negativo confirma que el coeficiente de `pct_foreign` sobre la tasa ENO ajustada por población **no es significativo** (coef = 0.026, p = 0.166), a pesar de que el modelo Poisson —inválido por sobredispersión extrema (χ²/df ≈ 252)— sí lo marcaba como significativo. El cambio de signo interpretativo entre modelos es el núcleo de la anomalía.

---

## Notebooks y tiempo de ejecución aproximado

| Notebook | Contenido | Tiempo estimado |
|---|---|---|
| `notebooks/tarea0.ipynb` | Setup y carga inicial | < 1 min |
| `notebooks/tarea1.ipynb` | Análisis exploratorio (Census) | 1–2 min |
| `notebooks/tarea2.ipynb` | Integración ENO + GRD | 2–3 min |
| `notebooks/tarea3.ipynb` | Modelos GLM y síntesis | 3–5 min |
| `notebooks/final_anomaly.ipynb` | **Anomalía defendida** ← figura titular | **~2 min** |

La figura titular (`figs/headline.png`) se genera en la celda 3 de `final_anomaly.ipynb`.

---

## Instalación y ejecución

### Opción A — Google Colab (recomendada)

1. Abrir `final_anomaly.ipynb` en [Google Colab](https://colab.research.google.com/).
2. Montar Drive o subir los archivos fuente a la carpeta `shared/` del entorno:
   ```
   shared/census_team*.csv
   shared/eno_team*.csv
   shared/grd_team*.csv
   ```
3. Crear la carpeta de figuras:
   ```python
   import os; os.makedirs('figs', exist_ok=True)
   ```
4. Ejecutar `Runtime → Run all`.

### Opción B — Local

```bash
git clone https://github.com/[TU-USUARIO]/[TU-REPO].git
cd [TU-REPO]
pip install -r requirements.txt
# Copiar los archivos de datos a shared/
jupyter notebook notebooks/final_anomaly.ipynb
```

### requirements.txt

```
pandas>=2.0
numpy>=1.24
matplotlib>=3.7
seaborn>=0.12
statsmodels>=0.14
scipy>=1.11
jupyter
```

---

## Estructura del repositorio

```
your-repo/
├── README.md
├── requirements.txt
├── notebooks/
│   ├── tarea0.ipynb
│   ├── tarea1.ipynb
│   ├── tarea2.ipynb
│   ├── tarea3.ipynb
│   └── final_anomaly.ipynb      ← NUEVO
├── data/
│   └── download_instructions.md  (no se suben archivos CSV/parquet grandes)
└── figs/
    ├── headline.png              ← figura usada en el video
    ├── check1_healthy_migrant.png
    └── check2_underreporting.png
```

---

## Declaración de uso de IA

Este proyecto utilizó **Claude (Anthropic)** como herramienta de apoyo en las siguientes tareas específicas:

- **Estructuración del notebook `final_anomaly.ipynb`**: Claude asistió en la organización lógica de las secciones (aislamiento, figura, checks alternativos) y en la redacción de los comentarios Markdown explicativos.
- **Depuración de código**: Se consultó a Claude para resolver errores de merge con sufijos duplicados y para la correcta especificación del offset en los modelos GLM.
- **Redacción del README**: La estructura y el texto base de este archivo fueron generados con apoyo de Claude y luego revisados y ajustados por el equipo.

Todo el código fue verificado, ejecutado y validado por los integrantes del equipo. Los números, interpretaciones y conclusiones son responsabilidad exclusiva de Camilo y Martina. "Claude lo escribió" no es una defensa válida si un número es incorrecto o una afirmación no está respaldada — y estamos de acuerdo con eso.
