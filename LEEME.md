# Web de Ángel Padilla — Guía rápida

Toda la web es **un solo archivo**: `index.html`. Se abre con doble clic en cualquier navegador.
No necesita internet para funcionar (salvo las tipografías de Google).

```
angel-padilla-web/
├── index.html      ← la web entera (ábralo con doble clic)
├── assets/
│   └── angel-padilla-headshot.jpg   ← retrato oficial (Stage Entertainment)
├── dossier-casting-VISTA-PREVIA.pdf ← ejemplo del CV que genera la web
└── LEEME.md        ← este archivo
```

> **Sobre el PDF incluido:** es el dossier de casting ya generado, con todos los datos
> definitivos. Puede enviarse tal cual. Si más adelante edita la web, genere uno nuevo
> con el botón "Descargar CV" para mantenerlo al día.

---

## 1. Datos ya configurados

No queda ningún campo pendiente de rellenar. La ficha está publicada con estos datos:

| Dato | Valor |
|---|---|
| Email de contacto | `angelpadilla@arpadia.es` |
| Idiomas | Castellano · Inglés |
| Registro vocal | Barítono dramático |
| Estado | Disponible |
| El Rey León | 2019 – 2025 (seis temporadas, finalizado) |

Se han retirado de la ficha los campos de altura, carné de conducir, teléfono y
representante, tal como se pidió. Si en algún momento quiere recuperarlos, basta con
añadir una línea como esta dentro del bloque correspondiente:

```html
<div class="frow"><dt>Altura</dt><dd>1,78 m</dd></div>
```

## 2. El formulario de contacto (ya activo)

### Qué es FormSubmit

Una web hecha solo con HTML no puede enviar correos por sí misma: para eso hace falta un
servidor. FormSubmit es un servicio gratuito que hace de intermediario. Cuando alguien
rellena el formulario, los datos van a FormSubmit y este los reenvía por correo.

No hay que registrarse, ni instalar nada, ni pagar. El correo **no aparece escrito en el
código de forma rastreable**, lo que reduce el spam.

### A qué dirección llegan

A **angelpadilla@arpadia.es**. Llegan como un correo normal, con este aspecto:

- **Asunto:** Nueva propuesta desde la web de Ángel Padilla
- **Contenido:** una tabla con nombre, email, empresa, tipo de propuesta y mensaje
- **Responder:** basta con darle a "Responder" y le llega a quien escribió

Además, quien envía el formulario recibe una confirmación automática diciendo que el
mensaje se ha recibido correctamente.

### Paso pendiente: activarlo (solo una vez)

**Esto es importante y hay que hacerlo antes de enseñar la web a nadie.**

1. Abra la web y envíe un mensaje de prueba desde el formulario.
2. FormSubmit enviará un correo a angelpadilla@arpadia.es con el asunto
   *"Confirm your email"* o similar. Revise también la carpeta de spam.
3. Pulse el botón de confirmación que aparece en ese correo.
4. Listo. A partir de ese momento todos los mensajes llegan directamente.

Mientras no se confirme, los envíos no llegarán a la bandeja.

### Cambiar la dirección de destino

Busque en el archivo esta línea y cambie el correo:

```html
<form id="cForm" action="https://formsubmit.co/angelpadilla@arpadia.es" method="POST">
```

Si cambia la dirección, habrá que volver a confirmarla con el paso anterior.

### Ajustes ya incluidos

Justo debajo de esa línea hay cuatro campos ocultos que no se ven en la web:

| Campo | Para qué sirve |
|---|---|
| `_subject` | El asunto con el que llega el correo |
| `_template` | Presenta el mensaje como tabla, más legible |
| `_autoresponse` | Respuesta automática a quien escribe |
| `_honey` | Trampa antispam: los robots la rellenan y el envío se descarta |

Puede editar el texto de `_subject` y `_autoresponse` libremente.

### Nota sobre pruebas en local

El formulario **solo funciona con la web publicada en internet**. Si abre `index.html`
con doble clic desde el ordenador, el envío dará error. Es normal: publique la web primero
(punto 6) y pruébelo desde su dirección real.

## 3. Añadir el videobook

1. Suba el vídeo a YouTube o Vimeo (puede ponerlo como "no listado" si no quiere que sea público).
2. Busque en el archivo la línea: `var VIDEO_URL = null;`
3. Sustitúyala por una de estas, con el enlace real:

```javascript
var VIDEO_URL = "https://www.youtube.com/embed/CODIGO_DEL_VIDEO?autoplay=1";
// o bien
var VIDEO_URL = "https://player.vimeo.com/video/NUMERO?autoplay=1";
```

El código de YouTube es lo que va después de `watch?v=` en la dirección del vídeo.

---

## 4. Añadir más fotos a la galería

En la sección **Galería** hay cinco huecos preparados. Para cada foto:

1. Copie la imagen dentro de la carpeta `assets/`.
2. Busque el hueco correspondiente en el archivo, por ejemplo el que contiene
   `<b>Headshot en color</b>`.
3. Sustituya todo el bloque `<div class="gslot">...</div>` por:

```html
<figure class="gslot gslot--real">
  <img src="assets/NOMBRE-DE-SU-FOTO.jpg" alt="Ángel Padilla en escena" loading="lazy">
  <figcaption><b>Título de la foto</b><span>Producción o año</span></figcaption>
</figure>
```

**Recomendaciones para las fotos:**
- Formato vertical, proporción 3:4 (por ejemplo 900 × 1200 píxeles).
- Peso inferior a 400 KB cada una, para que la web cargue rápido.
- Nombres sin acentos ni espacios: `angel-escena-cabaret.jpg`, no `Ángel en Cabaret.jpg`.

**Qué fotos funcionan mejor en un casting:** un primer plano neutro (headshot),
un plano de cuerpo entero, y dos o tres en personaje que muestren registros opuestos
(una dramática y una cómica).

---

## 5. El CV en PDF

El botón "Descargar CV" abre el diálogo de impresión del navegador.
La web tiene una **hoja de estilos de impresión** ya preparada: al imprimir se convierte
automáticamente en un dossier limpio en blanco y negro, sin menús ni animaciones.

Para guardarlo como PDF: en el diálogo de impresión, elegir **"Guardar como PDF"**
en lugar de una impresora.

---

## 6. Publicar la web en internet

La opción más sencilla y **gratuita** es **Netlify Drop**:

1. Entrar en [app.netlify.com/drop](https://app.netlify.com/drop)
2. Arrastrar la carpeta `angel-padilla-web` entera a la ventana.
3. En unos segundos da una dirección tipo `nombre-aleatorio.netlify.app`, que ya se puede compartir.
4. Registrándose (gratis) se puede cambiar el nombre a algo como `angelpadilla.netlify.app`.

Para un dominio propio tipo `angelpadilla.es`: se compra en cualquier registrador
(alrededor de 12 €/año) y se conecta desde el panel de Netlify.

Otras opciones equivalentes: GitHub Pages, Vercel, Cloudflare Pages.

---

## 7. Sobre la información publicada

Todos los datos biográficos y de trayectoria proceden de fuentes verificables:

- **Ficha oficial de Stage Entertainment** (El Rey León) — roles, formación, títulos, Premio Max
- **Wikipedia en español** — datos personales, cronología de obras, producciones
- **Antena 3** — reportaje de *Veo cómo cantas* (septiembre de 2021)
- **Alcalá Suena 2024** — datos sobre ARpadia, instrumentos y el proyecto *Ecléctico Retorno*
- **arpadia.es** — conciertos y festivales de la banda

No se ha inventado ningún dato. Los años de algunas producciones aparecen como
"Temporada" en lugar de fechas exactas porque las fuentes no coinciden entre sí:
si tiene las fechas precisas, conviene concretarlas.

**Dos apuntes que conviene revisar con él:**

1. En la web anterior figuraban personajes concretos (Colmenero en *Hoy no me puedo levantar*,
   Princeton y Rod en *Avenue Q*, Max Detweiler en *Sonrisas y Lágrimas*). No he podido
   confirmarlos en ninguna fuente pública, así que aparecen como "Elenco". Si él confirma
   esos papeles, merece la pena añadirlos: **los personajes protagonistas pesan mucho en un casting**.
2. La ficha oficial de Stage Entertainment indica que entró en *El Rey León* como **cover** de
   Scar, Pumbaa y Mufasa, además de **capitán de peleas** y **director de elenco infantil**.
   Lo he reflejado así porque es lo que dice la producción, y esos dos últimos cargos son
   un aval de responsabilidad que muchos actores no tienen.

3. **El Rey León figura como etapa finalizada (2019 – 2025).** Toda la web habla de esa
   producción en pasado y el perfil se presenta como *disponible para nuevos proyectos*,
   que es justo el mensaje que interesa en un casting. Wikipedia sigue diciendo "desde 2019"
   porque no está actualizada; si algún director de reparto lo comenta, la referencia buena
   es esta web.

---

## Cambios rápidos más habituales

**Cambiar el color dorado:** al principio del archivo, busque `--gold:#C9A961;` y cambie ese
código de color. El resto de la web se adapta sola.

**Cambiar un texto:** búsquelo tal cual en el archivo y edítelo. El texto está en el mismo
orden en que aparece en pantalla.

**Quitar una sección entera:** busque el comentario que la abre, por ejemplo
`<!-- ============ GALERÍA ============ -->`, y borre desde ahí hasta el `</section>`
correspondiente. Recuerde borrar también su enlace en el menú.
