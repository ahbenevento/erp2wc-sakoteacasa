# Trabajos realizados

> Según la versión publicada.

#### Versión 1.1.0

> **04/06/21**

1.  Al importar nuevos productos se marcan para no reservarse en ninguna venta.
2.  Los códigos de barra de los productos obtenidos desde la base de datos local son normalizados antes de importarse.

---

<small>

#### Versión 1.0.0

> **28/05/21**

1.  Obtiene la lista de productos desde la base de datos local.
2.  Puede gestionar más de una consulta ubicadas en el archivo `config.json` para obtener los productos según los filtros disponibles: **fecha**, **depósito**, **lista de precios**.
3.  Gestiona una cache local de productos para acelerar la importación diaria.
4.  Por cada producto, controla si realmente los datos han sido modificados para determinar si es necesaria su actualización.

</small>