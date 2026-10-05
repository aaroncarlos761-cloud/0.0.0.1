# Monitor de Contratación ESAP — SECOP II

Página de una sola pieza que consulta en vivo los datos abiertos de contratación
pública de Colombia y presenta la contratación de la ESAP para seguimiento de veeduría.

No tiene servidor, ni base de datos, ni costo. Cada vez que se abre o se cambia un
filtro, el navegador pregunta directamente a `datos.gov.co` y pinta lo que hay en ese
momento.

## Qué muestra

**Novedades.** Compara los contratos firmados en los últimos 120 días contra los que ya
estaban registrados en el navegador la última vez que se abrió. Detecta también los
cargues tardíos: un contrato firmado en mayo que la entidad sube a SECOP en septiembre
aparece como novedad, porque la comparación es por identificador de contrato y no por
fecha.

**Nuevos por monto.** Los contratos firmados en una ventana de 9 a 365 días, repartidos en ocho
rangos de valor con conteo y monto por rango, más un rango propio desde/hasta, fichas de resumen,
tabla ordenable con banderas rojas y CSV del rango.

**Banderas rojas.** Veintisiete reglas de detección aplicadas a cada contrato y a cada proceso,
con severidad crítica, alta o media. Se explican una por una más abajo y en la pestaña de
Metodología del propio sitio, con la fuente de cada una. Se puede filtrar por regla y exportar
lo marcado a CSV con la explicación incluida.

**Vencimientos y modalidades.** Los contratos en ejecución que terminan dentro de 30, 60 o 90
días, útil para pedir informes de supervisión a tiempo, con un filtro por tipo de señal que solo
ofrece las banderas que de verdad aparecen en esa ventana, cada una con su conteo, más una opción
para ver los que no activaron ninguna. Al filtrar, la página explica la regla escogida y su fuente,
y el CSV baja exactamente lo filtrado. Abajo, el reparto por modalidad de contratación del periodo.

**Caso BOG-1481-2025.** El expediente que la veeduría tiene abierto, en una sola pestaña:
el plazo original de setenta y ocho días frente a los 303 adicionados, la línea 1273 del Plan
Anual de Adquisiciones 2025 que tenía este contrato previsto para junio, las tres modificaciones
con la hora en que se crearon y se aprobaron, las seis facturas, los siete módulos que entraron
por adición y lo que el expediente respalda a favor de la entidad. Abajo, la tabla de las tres
peticiones con su radicado y su vencimiento, para llenar el día que se radiquen. Todo con la
fuente a la vista y sin calificar el contrato: prorrogar y adicionar es legal, y eso está dicho
en la propia pestaña.

**Historial en la ficha.** Al abrir la ficha de cualquier contrato aparece su historial de
modificaciones: cuándo se creó y se aprobó cada una, el plazo antes y después, el valor antes y
después, el propósito que registró la entidad y cuáles se tramitaron al vencimiento.

**Carga del contratista.** En la ficha de cualquier contrato hay un botón que busca, en todas las
entidades del país, qué otros contratos tenía el contratista vigentes el día que firmó y cuáles firmó
mientras lo ejecutaba. Si es un consorcio o una unión temporal, lo abre en sus integrantes con el
conjunto «Grupos de Proveedores» (`ceth-n4bn`) y busca los contratos de todos los consorcios donde
aparezca alguno de ellos; el valor ponderado cuenta solo la parte que les toca según su participación.
Dice además cuál era su contrato más grande antes de este. Sirve para ver si un contrato le quedaba
grande a alguien por carga simultánea. No reemplaza el cálculo de capacidad residual del pliego, y no
usa el valor pagado porque muchas entidades no lo actualizan. Salió del caso BOG-1363-2025.

**Aviso de fuente incompleta.** datos.gov.co recarga el conjunto de contratos una vez al día y
mientras lo hace puede quedar con unas pocas filas. El 23 de septiembre de 2026 tuvo 1.000 registros
para todo el país durante horas. Si al abrir el monitor la fuente tiene menos de 200.000 registros,
aparece un aviso arriba para que nadie tome un cero por dato.

**Metodología.** Qué detecta cada regla, por qué importa, de dónde sale y qué no puede ver este
monitor. Está dentro del sitio para que cualquiera pueda auditar el criterio.

**Buscar contratista.** Se escribe un nombre, parte de un nombre o un documento y sale la ficha
completa de esa persona o empresa: cuántos contratos tiene con la ESAP en todo el histórico, por
cuánto valor, cuántos están en curso hoy y cuántos vencen en los próximos sesenta días, desde
cuándo contrata y hace cuántos años, con qué sedes, por qué modalidades le adjudican, qué tipos de
contrato firma, quién le ha supervisado, qué banderas rojas acumula y un gráfico de contratos por
año. Esta búsqueda ignora a propósito el rango de fechas de los filtros de arriba, porque lo que
interesa es la trayectoria completa. Al nombre de cualquier contratista se le puede hacer clic
desde cualquier tabla del sitio para llegar a su ficha.

**Contratos.** La tabla completa con filtros por sede, fechas, modalidad, tipo y texto
libre sobre el objeto o el contratista.

**Contratistas repetidos.** Agrupado por documento, así que una misma persona con
contratos en varias sedes aparece una sola vez y sumada.

**Procesos.** La etapa anterior al contrato, que es donde una veeduría todavía alcanza a
incidir. La columna de invitados frente a respuestas deja ver cuánta competencia hubo de
verdad.

**Seguimiento.** Cualquier contrato, contratista o proceso se marca con la estrella y
queda fijado. La lista vive en el navegador del equipo, no se sube a ningún lado.

## Datos de identidad

Los documentos de contratistas personas naturales se muestran enmascarados
(`1013****76`). El número completo se sigue usando internamente para agrupar los
contratos de una misma persona, así que el análisis no pierde precisión. Los NIT de
empresas y entidades se muestran completos porque no son dato personal. Quien necesite
verificar un documento lo encuentra en el expediente oficial de SECOP, enlazado en cada
fila.

## Banderas rojas

El monitor evalúa veintisiete reglas de detección sobre cada contrato y cada proceso, y marca los
registros que merecen que alguien abra el expediente. Una bandera es un indicio, nunca una prueba.

Las tipologías de corrupción vienen del documento «Tipologías de corrupción en Colombia, Tomo III»
de la Fiscalía General de la Nación: fraccionamiento, objeto acomodado, direccionamiento, colusión,
alteración de modalidades, apropiación del anticipo, supervisor desleal y adiciones irregulares.

Los criterios de cálculo vienen de la guía «Red flags in public procurement» de la Open Contracting
Partnership, edición de 2024, que cataloga setenta y tres banderas rojas para datos de contratación.
De ese catálogo se implementaron las que se pueden calcular con los campos que SECOP II publica.

Los umbrales numéricos se calibraron contra los datos reales de la ESAP para que cada regla marque
lo excepcional y no lo cotidiano. Por ejemplo: el 16 % de los contratos de la entidad figura como
«modificado», así que esa condición sola no sirve de alarma; en cambio solo el 1,1 % tiene más de
noventa días de prórroga, y ese sí es un umbral que separa.

### Reglas sobre contratos

| Severidad | Regla | Qué detecta |
|---|---|---|
| Crítica | Valor imposible | Contrato por más de cien mil millones de pesos |
| Crítica | Se pagó más de lo contratado | Valor pagado superior al valor del contrato |
| Crítica | Empezó antes de firmarse | Fecha de inicio anterior a la fecha de firma |
| Crítica | Contratista sin identificar | Contratista «Sin Descripción» o documento «No definido» |
| Alta | Contratista sin documento registrado | El contrato no trae documento del contratista |
| Alta | Posible fraccionamiento | Dos o más contratos al mismo contratista, misma entidad, mismo día |
| Alta | Valor atípico para su tipo | Más de veinte veces el promedio de su tipo de contrato |
| Alta | Contratista recurrente | Cinco o más contratos en el periodo consultado |
| Alta | Prórroga extensa | Más de noventa días adicionados al plazo |
| Alta | Contrato con anticipo | Cualquier pago adelantado, que en la ESAP es rarísimo |
| Alta | Contrato cedido | El que firmó no fue el que ejecutó |
| Media | Publicado sin valor | Contrato con valor cero |
| Media | Sin fecha de firma | Registro no atribuible a ninguna administración |
| Media | Sin supervisor designado | Campo de supervisor vacío o «No definido» |
| Alta | Prórrogas encadenadas | Dos o más modificaciones publicadas que amplían el plazo |
| Media | Prórroga al vencimiento | Modificación de plazo creada entre dos días antes y un día después del vencimiento |
| Media | Adición cerca del tope | El valor subió 40 % o más sobre el inicial (el tope legal es 50 %) |
| Media | Pasa de vigencia | Pactado para terminar en la segunda quincena de diciembre y prorrogado al año siguiente |
| Alta | Solo anticipo | Obra, interventoría o consultoría vencida y sin cerrar donde lo pagado es exactamente el anticipo, o una fracción redonda del valor (10 %, 15 %, 20 %…) |
| Alta | Vencido y sin liquidar | Obra, interventoría o consultoría que exige liquidación, cuyo plazo para liquidar ya pasó y sigue abierta |

Las cuatro últimas salieron del caso BOG-1481-2025. Tres de ellas se calculan con el conjunto
«Modificaciones a contratos» (`u8cx-r425`), que el monitor consulta aparte, por lotes de 40, solo
para los contratos que tienen días adicionados o figuran como modificados, y pidiendo únicamente la
versión 1 de cada modificación (el antes) y las versiones publicadas (el después). Mientras esa
consulta corre, la pestaña lo avisa, y las reglas aparecen cuando termina. Calibración sobre la Sede
Central, modificaciones creadas desde 2025: de 2.972 contratos con modificaciones publicadas, 13
tienen dos o más prórrogas, 37 tienen una prórroga creada al filo del vencimiento y 37 suben su
valor un 40 % o más. Con el caso real, el motor da tres prórrogas, las tres al vencimiento y una
adición del 43,6 %, que es lo que dicen los documentos.

Las dos últimas salieron del caso BOG-1363-2025 (Consorcio Sedes Tupeon), que pagó el anticipo del
20 % y no volvió a registrar pagos. Calibración sobre los 81 contratos de obra, interventoría y
consultoría de la ESAP: 41 están vencidos y siguen abiertos, pero solo uno tiene pagada exactamente
una fracción redonda del valor, que es el de Tupeon; ocho están vencidos y sin liquidar.

SECOP registra en ese conjunto la fecha de terminación un día después de la que dice el documento
firmado en muchos contratos. Por eso la regla de vencimiento usa una ventana de varios días, y por eso
la ficha avisa que el documento firmado manda.

### Reglas sobre procesos

| Severidad | Regla | Qué detecta |
|---|---|---|
| Crítica | Adjudicado sin ofertas | Se adjudicó sin ninguna oferta registrada |
| Alta | Un solo oferente | Se adjudicó con una sola oferta recibida |
| Alta | Plazo corto para ofertar | Menos de cinco días entre publicación y cierre |
| Media | Adjudicado casi por el precio base | Valor adjudicado por encima del 99 % del base |
| Media | Muchos invitados, casi ninguna oferta | Veinte o más invitados y dos o menos respuestas |
| Alta | Competidores socios | Dos de los proponentes del proceso han sido socios en un consorcio o unión temporal en cualquier entidad |
| Media | Menos ofertas | Un proceso parecido de la misma entidad, por un valor similar, recibió muchas más ofertas antes |

Las dos últimas no corren solas: se calculan al pulsar **Buscar vínculos entre proponentes** en la
pestaña de Procesos. El botón toma los procesos con al menos una oferta (hasta 80), trae sus
proponentes del conjunto «Proponentes por proceso» (`hgi6-6wh3`), abre cada consorcio en sus
integrantes con «Grupos de Proveedores» (`ceth-n4bn`) y cuenta los consorcios que dos proponentes
han compartido, sin contar el propio consorcio con el que se presentaron. Para la segunda regla busca
procesos anteriores de la ESAP con ocho o más respuestas, del mismo valor aproximado (entre la mitad
y el doble) y con un nombre parecido, y avisa si el actual recibió un 35 % o menos de esas ofertas.
Salieron del caso BOG-1363-2025, donde los dos mejor calificados (Tupeon e Infracon) resultaron
tener vínculos entre sí. Que dos competidores hayan sido socios no prueba colusión, pero es justo lo que la
Superintendencia de Industria y Comercio pide revisar.

### Lo que no se puede detectar con estos datos

SECOP II no publica las ofertas perdedoras, así que las señales de colusión que exigen compararlas
—precios idénticos, múltiplos fijos, rotación de ganadores— no se pueden calcular. Tampoco publica
los beneficiarios finales de las empresas, así que no se puede detectar que dos oferentes compartan
dueño; lo más cerca que llega el monitor es ver que hayan sido socios en consorcios, y lo demás
(representantes, direcciones, revisores fiscales) hay que buscarlo en el RUES. Y el objeto acomodado solo se detecta leyendo los pliegos: el monitor puede decir a qué
proceso mirar, no leerlo por nadie.

## Publicar en GitHub Pages

Los pasos, en el repositorio `0.0.0.1` de la cuenta `aaroncarlos761-cloud`:

1. Entrar a <https://github.com/new>, poner `0.0.0.1` como nombre, dejarlo **público** y
   crearlo.
2. En el repositorio recién creado, usar **Add file → Upload files** y arrastrar
   `index.html`. Confirmar con **Commit changes**.
3. Ir a **Settings → Pages**. En *Build and deployment*, dejar *Source* en
   **Deploy from a branch**, escoger la rama `main` y la carpeta `/ (root)`. Guardar.
4. Esperar entre uno y dos minutos. La página queda en:

       https://aaroncarlos761-cloud.github.io/0.0.0.1/

Para actualizarla más adelante basta con subir de nuevo el `index.html`; GitHub
republica solo.

El repositorio tiene que ser público para que Pages funcione sin costo. Eso significa que
el código queda a la vista, lo cual no es un problema: no contiene claves ni datos, solo
las consultas.

## Uso local

El mismo `index.html` funciona abriéndolo con doble clic desde el computador, sin
publicarlo. Consulta la misma API y se comporta igual. La lista de seguimiento de la
versión local y la de la versión publicada son independientes, porque cada una vive en su
propio origen dentro del navegador.

## Fuentes

- Contratos electrónicos SECOP II — conjunto `jbjy-vk9h` en datos.gov.co
- Procesos de contratación SECOP II — conjunto `p6dx-8zbt` en datos.gov.co
- Modificaciones a contratos SECOP II — conjunto `u8cx-r425` en datos.gov.co
- Grupos de Proveedores SECOP II — conjunto `ceth-n4bn` en datos.gov.co

El conjunto de contratos se recarga completo una vez al día en la fuente, así que ese es
el límite real de frescura: la página siempre trae lo último publicado, y lo último
publicado se actualiza a diario.

Cada respuesta se guarda cinco minutos en la memoria de la página, así que cambiar de pestaña no repite consultas; el botón Consultar borra esa memoria y trae todo de nuevo.

Las consultas no usan token de aplicación. Socrata limita por dirección IP a quien
consulta sin token; para un uso personal no se alcanza ese límite. Si alguna vez la
página empieza a responder con error de límite excedido, se registra un token gratuito en
la cuenta de datos abiertos y se añade a las consultas.

## Cuentas de la ESAP incluidas

Se filtra por NIT y no por nombre, a propósito: buscar el texto "ESAP" arrastra a la
Unidad de Búsqueda de Personas Desaparecidas, porque la palabra "desaparecidas" contiene
esas cuatro letras.

| Cuenta | NIT |
|---|---|
| Sede Central (Bogotá) | 899999054 |
| Territorial Bolívar | 800248529 |
| Territorial Cundinamarca | 830011682 |
| Territorial Huila-Caquetá y Bajo Putumayo | 813006956 |
| Territorial Nariño-Alto Putumayo | 800117534 |
| Territorial Meta | 800117530 |
| Territorial Atlántico | 800117522 |
| Territorial Antioquia | 800117519 |
| Territorial Norte de Santander-Arauca | 800145876 |
| Territorial Boyacá-Casanare | 800117524 |
| Territorial Caldas | 800117525 |
| Territorial Tolima | 800117541 |
| Territorial Quindío-Risaralda | 800117537 |
| Territorial Santander | 800117540 |
| Territorial Cauca | 800117528 |
| Territorial Valle del Cauca | 800117545 |
