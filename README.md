# proyecto_integrador_U2_T.A.P

## DESARROLLO DE UN CATALOGO DE PRODUDCTOS REUTILIZABLES

En este proyecto se desarrolló una aplicación que muestra un catálogo de productos tecnológicos utilizando el framework Flet del lenguaje Python.

El objetivo principal fue aprender a crear componentes visuales reutilizables, organizando el código en módulos y utilizando el concepto de herencia para construir una interfaz gráfica más estructurada.

La aplicación muestra una lista de productos tecnológicos con su imagen, nombre, descripción, precio y botones de acción.

Además, el proyecto fue publicado en internet utilizando Netlify, lo que permite acceder a la página web desde cualquier navegador.

# MODELO DE DATOS 

El modelo de datos se encarga de almacenar la información de los productos que se mostrarán en el catálogo.

En el programa se utilizó una lista de diccionarios en Python, donde cada diccionario representa un producto diferente.

EJEMPLO:

```Python
productos = [
{
"id":1,
"nombre":"Laptop Gamer",
"descripcion":"Laptop para alto rendimiento",
"precio":25000,
"ruta_imagen":"laptop.jpg"
},
]
```

Cada porducto tendra como atributo el id, nombre, descripcion, precio y ruta de image, esta estructura permitira agregar facilmente mas productos sin modificar la interfaz.

# Organización del Proyecto en Módulos

El proyecto se organizó en dos módulos principales para mantener el código más ordenado y reutilizable.

- Módulo 1: main.py

Este archivo es el archivo principal del programa.
Aquí se encarga de:
- crear la ventana de la aplicación
- definir los productos
- organizar el catálogo en la pantalla
- llamar al componente reutilizable de producto

Ejemplo del código:

```Python
from producto import Producto
```
Esta línea importa la clase Producto desde otro archivo, lo que permite reutilizar ese componente varias veces dentro del catálogo.

# Módulo 2: producto.py

Este archivo contiene la clase personalizada que representa cada tarjeta de producto.

En lugar de escribir todo el diseño dentro del programa principal, se creó un componente reutilizable llamado Producto, que puede utilizarse para mostrar cualquier artículo del catálogo.

# Creación de la Clase Personalizada

Para crear el componente reutilizable se definió la siguiente clase:

```Python
class Producto(ft.Container):
```
Esta clase hereda de la clase Container del framework Flet.

Un Container es un componente que permite contener otros elementos visuales dentro de él.
gracias a esta herencia, el componente Producto puede utilizar propiedades como:
- ancho
- color de fondo
- bordes redondeados
- sombras
- contenido interno

Esto permite diseñar una tarjeta visual para cada producto.

# Diseño del Componente de Producto

Dentro de la clase se definieron varias propiedades que controlan la apariencia del componente.

Ejemplo:
```
self.width = 250
self.bgcolor = "white"
self.padding = 10
self.border_radius = 10
self.shadow = ft.BoxShadow(blur_radius=10)
```
Estas propiedades permiten que cada tarjeta tenga:
- un ancho fijo
- fondo blanco
- espacio interno
- bordes redondeados
- una sombra ligera

# Área de Imagen

Cada producto incluye una imagen que se carga desde la carpeta assets.

Ejemplo del código:
```
ft.Image(
src=f"/assets/{imagen}",
width=230,
height=150,
fit=ft.BoxFit.COVER,
)
```
Este componente muestra la imagen del producto.
Las propiedades utilizadas son:
- src: ruta de la imagen
- width y height: tamaño de la imagen
- fit: forma en que la imagen se ajusta al espacio disponible

# Información del Producto

Debajo de la imagen se muestra la información del producto.

Ejemplo:
```
ft.Text(nombre, weight="bold", size=16)
ft.Text(descripcion, size=12, color="grey")
ft.Text(f"${precio}", color="green", weight="bold", size=16)
```
Esto permite mostrar:
- el nombre del producto en negritas
- la descripción en un tamaño más pequeño
- el precio resaltado en color verde

# Barra de Acciones

Cada tarjeta incluye una barra de acciones con botones.

Ejemplo:
```
ft.Row([
ft.IconButton(icon=ft.Icons.FAVORITE_BORDER),
ft.ElevatedButton("Agregar al carrito")
])
```
Los botones incluidos son:
- botón de favoritos
- botón de agregar al carrito
- El botón de favoritos cambia de color cuando se presiona.

# Cambio de Color del Botón de Favoritos

Se creó una función para cambiar el estado del botón cuando se hace clic.

Ejemplo:
```
def _toggle_fav(self, e):
    self._is_fav = not self._is_fav
```
Esta función cambia el estado del botón entre:
- corazón vacío
- corazón lleno

Esto permite simular que el usuario guarda un producto como favorito.

# Layout de la Interfaz

En el archivo principal se utilizó un GridView para organizar los productos en la pantalla.

Ejemplo:
```
grid = ft.GridView(
expand=True,
runs_count=3,
spacing=20,
run_spacing=20
)
```
Esto permite que los productos se acomoden automáticamente en forma de cuadrícula, adaptándose al tamaño de la ventana.

# Gestión de Recursos (Assets)

Las imágenes del proyecto se almacenaron en una carpeta llamada assets.

Ejemplo de estructura:
```
assets
laptop.jpg
mouse.jpg
teclado.jpg
pc.jpg
audifonos.jpg
```
Para que el programa reconozca estas imágenes se configuró:
``` page.assets_dir = "assets" ```

Esto permite que el framework cargue correctamente las imágenes dentro de la aplicación.

# Despliegue en Web

El proyecto fue publicado en internet utilizando la plataforma Netlify. Para ello se creó una página web utilizando HTML, donde se muestra el catálogo de productos.

Codigo de html:
```
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Tech Store</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f5f5f5;
            margin: 0;
            padding: 0;
        }

        header {
            background: #1e1e2f;
            color: white;
            text-align: center;
            padding: 20px;
            font-size: 28px;
            font-weight: bold;
        }

        .contenedor {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            padding: 20px;
        }

        .card {
            background: white;
            border-radius: 10px;
            padding: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            text-align: center;
        }

        .card img {
            width: 100%;
            height: 150px;
            object-fit: cover;
            border-radius: 8px;
        }

        .card h3 {
            margin: 10px 0 5px;
        }

        .descripcion {
            font-size: 14px;
            color: gray;
        }

        .precio {
            color: green;
            font-weight: bold;
            font-size: 18px;
        }

        .acciones {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
        }

        button {
            border: none;
            padding: 8px 10px;
            border-radius: 5px;
            cursor: pointer;
        }

        .fav {
            background: none;
            font-size: 20px;
        }

        .carrito {
            background: #007bff;
            color: white;
        }

        .carrito:hover {
            background: #0056b3;
        }
    </style>
</head>

<body>

<header>CATÁLOGO TECNOLÓGICO</header>

<div class="contenedor">

    <!-- Producto 1 -->
    <div class="card">
        <img src="laptop.jpg">
        <h3>Laptop Gamer</h3>
        <p class="descripcion">Laptop para alto rendimiento</p>
        <p class="precio">$25000</p>

        <div class="acciones">
            <button class="fav" onclick="toggleFav(this)">🤍</button>
            <button class="carrito">🛒 Agregar</button>
        </div>
    </div>

    <!-- Producto 2 -->
    <div class="card">
        <img src="mouse.jpg">
        <h3>Mouse RGB</h3>
        <p class="descripcion">Mouse gamer con luces</p>
        <p class="precio">$800</p>

        <div class="acciones">
            <button class="fav" onclick="toggleFav(this)">🤍</button>
            <button class="carrito">🛒 Agregar</button>
        </div>
    </div>

    <!-- Producto 3 -->
    <div class="card">
        <img src="teclado.jpg">
        <h3>Teclado Mecánico</h3>
        <p class="descripcion">Teclado retroiluminado</p>
        <p class="precio">$1500</p>

        <div class="acciones">
            <button class="fav" onclick="toggleFav(this)">🤍</button>
            <button class="carrito">🛒 Agregar</button>
        </div>
    </div>

    <!-- Producto 4 -->
    <div class="card">
        <img src="pc.jpg">
        <h3>Monitor 27"</h3>
        <p class="descripcion">Monitor Full HD</p>
        <p class="precio">$4500</p>

        <div class="acciones">
            <button class="fav" onclick="toggleFav(this)">🤍</button>
            <button class="carrito">🛒 Agregar</button>
        </div>
    </div>

    <!-- Producto 5 -->
    <div class="card">
        <img src="audifonos.jpg">
        <h3>Audífonos Gamer</h3>
        <p class="descripcion">Audio envolvente</p>
        <p class="precio">$1200</p>

        <div class="acciones">
            <button class="fav" onclick="toggleFav(this)">🤍</button>
            <button class="carrito">🛒 Agregar</button>
        </div>
    </div>

</div>

<script>
function toggleFav(btn) {
    if (btn.innerText === "🤍") {
        btn.innerText = "❤️";
    } else {
        btn.innerText = "🤍";
    }
}
</script>

</body>
</html>
```

Posteriormente los archivos fueron cargados a Netlify, lo que generó un enlace público para acceder al sitio.
primero se subieron los archivos aqui:

<img width="641" height="259" alt="image" src="https://github.com/user-attachments/assets/23ab4772-0d02-4a95-9ab8-4c4e31037b04" />

y solo se selecciono estos archivos, que son las imagenes y el archivo de html:

<img width="543" height="298" alt="image" src="https://github.com/user-attachments/assets/b8525511-6eac-4d7d-b4c9-86ce88c2edf4" />

y finalmente se cargo en netlify y genero un enlace:

<img width="812" height="284" alt="image" src="https://github.com/user-attachments/assets/4ff9f852-bfb2-4600-9329-496a01b39672" />

Link del proyecto: https://proyectointegradoru2.netlify.app/


## DIAGRAMA DE CLASES

El proyecto está organizado en dos archivos principales: main.py y producto.py.
Como anteriormente se ha dicho el main.py se encuentra la lógica principal de la aplicación, mientras que en producto.py se define la clase reutilizable que representa cada tarjeta de producto.

La clase principal de la aplicación crea la ventana, carga los datos de los productos y utiliza la clase Producto para mostrar cada elemento del catálogo.

La relación entre las clases funciona de la siguiente forma:
1.- main.py crea la aplicación y contiene la lista de productos.
2.- Por cada producto del arreglo, se crea un objeto de la clase Producto.
3.- La clase Producto genera visualmente la tarjeta del producto.
4.- Cada tarjeta se agrega al GridView, que organiza los elementos en forma de cuadrícula.

diagrama de clases

<img width="204" height="626" alt="image" src="https://github.com/user-attachments/assets/f79376b6-935c-44b4-815e-5eb4ed54c3e5" />

Este diagrama muestra que la clase Producto hereda de Container, lo que permite crear un componente visual reutilizable dentro de la aplicación.

## EXPLICACION DE LA HERENCIA

En este proyecto se utilizó el concepto de herencia de la programación orientada a objetos.

La clase personalizada se definió de la siguiente manera:
```class Producto(ft.Container):```

Esto significa que la clase Producto hereda de la clase Container del framework Flet.

Un Container es un componente que permite contener otros elementos visuales dentro de una interfaz gráfica.

Al heredar de esta clase, el componente Producto puede utilizar propiedades como:
- ancho (width)
- color de fondo (bgcolor)
- bordes redondeados (border_radius)
- sombras (shadow)
- contenido interno (content)

Gracias a esta herencia fue posible crear una tarjeta de producto personalizada que incluye:
- imagen
- nombre
- descripción
- precio
- botones de acción

Este enfoque permite reutilizar el mismo componente varias veces sin tener que escribir el diseño repetidamente.

## EXPLICACION DEL ASSETS

Para mostrar las imágenes de los productos se utilizó un directorio de recursos locales llamado assets.

Dentro de esta carpeta se almacenaron las imágenes utilizadas en el catálogo.

Estructura del proyecto:

<img width="144" height="265" alt="image" src="https://github.com/user-attachments/assets/600a26fb-dedf-4a39-817c-7599b1a5dedb" />


Para que el framework pueda reconocer estas imágenes se configuró el directorio de recursos dentro del código.

Ejemplo:

```page.assets_dir = "assets"```

Esta configuración indica que todas las imágenes utilizadas por la aplicación se encuentran dentro de la carpeta assets. Posteriormente las imágenes se cargan en el componente mediante el control Image.

Ejemplo:
```
ft.Image(
src=f"/assets/{imagen}",
width=230,
height=150
)
```

De esta forma el programa puede mostrar correctamente las imágenes correspondientes a cada producto.


# CODIGO
A continuacion se muestra el codigo completo

- modulo main.py
```
import flet as ft
from producto import Producto


productos = [

    {
        "id":1,
        "nombre":"Laptop Gamer",
        "descripcion":"Laptop para alto rendimiento",
        "precio":25000,
        "ruta_imagen":"laptop.jpg"
    },

    {
        "id":2,
        "nombre":"Mouse RGB",
        "descripcion":"Mouse gamer con luces",
        "precio":800,
        "ruta_imagen":"mouse.jpg"
    },

    {
        "id":3,
        "nombre":"Teclado Mecánico",
        "descripcion":"Teclado retroiluminado",
        "precio":1500,
        "ruta_imagen":"teclado.jpg"
    },

    {
        "id":4,
        "nombre":"Monitor 27",
        "descripcion":"Monitor Full HD",
        "precio":4500,
        "ruta_imagen":"pc.jpg"
    },

    {
        "id":5,
        "nombre":"Audífonos Gamer",
        "descripcion":"Audio envolvente",
        "precio":1200,
        "ruta_imagen":"audifonos.jpg"
    }

]


def main(page: ft.Page):

    page.title = "Tech Store"
    page.scroll = "auto"
    
    encabezado = ft.Text(
        "CATÁLOGO TECNOLÓGICO",
        size=30,
        weight="bold"
    )

    grid = ft.GridView(
        expand=True,
        runs_count=3,
        spacing=20,
        run_spacing=20
    )

    for p in productos:
        grid.controls.append(Producto(
            p["nombre"],
            p["descripcion"],
            p["precio"],
            p["ruta_imagen"],
        ))

    page.add(
        encabezado,
        grid
    )


ft.app(target=main, assets_dir="assets")
```

- modulo producto.py

```
import flet as ft
from pathlib import Path


class Producto(ft.Container):

    def __init__(self, nombre, descripcion, precio, imagen):
        super().__init__()

        self.width = 250
        self.bgcolor = "white"
        self.padding = 10
        self.border_radius = 10
        self.shadow = ft.BoxShadow(blur_radius=10)



        self.content = ft.Column(
            [
                ft.Image(
                    src=imagen,
                    width=230,
                    height=150,
                    fit=ft.BoxFit.COVER,
                ),
                ft.Text(nombre, weight="bold", size=16),
                ft.Text(descripcion, size=12, color="grey"),
                ft.Text(f"${precio}", color="green", weight="bold", size=16),

                ft.Row(
                    [
                        ft.IconButton(
                            icon=ft.Icons.FAVORITE_BORDER,
                            tooltip="Agregar a favoritos",
                            on_click=self._toggle_fav,
                        ),
                        ft.ElevatedButton("Agregar al carrito")
                    ],
                    alignment="spaceBetween"
                )
            ],
            spacing=5
        )

        self._is_fav = False

    def _toggle_fav(self, e: ft.ControlEvent):
        self._is_fav = not self._is_fav

        if self._is_fav:
            e.control.icon = ft.Icons.FAVORITE
            e.control.icon_color = "red"
        else:
           e.control.icon = ft.Icons.FAVORITE_BORDER
           e.control.icon_color = "grey"

        e.control.update()
```
# Programa
<img width="1911" height="552" alt="Captura de pantalla 2026-03-16 220112" src="https://github.com/user-attachments/assets/46e5d425-afe7-4394-b2b4-bb09f3820e67" />


<img width="1270" height="464" alt="Captura de pantalla 2026-03-16 220119" src="https://github.com/user-attachments/assets/89a7bcbb-d1d6-498c-b1f1-7a0a1f8b2d3c" />


<img width="620" height="580" alt="Captura de pantalla 2026-03-16 220127" src="https://github.com/user-attachments/assets/8de23f12-bff6-480c-9cea-97daca77a0cc" />

# Programa en pagina web (netlify)
link de la pagina: https://proyectointegradoru2.netlify.app/

<img width="1913" height="627" alt="image" src="https://github.com/user-attachments/assets/15aa7a28-f29a-4c98-97e8-23dbb860f89d" />

