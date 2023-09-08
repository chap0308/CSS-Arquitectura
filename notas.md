## Forma corta de usar transition
```bash
.navegacion a {
    transition: background-color 300ms, color 300ms;
}

.navegacion a:hover {
    background-color: rgb( 255 255 255 / .5 );
    color: var(--negro);
}
```
## Los pseudo-elementos no existen en html como tal, pero aun así estos serían como los hijos de un elemento, ya que van despues de un elemento.
```bash
<a class="telefono">
    ::before /*se le considera como su hijo*/
    "01-02020"
</a>
```
## Pseudo-elementos: ::before y ::after. Tal y como su nombre lo dicen, se colocan antes o despues del elemento.
En el content se debe colocar lo que quieres aparezca.
```bash
.telefono::before {
    content: 'Hola mundo';
}
```
Para que aparezca todas las propiedas usamos "display:block;".
```bash
.telefono::before {
    content: '';
    display: block;/*IMPORTANTE*/
    width: 4rem;
    height: 4rem;
    background-image: url(../img/telefono.png);
    background-repeat: no-repeat;
    background-position: center center;
    margin-right: 1rem;
}
```
## Pseudo-elementos: Pero a pesar de que no existan, sí son afectados por las propiedades como display flex o grid, ya que estos son considerados como sus hijos.
Serán afectados los dos: el texto y el before(imagen)
```bash
<a class="telefono" href="tel:01-800-0000-000">
    ::before
    01-800-0000-000
</a>

.telefono {
    display: flex;
}
```
## Nota de display flex(align-items): Toma en cuenta algunas propiedades que definen el tamaño de los hijos cuando usas flex.
En este caso, la propiedad align-items hace que todos los elementos hijos tomen el tamaño necesario(width y height). Es decir, los ajustan al minimo necesario.
```bash
<nav class="navegacion">
    <a class="link" href="#">Inicio</a>
    <a class="link" href="#">Nosotros</a>
    <a class="link" href="#">Modelos</a>
    <a class="link" href="#">Galería</a>
    <a class="link" href="#">Contacto</a>
</nav>

.navegacion {
    display: flex;
    flex-direction: column;/* ESTA PROPIEDAD NO */
    align-items: center;/* esto hace que todos sus hijos tomen el tamaño necesario */
}
```
Más info en barra.html.
## Conclusion anterior:
Es muy poderoso el width y height en flex y grid, valores: 100%, auto, 20rem, etc. Prueba con las flechas.
## Acerca del width en responsive:
Luego de haber colocado un width para un tamaño determinado, coloca para el nuevo tamaño width: auto, para que no ocurra errores. Puede que el anterior tamaño no sea bueno para la otra pantalla.
```bash
.navegacion {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;/* Width anterior*/
    margin-top: 1rem;
}
@media (min-width: 768px) { 
    .navegacion {
        flex-direction: row;
        width: auto;/** Width para el otro tamaño*/
    }
}
```
## Nota importante para reutilizar codigo:
Si queremos reutilizar nuestros estilos, debemos tener en cuenta las clases padres que conforma. Si un clase hija depende la clase de un padre, va a ser un poco dificil reutilizar ya que cuando la reutilizemos puede que no tenga el mismo nombre que la clase padre, lo cual, genera que no se copien bien lo estilos y tengamos que buscar y volver a copiar el codigo ajustandole el nuevo nombre del padre. Por eso se trabaja en modulos con BEM.
Ejemplo del problema:
```bash
<header class="header">
    <nav class="navegacion">
        <a class="link" href="#">Inicio</a>
        <a class="link" href="#">Nosotros</a>
        <a class="link" href="#">Modelos</a>
        <a class="link" href="#">Galería</a>
        <a class="link" href="#">Contacto</a>
    </nav>
</header>

.header a {
    color: var(--blanco);
    font-size: 2rem;
}
```
Si copiamos y pegamos, no funcionaran los estilos y debemos rehacer el codigo
```bash
<footer class="footer mt-5">
    <nav class="navegacion">
        <a class="link" href="#">Inicio</a>
        <a class="link" href="#">Nosotros</a>
        <a class="link" href="#">Modelos</a>
        <a class="link" href="#">Galería</a>
        <a class="link" href="#">Contacto</a>
    </nav>
</footer>

.footer a {
    color: var(--blanco);
    font-size: 2rem;
}
```