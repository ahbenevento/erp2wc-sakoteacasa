# Trabajos realizados

> Según la versión publicada.

#### Versión 1.2.0

> **??/08/21**

1.  Envío del resumen de la importación por correo electrónico:
    1.  Productos con stock en cero.
    2.  Productos pasados a borrador.
    3.  Nuevos productos.

---

<small>

#### Versión 1.1.4

> **10/06/21**

1.  Corrección en el manejo de productos con precios menor igual a 0.

#### Versión 1.1.5

> **16/06/21**

1.  Corrección en el llamado al SP con un ID de depósito definido en "config.json".

#### Versión 1.1.3

> **10/06/21**

1.  En aquellos productos con stock menor a 0 se establece su cantidad en 0, pero el producto no pasa a borrador.

#### Versión 1.1.2

> **10/06/21**

1.  Los SKU de los productos son ignorados. En su reemplazo se utiliza el ID interno del ERP como código de búsqueda en la tienda Web.

#### Versión 1.1.1

> **05/06/21**

1.  Es posible comentar la razón por la que un producto es ignorado según su SKU.
2.  Durante una importación el ERRORLEVEL retornado por la aplicación será `100` si al menos el proceso alcanzó un producto modificado o registrado.

#### Versión 1.1.0

> **04/06/21**

1.  Al importar nuevos productos se marcan para no reservarse en ninguna venta.
2.  Los códigos de barra de los productos obtenidos desde la base de datos local son normalizados antes de importarse.

#### Versión 1.0.0

> **28/05/21**

1.  Obtiene la lista de productos desde la base de datos local.
2.  Puede gestionar más de una consulta ubicadas en el archivo `config.json` para obtener los productos según los filtros disponibles: **fecha**, **depósito**, **lista de precios**.
3.  Gestiona una cache local de productos para acelerar la importación diaria.
4.  Por cada producto, controla si realmente los datos han sido modificados para determinar si es necesaria su actualización.

</small>
