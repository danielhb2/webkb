# Mi Kanban

[🇬🇧 English version](README_EN.md)

![Version](https://img.shields.io/badge/versión-1.0-blue) ![Language](https://img.shields.io/badge/lenguaje-HTML5%20%2F%20JS-orange) ![License](https://img.shields.io/badge/licencia-GPL--3.0-green) ![Status](https://img.shields.io/badge/estado-estable-brightgreen)

---
Tablero Kanban personal que funciona completamente en el navegador, sin servidor ni base de datos. Todos los datos se guardan localmente en el dispositivo, pudiendo exportar a un archivo .json.  
¡SÓLO TRES ARCHIVOS! (115kb)  
Podés subir los archivos a tu servidor o usarlo desde tu PC, localmente. O ambas cosas a la vez.

---

## Requisitos

- Navegador moderno (Firefox, Brave, Chrome, Pale Moon)
- Los siguientes archivos deben estar en el mismo directorio:
  - `index.html`
  - `marked.min.js` (v9.x recomendada)
  - `tucan.png`
  - `README.md - opcional, incrustado en index.html`

---

## Estructura del tablero

El tablero se organiza en **columnas** que contienen **tareas**. Cada tarea puede tener **notas** con formato Markdown.

### Columnas

- Se crean desde el menú lateral (☰)
- Se pueden **renombrar** haciendo doble clic en el nombre de la columna
- Se pueden eliminar con el botón 🗑️ del encabezado
- Al eliminar una columna se eliminan también sus tareas
- Cada columna muestra un **contador** con la cantidad de tareas visibles
- El color de cada columna es **personalizable** con una paleta de 8 colores (botón 🎨 en el encabezado de la columna). El color elegido se guarda en el JSON y persiste entre sesiones.
- El botón ➕ en el encabezado abre un modal para agregar una tarea directamente a esa columna

### Tareas

- Se crean desde el menú lateral o con el botón ➕ de cada columna
- Se pueden mover entre columnas arrastrando (escritorio) o con pulsación larga (~400ms) en móvil
- Se pueden **reordenar dentro de la misma columna** arrastrando una tarea sobre otra
- Admiten **etiquetas** separadas por comas para clasificarlas
- Las etiquetas con nombres reservados tienen estilo visual especial automático:
  - `urgente` / `urgent` → texto blanco sobre fondo rojo
  - `importante` / `important` → texto amarillo sobre fondo verde
- Admiten una **fecha de vencimiento** con indicador de color:
  - 🟢 Verde: vence hoy o en más de 3 días
  - 🟡 Amarillo: vence en 1 a 3 días
  - 🔴 Rojo: vencida
- Se editan con el botón ✎ y se eliminan con 🗑️

### Notas

- Cada tarea puede tener múltiples notas con contenido en **Markdown**
- Las notas se muestran colapsadas bajo la tarea y se expanden al hacer clic en su título
- Cada nota guarda su **fecha de creación**, que se muestra junto al título
- Al guardar una nota aparece un **aviso de confirmación** (o de error si el contenido está vacío)
- El modal de edición permanece abierto tras guardar, para continuar editando

---

## Búsqueda y filtros

- El campo de búsqueda en el encabezado filtra en tiempo real por título, etiquetas y contenido de notas
- Hacer clic en una etiqueta filtra todas las tareas que la compartan
- Cuando hay un filtro activo, se muestra una **barra indicadora** debajo del encabezado con el filtro aplicado y un botón ✕ para quitarlo
- Al filtrar, las columnas sin resultados **se ocultan** automáticamente
- Ambos filtros (búsqueda y etiqueta) son acumulables

---

## Editor de Markdown

La barra de herramientas del editor de notas incluye:

| Botón | Función |
| :--- | :--- |
| Hn | Encabezados H1, H2, H3 |
| B | Negrita (`**texto**`) |
| *I* | Cursiva (`*texto*`) |
| Cód | Bloque de código (` ``` `) |
| ` | Código inline |
| List | Lista con viñetas (`- item`) |
| ☐ | Checklist (`- [ ] item` / `- [x] item`) |
| " | Cita (`> texto`) |
| 🔗 | Link (`[texto](url)`) |
| ⊞ | Tabla con plantilla de 3 columnas |
| — | Separador horizontal (`---`) |

### Tablas

La plantilla insertada por ⊞ incluye la línea de separadores con alineación:

```
| Col1 | Col2 | Col3 |
| :--- | :---: | ---: |
| izq  | centro | der |
```

> La línea de separadores (`| --- |`) es obligatoria. Sin ella el texto no se renderiza como tabla.

### Checklists

```
- [ ] Tarea pendiente
- [x] Tarea completada
```

Los ítems completados se muestran en verde. El estado se cambia editando la nota.

---

## Backup

Desde la sección **Backup** del menú lateral:

- **Exportar JSON**: descarga un archivo con todos los datos del tablero, con marca de tiempo en el nombre
- **Importar JSON**: carga un backup previamente exportado, reemplazando los datos actuales

> Se recomienda exportar regularmente. Los datos se guardan en el `localStorage` del navegador y pueden perderse si se borra el historial o la caché.

---

## Notas técnicas

- Sin dependencias externas en tiempo de ejecución (todo local)
- Markdown renderizado por [marked.js](https://marked.js.org/) v9.x con soporte GFM completo
- Compatible con Firefox, Brave, Chrome y Pale Moon
- El drag & drop en móvil usa pulsación larga (~400ms) para no interferir con el scroll
- Los datos persisten en localStorage con un wrapper de compatibilidad para Pale Moon
- La Content Security Policy bloquea explícitamente conexiones de red externas

La idea detrás del uso de localStorage con la capacidad de exportar e importar en formato .json es facilitar la portabilidad sin depender de servidores o backends complejos: el localStorage actúa como almacenamiento de trabajo inmediato, mientras que el archivo .json es el mecanismo de persistencia real a largo plazo.

---
**Problema con Pale Moon (archivo local)**: al cargar la página puede producirse un intento de conexión a direcciones internas (como 0.0.0.2). Es un comportamiento del navegador, no de la aplicación, y no afecta el funcionamiento ni la privacidad. No ocurre al acceder desde un servidor web.

---

## Ideas

- 📂 Podés crear backups en carpetas específicas para distintos proyectos y así tener varios proyectos en desarrollo y a mano.
- 📄 Podés crear columnas para notas de distinto carácter.
- 🗃️️ Podés usar Dropbox o Google Drive para sincronizar tus datos estés donde estés.
- Para las columnas: Ideas, En progreso, Finalizadas, Descartadas, Notas, etc.

---

## Créditos

**Código y desarrollo**
Claude Sonnet (Anthropic) — arquitectura, implementación, corrección de bugs y compatibilidad cross-browser

**Diseño, concepto y dirección**
[Daniel Horacio Braga](https://orquidealucinada.net) — diseño visual, definición de funcionalidades, testing en múltiples plataformas (Firefox, Brave, Pale Moon, móvil), y feedback iterativo

**Dependencias**
- [marked.js](https://marked.js.org/) — parser de Markdown, licencia MIT

---

## Licencia

**Mi Kanban** — Copyright © 2026 [Daniel Horacio Braga](https://orquidealucinada.net)

Este programa es software libre: podés redistribuirlo y/o modificarlo bajo los términos de la **Licencia Pública General de GNU (GPL)**, versión 3 o posterior, publicada por la Free Software Foundation.

Este programa se distribuye con la esperanza de que sea útil, pero **SIN NINGUNA GARANTÍA**; sin siquiera la garantía implícita de COMERCIABILIDAD o IDONEIDAD PARA UN PROPÓSITO PARTICULAR. Consulte la Licencia Pública General de GNU para más detalles.

Deberías haber recibido una copia de la Licencia Pública General de GNU junto con este programa. Si no, consultá [https://www.gnu.org/licenses/](https://www.gnu.org/licenses/).

> Nota: la licencia GPL aplica al código fuente de **Mi Kanban**. La librería **marked.js** se distribuye bajo su propia licencia MIT, que es compatible con GPL.

## Video


🎬 [![video 1](images/video1.png)](https://orquidealucinada.net/webkb/video1.webm)

🎬 [![video 1](images/video1.png)](https://orquidealucinada.net/webkb/video2.webm)


