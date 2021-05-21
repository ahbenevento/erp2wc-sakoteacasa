Esta página describe el funcionamiento de la herramienta encargada de importar los productos de la base de datos local hacia la tienda Web.

<small>Actualización: **19/05/2021**.</small>

## Instalación

Descargue el archivo `.zip` con la última versión y descomprímala en la carpeta deseada.

Esta herramienta de importación es una aplicación de consola por lo que es aconsejable abrir una terminal para realizar las primeras pruebas.

## Configuración

En la carpeta donde ha sido instalada la herramienta encontrará un archivo llamado `config.json`. El mismo contiene toda la configuración para el proceso de importación de productos.

### Características más importantes del archivo de configuración

| Opción | Descripción |
|--------|-------------|
|`uri_estado`|Contiene la dirección al servicio encargado de brindar cierta información sensible como los accesos a la base de datos, etc. **No se podrá realizar ninguna importación si esta configuración no se establece correctamente.**|
|`log.carpeta`|Permite definir el directorio donde se guardarán los archivos `.log` con los resultados de cada importación realizada. El símbolo `$` será reemplazado por la carpeta donde la herramienta ha sido instalada.|
|`log.backup`|Permite indicar la cantidad de días que los archivos `.log` serán guardados.|
|`cache.repositorio`|Permite definir la carpeta donde funcionará la cache de productos locales. El símbolo `$` será reemplazado por la carpeta donde la herramienta ha sido instalada.|
|`acceso_local.driver`|Define el driver utilizado para conectarse a la base de datos local. Por el momento el valor soportado es: `sqlserver`.|
|`acceso_local.dsn`|Permite definir información extra en la ruta **DSN** utilizada para conectarse con la base de datos local. Por ejemplo: `server` para indicar la IP del servidor.|
|`consultas`|Contiene al menos una consulta (activa) utilizada para obtener la lista de productos desde la base de datos local. Consulte más abajo para conocer cómo configurar estas consultas.|
|`http.espera`|Permite definir la cantidad máxima en segundos a esperar ante cualquier consulta **HTTP** realizada.|
|`wc.sin_categoria`|Permite definir el alias utilizado para indicar que los productos no cuentan con una categoría definida.|
|`wc.api.paginado`|Permite definir la cantidad de productos a obtener en cada consulta. El valor máximo es: **100**.|
|`wc.api.max_consultas_individuales`|Define la cantidad máxima de productos que podrían consultarse de forma individual, y no mediante el consultas masivas. Si se establece en **0** se calculará el valor automáticamente.|

#### Cómo definir consultas

Cada consulta debe estar definida con su nombre dentro de la configuración `consultas` del archivo `config.json`. La siguiente tabla muestra los parámetros posibles a configurar en cada consulta.


| Opción | Descripción |
|--------|-------------|
|`activo`|Permite indicar mediante los valores **true** o **false**, si la consulta se encuentra activa. La primera consulta activa que se encuentre definida será la predeterminada.|
|`no_probar`|Defina con **true** o **false**, si la configuración puede utilizarse o no durante una prueba de conexión.|
|`obj`|El nombre de la tabla, vista o *stored procedure* utilizado para obtener la lista de productos.|
|`desde_fecha`|La fecha de actualizacón de productos mínima a tener en cuenta (en formato: **AAAAMMDD**).|
|`id_deposito`|El código del depósito utilizado para obtener el stock de los productos.|
|`id_lista_precios`|El código de la lista de precios utilizada.|

## Modo de uso

La herramienta puede utilizarse de dos formas:

> Pruebas de conexión

```
erp2wc probar
    [--origen <nombre>]
```

**Permite realizar una prueba de conexión** local a la base de datos y a la API de la tienda Web. Debería utilizarse una vez realizada la instalación, y cuando la configuración del equipo o la red cambien.

\* Las opciones encerradas entre corchetes ([]) son opcionales.

### Opciones

| Opción | Descripción |
|-------:|-------------|
|**--origen&nbsp;&lt;nombre&gt;**|Define la consulta utilizada para obtener la lista de productos desde la base de datos local. `<nombre>` contiene el identificador de la consulta definida en **consultas** dentro del archivo **config.json**.|

> Importación

```
erp2wc importar
    [--origen <nombre>] [--ttl <segundos>]
    [--solo-nuevos | --solo-existentes]
    [--nocache]
    [--ro] [-v]
```

| Opción | Descripción |
|-------:|-------------|
|**&#45;&#45;origen&nbsp;&lt;nombre&gt;**|Define la consulta utilizada para obtener la lista de productos desde la base de datos local. `<nombre>` contiene el identificador de la consulta definida en **consultas** dentro del archivo **config.json**.|
|**--ttl&nbsp;&lt;segundos&gt;**|Define el tiempo de espera en segundos ante cualquier consulta *HTTP* realizada. El valor de `<segundos>` reemplazará al definido en **http.espera** en el archivo **config.json**.|
|**--solo-nuevos**|Establece que solo se registrarán aquellos productos que aún no existan en la tienda Web, ignorando cualquier modificación de productos ya existentes.|
|**--solo-existentes**|Establece que solo se actualizán los productos existentes en la tienda Web.|
|**--nocache**|Deshabilita la cache utilizada para determinar si los productos han sido modificados desde la última actualización. No recomendado.|
|**--ro**|Realiza solo las consultas "**read only**". Puede utilizarse para probar el proceso sin actualizar los productos en la Web.|
|**-v**|Muestra más información durante el proceso de importación.|

\* Las opciones encerradas entre corchetes ([]) son opcionales.

---

<small>Desarrollado por **[Pragmática](http://pragmatica.com.ar)**.</small>
