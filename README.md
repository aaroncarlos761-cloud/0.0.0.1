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

**Banderas rojas.** Dieciocho reglas de detección aplicadas a cada contrato y a cada proceso,
con severidad crítica, alta o media. Se explican una por una más abajo y en la pestaña de
Metodología del propio sitio, con la fuente de cada una. Se puede filtrar por regla y exportar
lo marcado a CSV con la explicación incluida.

**Vencimientos y modalidades.** Los contratos en ejecución que terminan dentro de 30, 60 o 90
días, útil para pedir informes de supervisión a tiempo, y el reparto por modalidad de
contratación del periodo.

**Metodología.** Qué detecta cada regla, por qué importa, de dónde sale y qué no puede ver este
monitor. Está dentro del sitio para que cualquiera pueda auditar el criterio.

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

El monitor evalúa dieciocho reglas de detección sobre cada contrato y cada proceso, y marca los
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
| Alta | Posible fraccionamiento | Dos o más contratos al mismo contratista, misma entidad, mismo día |
| Alta | Valor atípico para su tipo | Más de veinte veces el promedio de su tipo de contrato |
| Alta | Contratista recurrente | Cinco o más contratos en el periodo consultado |
| Alta | Prórroga extensa | Más de noventa días adicionados al plazo |
| Alta | Contrato con anticipo | Cualquier pago adelantado, que en la ESAP es rarísimo |
| Alta | Contrato cedido | El que firmó no fue el que ejecutó |
| Media | Publicado sin valor | Contrato con valor cero |
| Media | Sin fecha de firma | Registro no atribuible a ninguna administración |
| Media | Sin supervisor designado | Campo de supervisor vacío o «No definido» |

### Reglas sobre procesos

| Severidad | Regla | Qué detecta |
|---|---|---|
| Crítica | Adjudicado sin ofertas | Se adjudicó sin ninguna oferta registrada |
| Alta | Un solo oferente | Se adjudicó con una sola oferta recibida |
| Alta | Plazo corto para ofertar | Menos de cinco días entre publicación y cierre |
| Media | Adjudicado casi por el precio base | Valor adjudicado por encima del 99 % del base |
| Media | Muchos invitados, casi ninguna oferta | Veinte o más invitados y dos o menos respuestas |

### Lo que no se puede detectar con estos datos

SECOP II no publica las ofertas perdedoras, así que las señales de colusión que exigen compararlas
—precios idénticos, múltiplos fijos, rotación de ganadores— no se pueden calcular. Tampoco publica
los beneficiarios finales de las empresas, así que no se puede detectar que dos oferentes compartan
dueño. Y el objeto acomodado solo se detecta leyendo los pliegos: el monitor puede decir a qué
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

El conjunto de contratos se recarga completo una vez al día en la fuente, así que ese es
el límite real de frescura: la página siempre trae lo último publicado, y lo último
publicado se actualiza a diario.

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
