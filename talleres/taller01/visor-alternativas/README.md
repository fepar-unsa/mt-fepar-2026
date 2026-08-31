# Visor · Del árbol de objetivos a la alternativa de proyecto

Recurso interactivo del **Taller 01** de FEPAR 2026. Muestra, con el caso de la gestión del agua y los
efluentes en un establecimiento porcino de Rosario de Lerma, cómo se construye una alternativa de proyecto
a partir del árbol de objetivos y cómo se la compara con los indicadores de la asignatura.

## Qué contiene

Nueve pasos: el caso, el espejo problema–objetivo, los medios fundamentales, las acciones,
la clasificación de las acciones, el configurador de alternativas, la comparación financiera y multicriterio,
la Estructura Analítica y, al cierre, las trampas frecuentes con la bibliografía de respaldo.

Lo interactivo está en tres lugares:

- **Configurador de alternativas.** El alumno elige acciones y el tablero verifica en vivo que no haya
  acciones mutuamente excluyentes elegidas a la vez y que cada medio fundamental imprescindible tenga
  al menos una acción. Si falta uno, avisa que todavía no es una alternativa.
- **Evaluación financiera.** Calcula VAC, CAE, VAN y relación beneficio-costo con la TMAR y el horizonte
  que el alumno mueve. Los valores monetarios son de ejercicio, no un presupuesto.
- **Estructura Analítica dinámica.** Se rearma según la combinación elegida: cada medio cubierto se
  convierte en componente y las acciones elegidas pasan a ser sus actividades.

## Cómo publicarlo

El archivo es autónomo: un solo `index.html`, sin CDN, sin fuentes externas y sin dependencias.
Funciona igual abierto localmente que servido desde GitHub Pages.

1. Copiar la carpeta `visor-alternativas/` dentro de `talleres/taller01/` del repositorio del manual.
2. El `_quarto.yml` del proyecto ya declara `resources: - talleres/**`, así que el archivo se copia al
   sitio sin configuración adicional.
3. Publicar como siempre:

```bash
quarto render
quarto publish gh-pages
```

La dirección para compartir con los alumnos queda:

```
https://fepar-unsa.github.io/mt-fepar-2026/talleres/taller01/visor-alternativas/
```

## Cómo enlazarlo desde la página del taller

En `talleres/taller01/index.qmd` o en el HTML del taller, agregar el enlace:

```markdown
[🌳 Visor · Del árbol de objetivos a la alternativa de proyecto](visor-alternativas/)
```

Para incrustarlo dentro de la página del taller, en lugar de enlazarlo:

```html
<iframe src="visor-alternativas/" style="width:100%;height:82vh;border:1px solid #dcdbd4;border-radius:10px"
        title="Visor · Del árbol de objetivos a la alternativa de proyecto"></iframe>
```

## Cómo adaptarlo a otro escenario

Todo el contenido del caso está en el bloque `/* ================= DATOS ================= */`, al comienzo
del `<script>`. No hace falta tocar el resto del archivo.

| Constante | Qué define |
|---|---|
| `ESPEJO` | Filas de la tabla problema → objetivo. |
| `FINES` | Columnas de fines del árbol. |
| `MEDIOS` | Medios fundamentales, con `imp` (imprescindible), `rel` (excluyentes, complementarias, independiente o fuera) y `comp` (el componente en participio). |
| `ACCIONES` | Acciones por medio, con inversión `ci`, costo anual `co`, beneficio anual `b`, vida útil `vida` y los puntajes multicriterio `p`. |
| `PRESETS` | Alternativas prearmadas que aparecen en los botones y en la tabla comparativa. |
| `CRITERIOS` y `PESOS_PRESET` | Criterios no monetarios y sus configuraciones de peso. |
| `CHECKS` | Lista de autocontrol del último paso. |

Los indicadores financieros se calculan en `finanzas()` con los factores del manual: valor actual de una
serie uniforme y factor de recuperación del capital.

## Accesibilidad y compatibilidad

Navegación por teclado con flechas izquierda y derecha entre pasos, y `T` para alternar el tema.
Tema claro y oscuro, con la paleta de los escenarios y talleres de la cátedra. Diseño adaptable a pantallas
angostas. Al imprimir, se despliegan todos los pasos para obtener el recurso completo en PDF.

## Fundamentación

La construcción de alternativas sigue a Ortegón, Pacheco y Prieto, *Metodología del marco lógico para la
planificación, el seguimiento y la evaluación de proyectos y programas*, Serie Manuales 42, ILPES/CEPAL, 2005,
pp. 18-21 y 24-25; a Crespo, *Guía de diseño de proyectos sociales comunitarios bajo el enfoque del marco
lógico*, pp. 32-34; y a la Guía General del SNIP del MEF de Perú. Los indicadores de evaluación siguen el
Manual Teórico de la asignatura, capítulos de matemáticas financieras y evaluación financiera de proyectos.

---

Cátedra de Formulación y Evaluación de Proyectos Ambientales y de Recursos Naturales
Ingeniería en Recursos Naturales y Medioambiente · Universidad Nacional de Salta
