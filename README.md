# Organigrama Studio

Herramienta de **organigramas** en un solo archivo HTML. Se abre con doble clic en cualquier
navegador: sin instalación, sin servidor y sin internet.

Nace para reemplazar el dibujo a mano en herramientas online (Lira, Canva y similares), donde la
exportación sale en imágenes de baja resolución. Aquí el organigrama se **traza solo** a partir de
la estructura que declaras, aplica las reglas de graficación de la doctrina administrativa y exporta
en **PNG hasta 8x, SVG vectorial y PDF**.

## Cómo se usa

1. Abre `organigrama.html` (doble clic). Arranca con un organigrama de ejemplo; **Nuevo** parte en
   blanco y **Ejemplo** recarga la demo.
2. Selecciona una caja y agrega unidades desde la paleta izquierda, o con el teclado:
   `Tab` = unidad subordinada, `Enter` = unidad hermana, `Supr` = eliminar.
3. Escribe el nombre en el panel derecho (o doble clic sobre la caja). El trazado se reacomoda solo:
   nunca hay que mover cajas ni alinear líneas.
   Si vas a levantar la plantilla, llena también **N.º de personas** y, si quieres el resumen
   agrupado, **Categoría de cargo** (Directivo, Administrativo, Operativo, Técnico, Médico… la que uses).
4. Para cambiar de jefe: **arrastra una caja sobre otra**, o usa "Depende de" en el panel.
5. Llena el **cajetín** (título, unidad responsable, fecha de actualización). Es lo que exige el
   criterio de vigencia y lo primero que revisa quien aprueba el documento.
6. Revisa el panel **Normativa**: marca en vivo lo que incumple y lo que ya cumple.
7. Guarda con **Guardar** (`.org.json`) o exporta a **PNG / SVG / PDF**.

Atajos: rueda = zoom · arrastrar el fondo = mover · `Ctrl+Z` / `Ctrl+Y` = deshacer/rehacer ·
`Ctrl+S` = guardar. El organigrama se autoguarda en el navegador (localStorage) en cada cambio.

## Plantilla: personas por caja y resumen

Panel **Plantilla** (derecha). Es la clasificación normativa *de puestos y plazas*: el organigrama
consigna el número de plazas de cada unidad.

- **Sello `n`** arriba a la derecha de la caja: personas en esa unidad.
- **Sello `Σn`** abajo a la derecha: total del área, sumando todas sus dependencias.
  El título se centra en el espacio libre, así que nunca se cruza con los sellos.
- **Cuadro resumen** dentro del gráfico (sale en el PNG, el SVG y el PDF): totales **por área**
  al nivel jerárquico que elijas y **por categoría de cargo**, con porcentajes.
- Las sumas **siempre cierran**: lo que no cae en el nivel de agregación elegido aparece explícito
  como "Fuera de ese nivel", y la última fila es el total de personas.
- **Padrón en CSV** (botón CSV de la barra o del panel): nivel, unidad, tipo, de quién depende,
  categoría, personas, total del área y titular. Con BOM y separador `;`, abre directo en Excel.
- El auditor avisa si hay unidades sin el dato y si el cajetín todavía declara contenido "integral"
  cuando ya estás consignando plazas.

Los tres interruptores (sellos, acumulado, cuadro resumen) se apagan si el organigrama es solo
estructural.

## Años del plan: crecimiento en un solo archivo

Un mismo archivo guarda la estructura de todos los años. El selector **Año** de la barra cambia lo
que se ve y lo que se edita; con el botón **+** se agrega el año siguiente.

- **Existe desde / Existe hasta** por unidad: las que todavía no existen no se dibujan en los años
  anteriores, y las dadas de baja desaparecen del año siguiente al que declares.
- **N.º de personas es por año**, con arrastre: declaras 2 en 2026 y 4 en 2027, y los años sin dato
  heredan el último valor declarado. El panel muestra la serie completa de la unidad seleccionada.
- Al agregar una unidad mientras ves 2027, nace con **desde 2027** sola.
- El **cajetín** rotula el año y marca `PROPUESTA` en los años posteriores al base, porque un
  organigrama futuro no es estructura aprobada: la doctrina distingue el organigrama real del
  propuesto. El auditor te avisa si el título no lo dice.
- Los archivos exportados llevan el año en el nombre (`...-2027.png`).

### Reorganizaciones: cambiar de jefe solo en un año

El organigrama grafica **cargos, no personas**. Que quien hoy es jefe pase a un puesto menor no es
"un cargo que baja": es un cargo que termina y otro que nace. Con eso, una reorganización son
cuatro movimientos, y los cuatro se declaran en el mismo archivo:

| Movimiento | Cómo |
|---|---|
| El cargo de jefe desaparece | *Existe hasta* el año anterior |
| Entra un jefe nuevo | Cargo nuevo con *Existe desde* ese año |
| Aparece el puesto menor | Cargo nuevo bajo el jefe nuevo |
| Los subordinados pasan al jefe nuevo | **Reasignación por año** |

La reasignación se hace con el año activo puesto en el año del cambio: eliges el nuevo jefe en
**Depende de**, o arrastras la caja sobre él. Se guarda solo para ese año en adelante — el año base
queda intacto. En el año base, el mismo control cambia la dependencia de todos los años.

El panel lista las reasignaciones de la unidad (`2027 → Jefe de Rendimiento`) y permite anularlas.
En el dibujo, **la línea de mando sale del color del resalte** cuando el cargo cambia de dependencia
ese año, y el cuadro de crecimiento cuenta los cargos reasignados aparte de las altas y las bajas.

Así la reorganización no infla el conteo: un jefe nuevo más un médico nuevo son **2 cargos nuevos**,
no ocho, porque los subordinados no se duplican. Y el aviso de arrastre de bajas desaparece solo en
cuanto reasignas los cargos que se mantienen.

### Cómo se resalta el crecimiento

Respecto del año anterior, en el año que estás viendo:

- **Borde grueso de color** = el cargo es nuevo ese año.
- **Sello `+n`** del mismo color, arriba a la izquierda = personas que se suman. En un cargo nuevo
  son todas; en uno existente, solo el aumento.
- **Sello `-n`** atenuado = plazas que se reducen.
- **Cuadro de crecimiento** dentro del gráfico: cargos nuevos y sus plazas, ampliación de cargos
  existentes, reducciones, bajas, cargos reasignados y el total del año.
- El color del resalte se cambia en el panel Plantilla; todo el resalte se apaga con un interruptor.
- El **CSV trae una columna de personas por año**, más *Existe desde* y *Baja en*: ese es el archivo
  para presupuestar el crecimiento en Excel.

Un archivo de un solo año se comporta como antes y no muestra nada de esto. Los `.org.json` que ya
tengas se abren sin cambios: se leen como "todo existe desde el año base".

> Cuidado con una trampa: al dar de baja un jefe, sus dependencias también dejan de aparecer. Si
> esos cargos se mantienen, reasígnalos a otro jefe; el panel de la unidad y el auditor te lo avisan.

## Escalonado: bajar una caja respecto de sus pares

Campo **Escalonado** en el panel de la unidad (0 a 4 pasos; el paso se ajusta en Presentación,
24 px por omisión). Baja la caja **sin cambiarle el nivel jerárquico**: sigue colgada de la misma
línea de su jefe, y el CSV, el cuadro resumen y el conteo de niveles la cuentan donde le corresponde.
Sirve para el caso típico de analista y asistente que reportan al mismo jefe pero no son pares.

Conviene saber qué comunica: en el organigrama **la altura significa nivel jerárquico**, así que
bajar una caja se lee como "está un nivel abajo" aunque cuelgue de la misma línea. Es práctica
extendida en empresa privada, pero no es la forma normativa. Las tres salidas correctas:

1. Si el asistente **depende del analista**, cuélgalo del analista: el desnivel es real.
2. Si **asiste al jefe** (asistencia de dirección, apoyo secretarial, recepción), es una
   **unidad de apoyo**: tipo *Asesoría interna*, adosada perpendicular a la línea de mando.
3. Si **son pares de distinto grado**, misma altura y la diferencia va dentro de la caja
   (cargo o categoría), no en la geometría.

El panel Normativa reporta el escalonado como desviación, y lo marca como incumplimiento si el
desplazamiento es tan grande que se lee como otro nivel. El botón **Normativa** trae esta misma
explicación para citarla.

## Bandas de nivel: alinear por rango del puesto

Un coordinador que reporta al gerente general no es una gerencia, y conviene que se vea. Para eso
están las **bandas**: filas horizontales que corresponden al **rango del puesto** (Gerencia,
Jefatura, Coordinación, Analista, Asistente), no a la profundidad de dependencia.

- Campo **Altura (banda)** en el panel de la unidad: la alinea a la banda que elijas. Su subárbol
  la sigue, así que los subordinados de ese coordinador caen a la altura de los analistas.
- Nunca puede quedar por encima de su jefe: la herramienta fuerza al menos una banda debajo.
- **El nivel jerárquico real no cambia.** El CSV, el cuadro resumen y el conteo de niveles siguen
  contando la unidad donde le corresponde por dependencia; solo cambia el dibujo. El CSV trae las
  dos cosas: columna *Nivel* (dependencia) y columna *Banda visual* (rango).
- **Rotula las bandas** en Presentación → *Rotular las bandas de nivel*. Los rótulos salen al margen
  izquierdo con una guía punteada. Esto es lo que hace legítima la lectura: la doctrina llama
  "niveles jerárquicos" a las bandas de rango (directivo, medio, operativo), y el organigrama es
  correcto siempre que el lector sepa qué convención se está usando.
- Sin rótulos, el panel Normativa lo reporta como desviación: la altura se leería como dependencia.

Para ajustes de pocos píxeles entre pares (analista y asistente del mismo jefe) usa **Escalonado**,
que es independiente y se suma a la banda.

## Áreas por color

Campo **Color del área** en el panel de la unidad: pinta esa unidad **y todo lo que depende de
ella**. El color se hereda, no se copia, así que si mueves una unidad a otra área toma el color
nuevo sola. `Color de esta caja` sigue existiendo y manda sobre el área.

Las áreas declaradas aparecen en la **simbología** con su color y su nombre. Si hay áreas y la
simbología está oculta, el auditor avisa: sin declarar, el color es decoración que el lector tiene
que adivinar.

Indispensable en organigramas grandes: en el del club, pintar la gerencia deportiva de un color
permite ubicarla de un golpe de vista entre 50 cajas.

## Tipos de unidad y su trazo

| Tipo | Trazo | Regla que aplica |
|---|---|---|
| Unidad de línea | continuo grueso | autoridad por una sola línea, sin flechas |
| Unidad desconcentrada | grueso, discontinuo largo con punto intermedio | distribución de autoridad |
| Unidad descentralizada | grueso, discontinuo largo con puntos | distribución de servicios |
| Asesoría interna | continuo fino perpendicular | staff que forma parte de la estructura |
| Asesoría externa | discontinuo perpendicular | staff que actúa de modo independiente |
| Consejo | discontinuo corto | adscrito al órgano de dirección |
| Comisión interna | discontinuo corto | permanente, adscrita a la dirección |
| Comisión intersectorial | discontinuo largo | representantes de otras instituciones |
| Coordinación | grueso discontinuo | integración de actividades entre unidades |

Consejos y comisiones se **reasignan solos al órgano de dirección** cuando se intenta colgarlos de
una unidad operativa, y el auditor avisa si quedan mal adscritos.

## Lo que audita el panel Normativa

Criterios de **precisión, presentación, sencillez, uniformidad y vigencia**:

- falta la unidad responsable o la fecha de actualización en el cajetín;
- fecha de actualización con más de 12 meses;
- unidades sin nombre o con nombres repetidos;
- tramo de control mayor a 7 subordinados directos;
- más de 5 niveles jerárquicos;
- consejos o comisiones no adscritos al órgano de dirección;
- unidades de asesoría con unidades de línea subordinadas;
- texto desbordado de la caja (recordando que **todas las cajas deben medir igual**);
- línea de mando demasiado fina;
- contraste texto/fondo menor a 4.5:1;
- cajas con color propio cuando está activo el candado de uniformidad;
- unidades escalonadas respecto de sus pares, y escalonado tan grande que se lee como otro nivel;
- unidades sin n.º de personas y contenido del cajetín que no corresponde a las plazas consignadas;
- unidades alineadas a otra banda sin que las bandas estén rotuladas;
- áreas coloreadas con la simbología oculta;
- año proyectado sin que el título diga que es una propuesta;
- baja de un jefe que arrastra dependencias que no declararon su propio término;
- unidades previstas para el año cuyo jefe todavía no existe;
- unidades con el mismo nombre **bajo el mismo jefe** (que "Preparador Físico" se repita en varios
  equipos es correcto y no se reporta).

Por construcción la herramienta ya garantiza: cajas de dimensión uniforme, un solo tipo de figura,
textos horizontales, grosor de línea constante en todos los niveles, sin flechas descendentes,
una sola línea por superior y niveles alineados.

**Fuente normativa:** no existe norma ISO para organigramas. Se aplica la doctrina de
Enrique B. Franklin Fincowsky, *Organización de Empresas* (McGraw-Hill), recogida en las guías
técnicas oficiales para la elaboración de organigramas (USAC 2024, Gobierno de Jalisco, IPN y
municipios de México). El botón **Normativa** de la barra superior tiene el detalle citable.

## Exportación

| Formato | Uso | Detalle |
|---|---|---|
| PNG | pegar en Word, presentaciones, WhatsApp | escala 2x a 8x; el ejemplo a 3x sale en 5934×2541 px. En organigramas muy anchos la escala se baja sola: los navegadores no dibujan más de ~16.000 px por lado |
| SVG | imprenta, seguir editando en Illustrator/Inkscape | vectorial, texto real |
| PDF | anexo de un estatuto o manual | vía diálogo de impresión, vectorial; A4/A3/Carta, vertical o apaisado |
| CSV | padrón de plazas en Excel | nivel, banda, área, unidad, jefe, categoría, vigencia y **una columna de personas por año** |
| .org.json | archivo de trabajo | estructura completa, se vuelve a abrir y editar |

Para el PDF: botón **PDF** y en el diálogo del navegador elegir "Guardar como PDF".

## Estructura del archivo `.org.json`

```
{ v, root, meta{titulo,subtitulo,unidad,fecha,aprobado,ambito,contenido},
  cfg{modo,w,h,gapH,gapN,gapS,g,fs,colores...},
  cfg{... verBandas, bandas[], pasoDesnivel, anios[], anio, verCrecimiento, colNuevoBorde},
  nodes{ id:{id,parent,tipo,titulo,titular,funciones[],lado,ord,color,areaColor,
             personas,categoria,desnivel,nivelVisual,desde,hasta,plazasAnio{},parentAnio{}} },
  rel[{a,b,tipo}], view{x,y,z} }
```

## Entrega a clientes

Al inicio del `<script>` está el bloque de compilación:

```js
const BUILD = { activo:false, caduca:"2026-12-31", ref:"SVG_LAYOUT_0x800706BE" };
```

- `activo:false` — copia maestra, sin caducidad (esta es la tuya, no la entregues así).
- `activo:true` + `caduca` — copia para el cliente. Guarda un sello de la fecha máxima vista, así
  que atrasar el reloj del equipo no revierte la caducidad.
- Los datos del cliente nunca se borran: al entregar un archivo nuevo con otra fecha, su
  organigrama reaparece intacto desde el navegador.

Antes de entregar: poner `activo:true`, fijar `caduca`, y renombrar el archivo si corresponde.

## Pendiente para una v2

- Presentación **mixta** y **de bloque** (varias unidades de la base en poco espacio).
- Plantillas de estructura (organización deportiva, pyme, institución pública).
- Foto o iniciales del titular en la caja.
- Plazas ocupadas frente a vacantes (hoy es un solo número por unidad).
- Generar los organigramas **específicos** por área a partir del general, en un clic.
- Vista comparativa de dos años lado a lado en la misma hoja.

---

**LOGIK** · marcespal91@gmail.com
