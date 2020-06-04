Wallablock es un framework para la publicación de ofertas, de forma descentralizada y segura.

# Arquitectura

![Arquitectura]

Wallablock se compone de varios componentes, tal y como se muestra en la figura. Estos son:

* _Blockchain_ ([Ethereum]): Guarda los datos principales de las ofertas.
* Almacenamiento distribuído ([IPFS]):
  Almacena datos cuando hacerlo en la blockchain sería demasiado caro.
  Son datos que no consideramos críticos para la validez de la oferta (imágenes y descripción detallada).
* Base de datos ([ElasticSearch]): Ver sección [Base de datos](#base-de-datos).
* Cliente web ([React]): Frontend que permite al usuario interactuar con el resto de componentes de forma cómoda.

## Base de datos

Como novedad, incorporamos una base de datos además de la cadena de bloques. Aunque podría parecer redundante,
ambas cumplen una función crítica.

La _blockchain_ permite que varias partes puedan intercambiar información entre ellas sin necesidad de confiar
las unas en las otras. Esto permite que dos clientes puedan interactuar con la misma oferta desde nodos independientes.
Sin embargo, las búsquedas en la cadena de bloques son, por lo general, muy lentas.

Para paliar esta situación, incluímos una base de datos NoSQL, como es el caso de ElasticSearch, que se especializa
en hacer búsquedas rápidamente. Esta base de datos no nos ofrece las garantías de seguridad que tenemos con la _blockchain_,
ya que la base de datos está totalmente controlada por una única entidad; a cambio, tampoco tenemos las mismas restricciones,
por lo que podemos permitir al usuario hacer las búsquedas a las que está acostumbrado, filtrando por categorías
o por títulos parciales, por ejemplo.

## Descentralización

Todo esto nos permite que la web de Wallablock no dependa de una única entidad: cualquiera puede unirse a la red Ethereum, la red IPFS, crear una base de datos ElasticSearch y alojar el cliente web en su servidor (o incluso crear otro cliente). De hecho, también se puede elegir alojar una parte de la arquitectura y delegar el resto a terceros, según las limitaciones del proveedor.

# Ejemplos de uso

## Buscar

![Buscar]

La acción más habitual que realizarán los usuarios será la de buscar ofertas. Para ello,
se servirán de los filtros disponibles en el menú izquierdo y del campo de búsqueda
para concretar el título de la oferta deseada.

## Ver oferta

![Ver oferta]

Para ver toda la información relativa a una oferta, es suficiente con que el usuario
pinche sobre ella y se desplegará un _pop-up_. En este, el usuario encontrará información
como el título, el precio de la oferta y una breve descripción del artículo.

## Comprar

![Comprar]

A la hora de comprar una oferta, el usuario es redirigido a una página específica la cual
se encarga de obtener la información relativa a la oferta desde la _blockchain_, para
asegurar la veracidad y fiabilidad de los datos. Antes de proceder a realizar la compra,
el usuario debe introducir un correo de contacto para permitir la comunicación entre
comprador y vendedor.

## Publicar oferta

![Publicar oferta]

El proceso de publicar una oferta en WallaBlock es muy sencillo. Para ello, es suficiente
con rellenar un formulario compuesto por diversos campos obligatorios como: título,
precio, categoría y país de origen, combinado con otros dos campos opcionales como
son descripción e imágenes.

## Ver ofertas en las que el usuario participa

![Ver ofertas en las que el usuario participa][Ver ofertas propias]

El usuario tiene la opción de ver todas las ofertas en las que este participa. Por cada
oferta, el usuario puede realizar una serie de acciones en función del estado actual en
el que se encuentra la oferta (esperando comprador, esperando confirmación,
finalizada o cancelada) y del rol del usuario en la oferta (comprador o vendedor). Cabe
mencionar que estas ofertas son obtenidas desde la _blockchain_.

## Editar oferta

![Editar oferta]

Una vez la oferta ha sido publicada, pero siempre que no haya un comprador, el
vendedor tiene la opción de editar ciertos campos, como el título, el precio, el país de
origen, la categoría o las imágenes. Quizá la acción más interesante es la de cambiar el
precio, que se encarga de requerir los fondos necesarios en el caso de que el precio
indicado sea superior al original, o de devolver los fondos correspondientes si es
inferior.

## Retirar fondos de una oferta

![Retirar fondos de una oferta][Retirar fondos]

Cuando una oferta ha sido finalmente confirmada por el comprador, ambas partes
pueden proceder a retirar los fondos que estaban retenidos dentro del contrato. Por
ende, esta acción debe ser realizada tanto por parte del vendedor como del comprador
para recuperar su depósito y cobro en el caso del vendedor. Cabe destacar que el coste
de esta acción es únicamente el coste del gas. Esta acción també se debe realizar cada
vez que el contrato nos devuelva dinero (por ejemplo, al cancelar la oferta o cuando
bajamos el precio).

[Arquitectura]: Arquitectura.svg
[Buscar]: Buscar.png
[Ver oferta]: VerOferta.png
[Comprar]: Comprar.png
[Publicar oferta]: PublicarOferta.png
[Ver ofertas propias]: VerOfertasPropias.png
[Editar oferta]: EditarOferta.png
[Retirar fondos]: RetirarFondos.png

[Ethereum]: https://ethereum.org/
[IPFS]: https://ipfs.io/
[ElasticSearch]: https://www.elastic.co/
[React]: https://reactjs.org/
