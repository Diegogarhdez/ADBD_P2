# ADBD_P2

Modelo Entidad/Relación del sistema de gestión de viveros

Este repositorio contiene el modelo Entidad/Relación correspondiente al escenario de gestión de viveros, zonas, productos, empleados, clientes y pedidos.

El modelo se ha representado mediante un diagrama E/R, incluyendo las entidades, atributos, relaciones y cardinalidades correspondientes.

Archivos del modelo

El repositorio debe contener los siguientes archivos:

.
├── modelo.drawio
├── modelo.png
└── README.md
modelo.drawio: diagrama Entidad/Relación en formato editable de diagrams.net (Draw.io).
modelo.png: representación gráfica del modelo en formato PNG.
README.md: descripción detallada del modelo, sus entidades, atributos, relaciones, cardinalidades y restricciones semánticas.
1. Entidades

El modelo está compuesto por las siguientes entidades:

Vivero
Zona
Producto
Empleado
Cliente
Pedido
1.1. Vivero

La entidad Vivero representa cada uno de los viveros gestionados por el sistema.

Atributos
Atributo	Descripción	Dominio / Ejemplo
ID	Identificador único del vivero.	Entero positivo. Ejemplo: 15
Latitud	Coordenada geográfica de la ubicación del vivero.	Número real entre -90 y 90. Ejemplo: 28.4636
Longitud	Coordenada geográfica de la ubicación del vivero.	Número real entre -180 y 180. Ejemplo: -16.2518

El atributo ID identifica de forma unívoca a cada vivero.

Ejemplo:

Vivero
ID: 15
Latitud: 28.4636
Longitud: -16.2518
1.2. Zona

La entidad Zona representa una zona geográfica en la que pueden encontrarse uno o varios viveros.

Atributos
Atributo	Descripción	Dominio / Ejemplo
ID	Identificador único de la zona.	Entero positivo. Ejemplo: 3
Nombre Zona	Nombre que identifica la zona.	Cadena de caracteres. Ejemplo: "Zona Norte"
Latitud	Coordenada geográfica asociada a la zona.	Real entre -90 y 90. Ejemplo: 28.5000
Longitud	Coordenada geográfica asociada a la zona.	Real entre -180 y 180. Ejemplo: -16.3000

Ejemplo:

Zona
ID: 3
Nombre Zona: "Zona Norte"
Latitud: 28.5000
Longitud: -16.3000
1.3. Producto

La entidad Producto representa los diferentes productos que pueden estar disponibles en los viveros.

Atributos
Atributo	Descripción	Dominio / Ejemplo
ID	Identificador único del producto.	Entero positivo. Ejemplo: 102
Tipo Producto	Tipo o categoría a la que pertenece el producto.	Cadena de caracteres. Ejemplo: "Planta ornamental"

Ejemplo:

Producto
ID: 102
Tipo Producto: "Planta ornamental"

El identificador permite distinguir productos incluso cuando varios pertenecen al mismo tipo.

1.4. Empleado

La entidad Empleado representa a las personas que trabajan en los viveros y gestionan los pedidos.

Atributos
Atributo	Descripción	Dominio / Ejemplo
DNI	Identificador oficial del empleado.	Cadena con formato de DNI. Ejemplo: "12345678A"
Nombre	Nombre del empleado.	Cadena de caracteres. Ejemplo: "Juan Pérez"

El DNI identifica de forma única a cada empleado.

Ejemplo:

Empleado
DNI: "12345678A"
Nombre: "Juan Pérez"
1.5. Cliente

La entidad Cliente representa a las personas que realizan pedidos en el sistema.

Atributos
Atributo	Descripción	Dominio / Ejemplo
ID	Identificador único del cliente.	Entero positivo. Ejemplo: 25
Fecha ingreso	Fecha en la que el cliente se registró en el sistema.	Fecha válida. Ejemplo: 2026-09-15
Compras mensuales	Cantidad o volumen de compras realizadas mensualmente por el cliente.	Número no negativo. Ejemplo: 8
Bonificación	Bonificación asociada al cliente.	Valor o porcentaje no negativo. Ejemplo: 10%

El atributo Bonificación aparece representado mediante un doble óvalo, por lo que se interpreta como un atributo multivaluado en el modelo conceptual.

Ejemplo:

Cliente
ID: 25
Fecha ingreso: 2026-09-15
Compras mensuales: 8
Bonificación: 10%
1.6. Pedido

La entidad Pedido representa una solicitud realizada por un cliente.

Atributos
Atributo	Descripción	Dominio / Ejemplo
ID	Identificador único del pedido.	Entero positivo. Ejemplo: 5001

Ejemplo:

Pedido
ID: 5001
2. Relaciones

El modelo contiene las siguientes relaciones:

Pertenece
Contiene
Asignado
Realiza
Gestiona
2.1. Pertenece

La relación Pertenece establece la correspondencia entre un Vivero y una Zona.

Vivero ─── Pertenece ─── Zona
Cardinalidad
Un Vivero pertenece obligatoriamente a una única Zona: 1:1.
Una Zona puede tener uno o varios Viveros: 1:N.

Por tanto:

Zona 1 ───── N Vivero

Esto significa que una zona puede agrupar varios viveros, mientras que un vivero no puede pertenecer simultáneamente a varias zonas.

Ejemplo
Zona Norte
 ├── Vivero 1
 ├── Vivero 2
 └── Vivero 3
2.2. Contiene

La relación Contiene representa los productos disponibles en una zona.

Zona ─── Contiene ─── Producto
Cardinalidad

La relación es N:M:

Una Zona puede contener varios productos.
Un Producto puede estar disponible en varias zonas.

Por tanto:

Zona N ───── M Producto
Atributo de la relación

La relación posee el atributo:

Cantidad disponible

Este atributo indica la cantidad de un determinado producto disponible en una determinada zona.

Ejemplo
Zona Norte ─── Producto 102 ─── Cantidad disponible: 150
Zona Norte ─── Producto 205 ─── Cantidad disponible: 80
Zona Sur   ─── Producto 102 ─── Cantidad disponible: 40

El mismo producto puede aparecer en diferentes zonas con cantidades disponibles diferentes.

2.3. Asignado

La relación Asignado establece la asignación de empleados a viveros.

Vivero ─── Asignado ─── Empleado
Cardinalidad

Según el modelo:

Cada Vivero tiene asignado exactamente un Empleado: 1:1.
Un Empleado puede estar asignado a uno o varios Viveros: 1:N.

Por tanto:

Empleado 1 ───── N Vivero
Atributos de la relación

La relación contiene el atributo compuesto Puesto, que describe las características de la asignación del empleado.

Puesto está compuesto por:

Tipo tarea
Productividad
Fecha

A su vez, Fecha se descompone en:

Inicio
Fin
Ejemplo
Empleado: Juan Pérez
Vivero: Vivero 15

Puesto:
    Tipo tarea: "Mantenimiento"
    Productividad: 92
    Inicio: 2026-09-01
    Fin: 2026-12-31

De esta forma, las características del puesto pertenecen a la asignación, y no directamente al empleado ni al vivero.

2.4. Realiza

La relación Realiza representa los pedidos que realizan los clientes.

Cliente ─── Realiza ─── Pedido
Cardinalidad

Según el diagrama:

Un Cliente realiza uno o varios pedidos: 1:N.
Cada Pedido pertenece a un único cliente: 1:1.

Por tanto:

Cliente 1 ───── N Pedido
Ejemplo
Cliente 25
 ├── Pedido 5001
 ├── Pedido 5002
 └── Pedido 5003

Los tres pedidos pertenecen al mismo cliente, pero cada pedido está asociado a un único cliente.

2.5. Gestiona

La relación Gestiona representa la gestión de los pedidos por parte de los empleados.

Empleado ─── Gestiona ─── Pedido
Cardinalidad

Según el modelo:

Un Empleado puede gestionar uno o varios pedidos: 1:N.
Cada Pedido es gestionado por un único empleado: 1:1.

Por tanto:

Empleado 1 ───── N Pedido
Ejemplo
Empleado: Juan Pérez
 ├── Pedido 5001
 ├── Pedido 5004
 └── Pedido 5008

Esto permite determinar qué empleado se encarga de cada pedido.

3. Resumen de cardinalidades
Relación	Entidad 1	Entidad 2	Cardinalidad
Pertenece	Vivero	Zona	N:1
Contiene	Zona	Producto	N:M
Asignado	Vivero	Empleado	1:N
Realiza	Cliente	Pedido	1:N
Gestiona	Empleado	Pedido	1:N

De forma equivalente, tomando como referencia la entidad que aparece primero en la tabla:

Vivero   N ─── 1 Zona
Zona     N ─── M Producto
Vivero   1 ─── N Empleado
Cliente  1 ─── N Pedido
Empleado 1 ─── N Pedido

Nota: las cardinalidades se han interpretado directamente a partir de las etiquetas 1:1, 1:N y N:M del diagrama.

4. Dominios de los atributos

Para garantizar la coherencia de los datos, se pueden establecer los siguientes dominios:

Identificadores

Los atributos:

Vivero.ID
Zona.ID
Producto.ID
Cliente.ID
Pedido.ID

deben ser valores enteros positivos y únicos dentro de su entidad.

Coordenadas

Los atributos Latitud y Longitud deben respetar los rangos geográficos estándar:

-90 ≤ Latitud ≤ 90
-180 ≤ Longitud ≤ 180

Por ejemplo:

Latitud: 28.4636   ✓
Longitud: -16.2518 ✓

Mientras que:

Latitud: 120       ✗
Longitud: -250     ✗

no serían valores válidos.

Fechas

Fecha ingreso, Inicio y Fin deben corresponder a fechas válidas.

Además, para una asignación:

Inicio ≤ Fin
Cantidad disponible

Cantidad disponible debe ser un número entero mayor o igual que cero:

Cantidad disponible ≥ 0

No tendría sentido almacenar una cantidad negativa de productos.

Compras mensuales

Compras mensuales debe ser un número no negativo:

Compras mensuales ≥ 0
Productividad

La productividad debería representar un valor no negativo. Si se interpreta como porcentaje:

0 ≤ Productividad ≤ 100
DNI

El DNI debe ser único para cada empleado y respetar el formato establecido para los documentos nacionales de identidad.

5. Restricciones semánticas

Además de las restricciones estructurales derivadas de las cardinalidades, se proponen las siguientes restricciones semánticas.

5.1. Identificadores únicos

Los identificadores de cada entidad deben ser únicos.

Vivero.ID       → único
Zona.ID         → único
Producto.ID     → único
Cliente.ID      → único
Pedido.ID       → único
Empleado.DNI    → único
5.2. Un pedido pertenece a un único cliente

Un pedido no puede estar asociado simultáneamente a varios clientes.

Pedido → exactamente un Cliente
5.3. Un pedido es gestionado por un único empleado

Cada pedido debe tener asignado un único empleado responsable de su gestión.

Pedido → exactamente un Empleado
5.4. Un vivero pertenece a una única zona

Un vivero no puede pertenecer simultáneamente a diferentes zonas.

Vivero → exactamente una Zona
5.5. Cantidades no negativas

La cantidad disponible de un producto nunca puede ser negativa:

Cantidad disponible ≥ 0
5.6. Coherencia temporal de los puestos

Cuando una asignación tenga una fecha de inicio y una fecha de finalización:

Fecha inicio ≤ Fecha fin

Además, una asignación no debería tener una fecha de finalización anterior a su fecha de inicio, porque incluso las bases de datos tienen límites para la creatividad.

5.7. Consistencia geográfica

Las coordenadas de viveros y zonas deben encontrarse dentro de los rangos válidos de latitud y longitud.

Esto evita almacenar ubicaciones físicamente imposibles.

5.8. Integridad referencial

Las relaciones deben mantener la correspondencia entre las entidades involucradas.

Por ejemplo, no debería existir un pedido asociado a un cliente inexistente ni un pedido gestionado por un empleado que no esté registrado en el sistema.

6. Resumen del modelo

El modelo representa un sistema en el que:

Los viveros están situados dentro de zonas.
Las zonas disponen de diferentes productos, indicando la cantidad disponible de cada uno.
Los empleados se asignan a los viveros y dicha asignación puede contener información sobre el puesto, las tareas, la productividad y el periodo de asignación.
Los clientes realizan pedidos.
Los empleados gestionan esos pedidos.
Las restricciones de cardinalidad garantizan que las relaciones entre las distintas entidades sean coherentes.
Los dominios de los atributos evitan valores inválidos, como coordenadas imposibles, cantidades negativas o fechas inconsistentes.

En conjunto, el modelo permite representar la estructura básica del sistema manteniendo separadas las entidades principales y utilizando relaciones para representar las asociaciones entre ellas.
