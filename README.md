# Modelo Entidad/Relación

Este repositorio contiene el modelo Entidad/Relación correspondiente al sistema de gestión de viveros, zonas, productos, empleados, clientes y pedidos.

## Archivos del repositorio

El repositorio contiene los siguientes archivos:

- `modelo.drawio`: diagrama Entidad/Relación en formato editable de Draw.io.
- `modelo.png`: representación gráfica del modelo en formato PNG.
- `README.md`: documentación detallada del modelo Entidad/Relación.

---

# 1. Entidades

El modelo está compuesto por las siguientes entidades:

- **Vivero**
- **Zona**
- **Producto**
- **Empleado**
- **Cliente**
- **Pedido**

---

## 1.1. Vivero

La entidad **Vivero** representa cada uno de los viveros gestionados por el sistema.

### Atributos

| Atributo | Descripción |
|---|---|
| `ID` | Identificador único del vivero. |
| `Latitud` | Coordenada geográfica de la ubicación del vivero. |
| `Longitud` | Coordenada geográfica de la ubicación del vivero. |

### Ejemplo

Un vivero podría tener los siguientes valores:

- **ID:** `15`
- **Latitud:** `28.4636`
- **Longitud:** `-16.2518`

El atributo `ID` identifica de forma unívoca a cada vivero.

---

## 1.2. Zona

La entidad **Zona** representa una zona geográfica en la que se encuentran uno o varios viveros.

### Atributos

| Atributo | Descripción |
|---|---|
| `ID` | Identificador único de la zona. |
| `Nombre Zona` | Nombre identificativo de la zona. |
| `Latitud` | Coordenada geográfica asociada a la zona. |
| `Longitud` | Coordenada geográfica asociada a la zona. |

### Ejemplo

Una zona podría tener los siguientes valores:

- **ID:** `3`
- **Nombre Zona:** `Zona Norte`
- **Latitud:** `28.5000`
- **Longitud:** `-16.3000`

---

## 1.3. Producto

La entidad **Producto** representa los diferentes productos disponibles en las zonas gestionadas por el sistema.

### Atributos

| Atributo | Descripción |
|---|---|
| `ID` | Identificador único del producto. |
| `Tipo Producto` | Tipo o categoría del producto. |

### Ejemplo

Un producto podría tener los siguientes valores:

- **ID:** `102`
- **Tipo Producto:** `Planta ornamental`

El `ID` permite diferenciar productos aunque pertenezcan al mismo tipo.

---

## 1.4. Empleado

La entidad **Empleado** representa a las personas que trabajan en los viveros y se encargan de gestionar los pedidos.

### Atributos

| Atributo | Descripción |
|---|---|
| `DNI` | Identificador del empleado. |
| `Nombre` | Nombre del empleado. |

### Ejemplo

Un empleado podría tener los siguientes valores:

- **DNI:** `12345678A`
- **Nombre:** `Juan Pérez`

El `DNI` identifica de forma unívoca a cada empleado.

---

## 1.5. Cliente

La entidad **Cliente** representa a las personas registradas en el sistema que pueden realizar pedidos.

### Atributos

| Atributo | Descripción |
|---|---|
| `ID` | Identificador único del cliente.
| `Fecha ingreso` | Fecha en la que el cliente se registró en el sistema. |
| `Compras mensuales` | Número de compras realizadas por el cliente durante un mes. |
| `Bonificación` | Bonificación asociada al cliente. |

### Ejemplo

Un cliente podría tener los siguientes valores:

- **ID:** `25`
- **Fecha ingreso:** `2026-09-15`
- **Compras mensuales:** `8`
- **Bonificación:** `10%`

En el diagrama, `Bonificación` aparece representada mediante un doble óvalo, por lo que se considera un atributo multivaluado.

---

## 1.6. Pedido

La entidad **Pedido** representa una solicitud realizada por un cliente.

### Atributos

| Atributo | Descripción |
|---|---|
| `ID` | Identificador único del pedido.

### Ejemplo

Un pedido podría tener:

- **ID:** `5001`

Cada pedido se identifica de forma única mediante su `ID`.

---

# 2. Relaciones

El modelo contiene las siguientes relaciones:

1. **Pertenece**
2. **Contiene**
3. **Asignado**
4. **Realiza**
5. **Gestiona**

---

## 2.1. Pertenece

La relación **Pertenece** establece la relación entre los viveros y las zonas.

### Cardinalidad

- Cada **Vivero** pertenece a una única **Zona**.
- Una **Zona** puede tener uno o varios **Viveros**.

Por tanto, la relación es de tipo **1:N**, considerando `Zona` como el lado 1 y `Vivero` como el lado N.

### Ejemplo

Una zona puede contener varios viveros:

- Zona Norte → Vivero 1
- Zona Norte → Vivero 2
- Zona Norte → Vivero 3

Sin embargo, un vivero concreto solo puede pertenecer a una única zona.

---

## 2.2. Contiene

La relación **Contiene** representa los productos disponibles en cada zona.

### Cardinalidad

La relación es de tipo **N:M**:

- Una **Zona** puede contener varios **Productos**.
- Un **Producto** puede encontrarse en varias **Zonas**.

### Atributos de la relación

La relación posee el atributo:

- `Cantidad disponible`

Este atributo representa la cantidad disponible de un determinado producto dentro de una determinada zona.

### Ejemplo

Una posible situación sería:

| Zona | Producto | Cantidad disponible |
|---|---|---:|
| Zona Norte | Producto 102 | 150 |
| Zona Norte | Producto 205 | 80 |
| Zona Sur | Producto 102 | 40 |

El producto `102` puede encontrarse en varias zonas y tener una cantidad disponible diferente en cada una de ellas.

---

## 2.3. Asignado

La relación **Asignado** representa la asignación de empleados a viveros.

### Cardinalidad

- Un **Vivero** tiene asignado un **Empleado**.
- Un **Empleado** puede estar asignado a uno o varios **Viveros**.

Por tanto, la relación es de tipo **1:N**, considerando `Empleado` como el lado 1 y `Vivero` como el lado N.

### Atributo compuesto `Puesto`

La relación posee el atributo compuesto `Puesto`, que contiene:

- `Tipo tarea`
- `Productividad`
- `Fecha`

A su vez, el atributo `Fecha` está compuesto por:

- `Inicio`
- `Fin`

Estos atributos describen las características de la asignación concreta de un empleado a un vivero.

### Ejemplo

Una asignación podría ser:

| Atributo | Valor |
|---|---|
| Empleado | Juan Pérez |
| Vivero | 15 |
| Tipo tarea | Mantenimiento |
| Productividad | 92 |
| Inicio | 2026-09-01 |
| Fin | 2026-12-31 |

La información del puesto pertenece a la relación de asignación y no directamente al empleado o al vivero.

---

## 2.4. Realiza

La relación **Realiza** representa los pedidos realizados por los clientes.

### Cardinalidad

- Un **Cliente** puede realizar uno o varios **Pedidos**.
- Cada **Pedido** es realizado por un único **Cliente**.

Por tanto, la relación es de tipo **1:N**, considerando `Cliente` como el lado 1 y `Pedido` como el lado N.

### Ejemplo

Un cliente puede realizar varios pedidos:

- Cliente 25 → Pedido 5001
- Cliente 25 → Pedido 5002
- Cliente 25 → Pedido 5003

Los tres pedidos pertenecen al cliente `25`, mientras que cada pedido está asociado exclusivamente a ese cliente.

---

## 2.5. Gestiona

La relación **Gestiona** representa la gestión de los pedidos por parte de los empleados.

### Cardinalidad

- Un **Empleado** puede gestionar uno o varios **Pedidos**.
- Cada **Pedido** es gestionado por un único **Empleado**.

Por tanto, la relación es de tipo **1:N**, considerando `Empleado` como el lado 1 y `Pedido` como el lado N.

### Ejemplo

Un empleado puede gestionar varios pedidos:

- Juan Pérez → Pedido 5001
- Juan Pérez → Pedido 5004
- Juan Pérez → Pedido 5008

De esta forma, cada pedido tiene un empleado responsable de su gestión.

---

# 3. Resumen de cardinalidades

| Relación | Entidad 1 | Cardinalidad | Entidad 2 |
|---|---|---|---|
| `Pertenece` | Zona | `1:N` | Vivero |
| `Contiene` | Zona | `N:M` | Producto |
| `Asignado` | Empleado | `1:N` | Vivero |
| `Realiza` | Cliente | `1:N` | Pedido |
| `Gestiona` | Empleado | `1:N` | Pedido |

---

# 4. Restricciones semánticas

Además de las restricciones estructurales derivadas de las cardinalidades, se establecen las siguientes restricciones semánticas.

## 4.1. Identificadores únicos

Los identificadores de cada entidad deben ser únicos:

- `Vivero.ID` → único.
- `Zona.ID` → único.
- `Producto.ID` → único.
- `Cliente.ID` → único.
- `Pedido.ID` → único.
- `Empleado.DNI` → único.

No puede haber dos entidades del mismo tipo con el mismo identificador.

---

## 4.2. Un vivero pertenece a una única zona

Cada vivero debe estar asociado a una única zona.

Un mismo vivero no puede pertenecer simultáneamente a dos zonas diferentes.

---

## 4.3. Un pedido pertenece a un único cliente

Cada pedido debe estar asociado a un único cliente.

Un pedido no puede pertenecer simultáneamente a dos clientes diferentes.

---

## 4.4. Un pedido es gestionado por un único empleado

Cada pedido debe ser gestionado por un único empleado.

Esto permite identificar al empleado responsable de cada pedido.

---

## 4.5. Cantidades no negativas

La cantidad disponible de cualquier producto no puede ser negativa.

Por tanto:

- `Cantidad disponible ≥ 0`

---

## 4.6. Coherencia temporal

Cuando una asignación tenga una fecha de inicio y una fecha de finalización, debe cumplirse:

- `Fecha inicio ≤ Fecha fin`

No puede existir una asignación cuyo periodo finalice antes de comenzar.

---

## 4.7. Coordenadas válidas

Las coordenadas geográficas de los viveros y las zonas deben encontrarse dentro de los rangos válidos:

- `-90 ≤ Latitud ≤ 90`
- `-180 ≤ Longitud ≤ 180`

---

## 4.8. Integridad referencial

Las relaciones entre entidades deben mantener la correspondencia entre los registros existentes.

Por ejemplo:

- No puede existir un pedido asociado a un cliente inexistente.
- No puede existir un pedido gestionado por un empleado inexistente.
- No puede existir un vivero asociado a una zona inexistente.
- No puede existir una relación `Contiene` entre una zona inexistente y un producto inexistente.

---

# 5. Resumen del modelo

El modelo representa un sistema de gestión de viveros en el que:

1. Los **Viveros** pertenecen a determinadas **Zonas**.
2. Las **Zonas** contienen diferentes **Productos**, indicando la cantidad disponible de cada uno.
3. Los **Empleados** se asignan a los **Viveros**.
4. La asignación de un empleado a un vivero contiene información sobre el **Puesto**, incluyendo el tipo de tarea, la productividad y el periodo de asignación.
5. Los **Clientes** realizan **Pedidos**.
6. Los **Empleados** gestionan los **Pedidos**.
7. Las cardinalidades establecen las restricciones de participación de cada entidad en las diferentes relaciones.
8. Los dominios y restricciones semánticas permiten garantizar la coherencia de los datos almacenados.

El modelo Entidad/Relación constituye la representación conceptual del sistema y puede utilizarse posteriormente como base para su transformación al correspondiente modelo relacional.
