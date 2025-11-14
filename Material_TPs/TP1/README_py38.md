# TP1 — White Patch (Visión por Computadora I)

Este repositorio contiene el notebook **`TP1_white_patch_a2221-a2222-a2227.ipynb`** con las funciones y el análisis del método *White Patch* y métricas asociadas.

## 📂 Estructura
```
Material_TPs/
└── TP1/
    ├── TP1_white_patch_a2221-a2222-a2227.ipynb
    ├── requirements.txt
    └── (imágenes de prueba *.png/*.jpg, salidas *_wp_*.png)
```
> Las imágenes de ejemplo se referencian por nombres como `img1_tp.png`, `img2_tp.png`; se puede usar imágenes propias `.png/.jpg/.jpeg/.bmp/.tif/.tiff`.

## 🐍 Instalación con micromamba (recomendado)

> Reproduce el entorno sin usar `pip`.

1) Crear y activar entorno:
```bash
micromamba create -n vc1 -y
micromamba activate vc1
```

2) Instalar dependencias desde `environment.yml`:
```bash
micromamba install -f environment.yml -y
```

3) Abrir el notebook:
```bash
jupyter notebook TP1_white_patch_a2221-a2222-a2227.ipynb
```

> Notas:
> - En conda/mamba el paquete es `opencv` (no `opencv-python`).
> - Si tenés conflicto de versiones con `matplotlib`, probá fijar `<3.8` (por ej. `matplotlib=3.7.*`).
> - Si usás GPU u OpenCV con contrib, podés reemplazar `opencv` por `opencv-contrib`.

## ▶️ Uso rápido
Abrir Jupyter y ejecutar el notebook:
```bash
jupyter notebook TP1_white_patch_a2221-a2222-a2227.ipynb
```
El notebook incluye helpers para visualizar resultados y guardar salidas con patrones como:
- `{p.stem}_wp_max.png`
- `{p.stem}_wp_p{robust_p}.png`
- `{p.stem}_wp_p{rp}_auto.png`
- `{stem}_mask_{k}.png` y `{stem}_overlay.png` (si generás máscaras)

## 🧠 Funciones principales (resumen)
- `white_patch(img, p=95|99)`: aplica *White Patch* con percentil robusto.
- `pct(img)`: calcula percentiles de intensidad.
- `compute_hist(img)`: histograma para diagnóstico.
- `analyze_defects(img)`: estima `sat_pct`, `spec_pct`, `noise_pct`.
- `barplot_metric(...)`, `show_gray(...)`, `show_side_by_side_bgr(...)`: utilidades de visualización.
- `save_masks_and_overlay(...)`: exporta máscaras y overlays si corresponde.
- `md5_of_image(...)`: verificación de integridad (hash).

> Módulos usados: `numpy`, `opencv-python (cv2)`, `matplotlib`, `tabulate`. El resto (`pathlib`, `csv`, `hashlib`) son **stdlib**.

## 📈 ¿Por qué percentil robusto?
Usamos percentiles altos (95–99) para normalizar el rango dinámico **sin amplificar ruido ni reflejos especulares**. Esto evita que pocos outliers dicten la escala global. Regla adoptada:
- imágenes limpias/sintéticas → `99%`;
- imágenes reales con ruido/saturación → `95%`.

## ✅ Reproducibilidad
- El notebook fija operaciones deterministas donde aplique.
- Si se cambian imágenes/paths, verificar los nombres esperados en las celdas (e.g., `img1_tp.png`, `img2_tp.png`).

## 📝 Notas
- Si se usan datasets grandes, considera ignorar carpetas en `.gitignore`.
- Para colaborar: crear rama (`git switch -c ossie/notebook-v1`) y abrir PR.
- **Compatibilidad:** las versiones están fijadas para Python 3.8. Si actualizan a Python 3.10+, podés relajar los pines (por ejemplo `numpy>=1.25`, `matplotlib>=3.8`).

