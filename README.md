# Selector de Materiales JARVIS

Herramienta web para **preseleccionar materiales** a partir de sus propiedades elásticas calculadas, y para **aprender** cómo se relacionan K, G, E, ν y la razón de Pugh.

Etapa 3 del proyecto de Python · Ingeniería de Materiales · Facultad de Ingeniería, UNAM · Dataset 5 (JARVIS-DFT).

**Página publicada:** `https://<usuario>.github.io/<repositorio>/`

## Para quién es

- **Ingeniería y diseño:** filtrar candidatos por rigidez, densidad, band gap y composición, y revisar qué tan confiable es cada dato antes de considerarlo.
- **Estudiantes:** entender, con valores reales, qué significan los módulos elásticos y el criterio de ductilidad de Pugh.

## Qué incluye

| Vista | Función |
|---|---|
| **Selector** | Filtros por familia química, rangos de propiedades, elementos incluidos o excluidos, confiabilidad y estabilidad. Gráfica de dispersión con ejes configurables (tipo Ashby), tabla ordenable y ficha de cada material. |
| **Calculadora elástica** | A partir de K y G calcula E, ν, K/G, λ y M, muestra el desarrollo de las fórmulas, interpreta el resultado y busca los materiales del dataset más parecidos. |
| **Guía** | Definiciones, cómo leer los indicadores y limitaciones de los datos. |

## Estructura del repositorio

```
├── index.html              Página de la herramienta (HTML + CSS + JavaScript, sin dependencias)
├── datos.js                Datos procesados, generados por el notebook
├── preparar_datos.ipynb    Limpieza y procesamiento en Python
├── Dataset_5.csv           Dataset original del curso
└── README.md
```

## Cómo se generan los datos

`preparar_datos.ipynb` (Python, pandas y numpy):

1. Convierte los faltantes `'na'` en `NaN` y las propiedades a numéricas, como en la Etapa 1.
2. Asigna la familia química con la regla de la Etapa 2.
3. Calcula E = 9KG/(3K+G), ν = (3K−2G)/[2(3K+G)], K/G y E/ρ.
4. Calcula el residuo de cada material respecto a la relación log G – log K de su familia (modelo de la Etapa 2).
5. Asigna dos indicadores:
   - **Confiabilidad del dato** (Alta, Media, Baja), según avisos como módulos no positivos, G < 5 GPa, residuo K–G atípico, Poisson reportado incoherente, baja dimensionalidad o ehull < Ef.
   - **Estabilidad** (Estable, Metaestable, Hipotético), según ehull ≤ 0.1, ≤ 0.5 o > 0.5 eV/átomo.
6. Exporta todo a `datos.js`.

Para regenerar los datos: abrir el notebook en Google Colab, ejecutar todas las celdas y reemplazar `datos.js` en el repositorio con el archivo descargado.

## Cómo usarla sin internet

Descargar el repositorio y abrir `index.html` en el navegador. No necesita servidor.

## Limitaciones

- Propiedades calculadas con DFT a 0 K, no medidas experimentalmente.
- K y G son promedios de Voigt (cota superior). Sin el tensor elástico completo no se evalúa anisotropía ni los criterios de estabilidad de Born.
- La razón de Pugh es un criterio empírico de tendencia, no una medida de ductilidad.
- Solo 1050 de los 3000 materiales tienen propiedades elásticas.

## Fuente

Choudhary, K. et al. (2018). *Elastic properties of bulk and low-dimensional materials using van der Waals density functional*. Physical Review B, 98, 014107. Datos de JARVIS-DFT (NIST).

## Equipo

- Integrante 1 —
- Integrante 2 —
- Integrante 3 —
- Integrante 4 —
