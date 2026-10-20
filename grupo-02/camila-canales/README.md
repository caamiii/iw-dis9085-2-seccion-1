¿Qué hice en el sitio?

- Diseñé en Figma con mi compañera la versión desktop del sitio, su **página de inicio** y la **página de Entradas** y su versión mobile.
- Vi la tipografía y sus estilos, los componentes con sus variantes, noticias e íconos de video, animaciones, distribución y correcciones de mejoras.
- Corregi los HTML que se habían hecho siguiendo el orden del material de apoyo (ya que habian códigos que no habiamos visto en clases)
- Con apoyo de la IA, pasé el diseño a CSS y luego teniendolo como contraparte corregi el CSS de la página principal hasta donde estaba y lo complete con el resto del diseño que faltaba. El CSS de las entradas solo corregi detalles ya que estaba completo y utilice JavaScript para elementos como el carrusel, botones del video y cuentra regresiva ya que investigando, la IA me dijo que era mejor trabajar esos elementos con JavaScripy para tener un mayor control y que quedaran lo más parecidas al diseño en figma.
- Revisé cada versión en el navegador comparandola con el diseño en figma y fui haciendo las correciones de medidas, proporciones, animaciones, velocidades.

- ### ¿Qué dificultades tuve y cómo las resolví?

#### Consulta: qué es el hero

> Que son las franjas del hero?

**Respuesta de la IA (resumen):** el *hero* es la primera sección de la página. Las franjas son las 8 bandas horizontales de vidrio desenfocado que cruzan el fondo, y en el Figma son las capas *Frame 1* a *Frame 9*.
**Sugerencias:**
1. **Rechazado:** las animaciones de entrada de las franjas y del texto. 
2. **Rechazado:** usar un video de fondo. El archivo original es un GIF.
3. **Aceptado:** dejar una imagen fija, hasta poner el GIF cuando pudiera descargarlo.

#### Consulta: Quiero mantener la tipografía Helvetica Neue no otra

> Respecto a la tipografia, necesito mantener Helvetica Neue. Que se debe hacer pana mantenerla, y que se vea bien en windows.

**Respuesta de la IA (resumen):** explicó que Helvetica Neue no viene en Windows y que tiene licencia. Revise que estuviera instalada en mi PC. La IA convirtió los 5 pesos usados al formato `.woff2` y los adjunte en la carpeta del sitio.

**Antes** (fuente de reemplazo):

```css
@font-face {
  font-family: "Inter Tight";
  font-weight: 500;
  src: url("assets/fonts/inter-tight-latin-500-normal.woff2") format("woff2");
}
```

**Después:**

```css
@font-face {
  font-family: "Helvetica Neue Web";
  font-weight: 500;
  font-display: block;
  src: url("assets/fonts/helvetica-neue-medium.woff2") format("woff2");
}
```

**Sugerencias:**
1. **Rechazado:** usar *Inter Tight* como fuente parecida. Necesitaba la tipografía que teniamos en el diseño de figma.
2. **Aceptado:** incluir solo los 5 pesos usados (Light, Medium, Bold, Heavy y Black) y no los 30 archivos de la carpeta, para que el sitio cargue rápido.

#### Consulta: necesito descargar el GIF desde el figma pero no se como se hace

> Respecto al fondo de gif del inicio ¿Cómo lo busco en Figma para descargarlo?

**Respuesta de la IA (resumen):** indicó que el fondo es la capa llamada *Degradado*. Explicó que el botón *Export* de Figma baja la imagen sin animación, así que hay que usar el archivo original o un plugin.

**Solución propia (después de buscar en figma ya que no me funcionaba lo que me decia la IA):** el error estaba en que lo intentaba exportar desde la ventana diseño y ahí solo lo convertía en png no me dejaba el gif. Probando descubri que tenía que irme a Dev mode y en recursos salia el gif para poder descargarlo como gif y no como png.

#### Consulta: 
> si tengo una web para computador es mejor poner en los codigos que se adapte a celular o mejor una especial para celu

**Respuesta de la IA (resumen):** Es infinitamente mejor hacer que tu web actual se adapte a celular (diseño responsivo o Responsive Web Design) en lugar de crear una web separada exclusivamente para móviles.
Hoy en día, las páginas web separadas (como las antiguas versiones ://tuweb.com) están en desuso porque los motores de búsqueda como Google penalizan o complican el posicionamiento de los sitios que duplican su contenido.

#### Consulta: aumentar la velocidad del carrusel

> Necesito aumentar la velocidad de cambio del carrusel, para que quede similar al figma, que se ve que cambia mas rapido. Donde debo ajustar eso?

**Respuesta de la IA (resumen):** la velocidad está en `script.js`, no en el CSS, y se mide en milisegundos (1000 = 1 segundo):
- `ESPERA` es el tiempo que se queda quieta cada vista.
- `DURACION` es lo que tarda el deslizamiento.

Para que quede igual al Figma, sugirió copiar el tiempo de la interacción *After delay* del panel **Prototype**.

**Antes:**

```javascript
const ESPERA = 3500;        // tiempo que se queda quieta cada vista
const DURACION = 900;       // duración del desplazamiento
```

**Después:**

```javascript
const ESPERA = [valor];     // tiempo que se queda quieta cada vista
const DURACION = [valor];   // duración del desplazamiento
```

**Sugerencias:**
1. **Aceptado:** bajar `ESPERA` para que cambie más rápido, como en el Figma.
2. **Aceptado:** no modificar `PASO`, porque es el ancho que avanza en cada cambio y las fotos quedarían desalineadas.

#### Consulta: por qué algunas cosas van en JavaScript y no en CSS

> por que el carrusel, la cuenta regresiva y los controles de video de pausa y de silencio se hacen en un .js y no el css

**Respuesta de la IA (resumen):**

| Lenguaje | Rol | Ejemplo en el sitio |
|---|---|---|
| **HTML** | **Qué hay** en la página | Un título, una foto, un botón |
| **CSS** | **Cómo se ve** | Colores, tamaños, ubicación, efectos al pasar el mouse |
| **JavaScript** | **Qué hace y cuándo**: calcula, decide y reacciona | Contar el tiempo, mover cosas por pasos, dar órdenes al video |

- **Cuenta regresiva:** hay que saber la hora actual, restarla a la fecha del festival y repetir el cálculo cada segundo. CSS no sabe la hora ni hace cálculos.
- **Controles del video:** el botón tiene que darle una orden al video y cambiar el ícono. Solo JavaScript puede dar órdenes:

```javascript
video.pause();          // pausar
video.muted = false;    // activar el sonido
```

- **Carrusel:** un carrusel simple *sí* se puede hacer solo con CSS (`@keyframes`). Usamos JavaScript para avanzar de a dos fotos con pausas, volver al inicio sin que se note y detenerlo al pasar el mouse.

¿Qué aprendí?

- **Un diseño ordenado facilita el desarrollo:** desde el Figma había que seguir el mismo paso a paso que se hizo para realizar el diseño así quedaba en codigos ordenado y también ponerle estos comentarios arriba de los códigos para que después sea más fácil saber a que corresponde cada código al momento de tener que editar algo.
- **Las fuentes tienen licencia:** una fuente instalada en mi PC no se ve en otro computador si no se incluye en el sitio.
- - **Un solo CSS para varias páginas:** si dos páginas usan el mismo `styles.css`, un cambio se aplica en ambas.
- **HTML, CSS y JavaScript tienen roles distintos:** HTML define *qué hay*, CSS define *cómo se ve* y JavaScript define *qué hace y cuándo*. Si algo solo cambia de aspecto va en CSS; si hay que calcular, recordar o dar órdenes, va en JavaScript.
- **Tener más confianza en hacer los códigos:** Si bien aún me queda mucho por aprender ya no me siento tan perdida como la primera vez que vi los códigos y también que esto requiere de paciencia.













