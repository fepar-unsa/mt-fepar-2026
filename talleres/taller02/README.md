# Taller 02 · De la alternativa al proceso

Conductor de clase para los **sesenta minutos** del Taller 02 de FEPAR 2026. Retoma el F01 donde quedó,
desarrolla los estudios técnicos que pide la Guía 02 y deja a los equipos trabajando en el Formulario 02.

## Los nueve bloques y su tiempo

Los cinco primeros retoman el caso desde el F01, siguiendo el orden del árbol: primero el árbol de problemas,
luego el de objetivos, después el indicador y la meta, y recién entonces las acciones y la elección de la alternativa.
Los cuatro últimos desarrollan el F02.

| # | Bloque | Minutos | Etapa |
|---|---|---|---|
| 1 | El caso y el árbol de problemas | 5 | Repaso del F01 |
| 2 | El árbol de objetivos y los medios fundamentales | 6 | Repaso del F01 |
| 3 | El indicador y la meta | 5 | Repaso del F01 |
| 4 | Las acciones y la alternativa | 7 | Repaso del F01 |
| 5 | Elegir: evaluación multicriterio | 11 | Repaso del F01 |
| 6 | Dimensionamiento | 5 | F02 |
| 7 | Acción, tarea y componente | 9 | F02 |
| 8 | Inversión, operación y cronograma | 8 | F02 |
| 9 | Recursos, consignas y dudas | 4 | F02 |
| | **Total** | **60** | |

El cronómetro de la barra superior acompaña el plan: cuenta el tiempo transcurrido y se pone en ámbar
cuando el bloque en pantalla ya debería haber cerrado. Se arranca con el botón o con la tecla `C`;
doble clic en el botón lo reinicia.

## Lo interactivo

- **Árbol de problemas completo.** Efecto final, efectos, problema central y causas, con la correspondencia explícita
  de cada causa con el medio fundamental que después se le opone.
- **Constructor de indicadores.** Los cinco elementos de la ecuación de la cátedra en campos editables: se rearma la línea
  a medida que se escribe y el visor avisa cuál de los cinco falta si se vacía uno.
- **Configurador de alternativas.** Los mismos medios fundamentales y acciones del Taller 01. Verifica en vivo que no haya
  acciones mutuamente excluyentes elegidas a la vez y que la combinación cubra los cuatro medios imprescindibles.
- **Evaluación multicriterio con normalización.** Matriz de decisión con los datos en sus unidades reales —millones de pesos,
  porcentajes, meses, escalas—; cada criterio se declara como de costo o de beneficio; se elige el método de normalización
  (mín–máx, por la suma, por el máximo o vectorial); y el visor muestra la matriz normalizada con la fórmula aplicada en cada fila, la matriz ponderada
  y el ranking. Cambiar la dirección de un criterio o el método de normalización reordena el resultado a la vista de todos.
- **Dimensionamiento en vivo.** Tres controles —caudal generado, días sin ventana de aplicación y reducción
  en origen— y el visor recalcula el indicador de tamaño, el volumen acumulado y cuánto almacenamiento nuevo
  hay que construir por encima de las fosas existentes.
- **Verificador de redacción.** El alumno escribe una acción y su componente, y el visor controla las dos
  reglas de la Guía: verbo en infinitivo en la acción, participio en el componente.
- **Clasificador de etapas.** Diez acciones del caso para asignar a inversión u operación, con corrección.
- **Gantt que se recalcula.** Cambiando la duración de una acción se corre todo lo que depende de ella,
  porque las fechas se derivan de las predecesoras y no están escritas a mano.

## Cómo publicarlo

Archivo autónomo, sin dependencias externas. Se copia la carpeta dentro de `talleres/` del repositorio,
y como el `_quarto.yml` ya declara `resources: - talleres/**`, no hace falta tocar configuración:

```bash
quarto render
quarto publish gh-pages --no-prompt
```

Enlace para compartir:

```
https://fepar-unsa.github.io/mt-fepar-2026/talleres/taller02/
```

El bloque 4 enlaza al visor del Taller 01 con una ruta relativa (`../visor-alternativas/`), de modo que
los dos recursos quedan encadenados. Si el visor del Taller 01 se mueve de lugar, hay que actualizar ese enlace.

## Cómo adaptarlo

Todo el contenido variable está en las constantes del comienzo del `<script>`:

| Constante | Qué define |
|---|---|
| `BLOQUES` | Títulos y minutos de cada bloque. Cambiar los minutos reajusta el cronómetro y la navegación. |
| `MEDIOS` y `ACC` | Medios fundamentales del árbol y acciones por medio. Alimentan el bloque 2 y el configurador del bloque 4. |
| `PRESETS` | Las tres alternativas prearmadas. |
| `CRIT` y `ALT` | Criterios de la evaluación multicriterio, con unidad, dirección (costo o beneficio) y peso; y la matriz de decisión con los valores de cada alternativa. |
| `EFECTOS` y `CAUSAS` | Ramas del árbol de problemas del bloque 1. Cada causa lleva el medio fundamental con el que se corresponde. |
| `IND` | Los cinco elementos del indicador del bloque 3, con su texto inicial. |
| `EDT` | Las acciones del F02, con código, componente, etapa, duración, predecesoras, periodicidad y tareas. Alimenta la tabla de desglose, el clasificador y el Gantt. |
| `CHECKS` | La lista de autocontrol del F02. |

Los valores del dimensionamiento están en la función `dimensionar()`, con la capacidad instalada actual
—las fosas de 670 m³— como referencia.

## Sobre la evaluación multicriterio

El Manual Teórico presenta tres métodos de normalización: por la suma, mín–máx y estandarización z-score. El visor implementa
los dos primeros, que quedan acotados entre 0 y 1 y por eso son los que se prestan a la suma ponderada; el z-score se menciona
con su limitación. A cada método se le agrega el tratamiento de la dirección del criterio, que es lo que la mayoría de los
manuales da por supuesto y los estudiantes suelen omitir:

| Método | Criterio de beneficio | Criterio de costo | Nota |
|---|---|---|---|
| Mín–máx | `(x − mín)/(máx − mín)` | `(máx − x)/(máx − mín)` | La peor alternativa recibe 0 |
| Por la suma | `x / Σx` | `(1/x) / Σ(1/x)` | Los valores suman 1; nadie recibe 0 |
| Por el máximo | `x / máx` | `mín / x` | La mejor recibe 1 |
| Vectorial | `x / √(Σx²)` | `1 − x / √(Σx²)` | La de TOPSIS |
| z-score | `(x − x̄)/s` | `(x̄ − x)/s` | No acotada; sólo se menciona |

Los cuatro primeros están implementados y se eligen desde el visor. La agregación es la suma ponderada
`S = Σ wⱼ · rᵢⱼ` con `Σ wⱼ = 1`.

El bloque 5 desarrolla además, en pantalla: los dos obstáculos que la normalización resuelve —unidades y dirección—;
las dos maneras de manejar la dirección, con la advertencia de que convertir por diferencia (`máx − x`) y por inverso (`1/x`)
no son equivalentes; el cálculo paso a paso con dos criterios del caso; por qué el método cambia el ganador; cinco reglas
prácticas; y el criterio de valor objetivo, que no es ni costo ni beneficio y se normaliza por distancia al objetivo
`r = 1 − |x − objetivo| / máx|x − objetivo|`.

## Fundamentación

Guía 02 de la cátedra, *Estudios técnicos. Las acciones y tareas de proyecto. Estructura de desglose de tareas (EDT)*:
dimensionamiento e indicadores de tamaño, redacción de acciones y componentes, etapas de inversión y operación,
las cuatro formas de vinculación entre acciones siguiendo a CEPADE — Universidad Politécnica de Madrid,
dimensión temporal y periodicidad, y determinación de recursos en las pestañas RECURSOS-I y RECURSOS-O de la
planilla de la cátedra. Formulario 02, ítems A a K.

---

Cátedra de Formulación y Evaluación de Proyectos Ambientales y de Recursos Naturales
Ingeniería en Recursos Naturales y Medioambiente · Universidad Nacional de Salta
