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

**Señales.** Tres cosas a la vez. Valores imposibles, que son los contratos por encima de
cien mil millones de pesos y que en esta entidad solo pueden ser errores de digitación al
cargar a SECOP. Atípicos, que son los que superan veinte veces el promedio de su propio
tipo de contrato, calculado excluyendo los imposibles para que no contaminen el promedio.
Y el reparto por modalidad, con el porcentaje que se adjudica por contratación directa.
Abajo, los contratos en ejecución que vencen dentro de 30, 60 o 90 días.

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
