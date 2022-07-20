# SASSLA Historical Records API
Consulta registros sísmicos históricos de agencias oficiales internacionales.

## General
[SASSLA](https://github.com/sassla/sassla) proveé esta herramienta para facilitar la consulta, búsqueda y filtro de eventos sísmicos registrados por las agencias oficiales alrededor del mundo. Es posible consultar registros de las siguientes agencias:

- [Servicio Sismológico Nacional](http://www.ssn.unam.mx/) - UNAM México (SSN) - ID: SSN
- [United States Geological Survey](https://www.usgs.gov/) (USGS) - ID: USGS

## Funciones clave

| Función                      | Descripción                                                              |
|------------------------------|--------------------------------------------------------------------------|
| Últimos sismos               | Obtén los eventos de los últimos 7 días ordenados cronológicamente.      |
| Búsqueda por fecha           | Obtén los eventos ocurridos en una ventana de tiempo específica.         |
| Búsqueda por región          | Obtén los eventos cercanos a una ciudad o dentro de una zona específica. | 
| Búsqueda por parámetros      | Obtén los eventos con una magnitud y/o profundidad específica.           |
| Búsqueda por fuente          | Obtén los eventos de una fuente de datos específica.                     |

## Recursos REST: historical.sasslaapis.records
### Endpoint

```
https://historical.sasslaapis.com/records
```

> Este extremo aún no está habilitado. Esta documentación es una prueba de concepto.

### Recurso: historical.sasslaapis.records.request 
Representación de solicitud.

#### Method

```
GET
```

#### Headers

```json
{
   "Content-Type": "application/json",
   "Authorization": "key=API_KEY"
}
```

#### Body

```json
{
       "limit": 100,
       
        "filters": {
            "date-range": "1626763680...1658281682",

            "region": {
                "latitude": 19.42847,
                "longitude": -99.12766,
                "radius": 50
            },

            "parameters": {
                "min-magnitude": 1.0,
                "min-depth": null
            },

            "sources": ["SSN"]
        }
}
```

#### Sintaxis de la solicitud

| Parámtero | Uso | Descripción |
|-----------|-----|-------------|
| **limit** | Opcional, número | Este parámetro establece el número máximo de resultados en la respuesta. Máximo: ```500```. Mínimo: ```1```. Por defecto: ```100```. |
| **filters** | Obligatorio, matriz JSON | Consultar [historical.sasslaapis.records.request.filters](https://github.com/sassla/Historical-Records-API/blob/main/README.md#historicalsasslaapisrecordsrequestfilters)


### historical.sasslaapis.records.request.filters

| Parámtero | Uso | Descripción |
|-----------|-----|-------------|
| **date-range** | Obligatorio, string | Este parámetro establece el rango de fechas de la búsqueda en el siguiente formato: ```"since_unix_date...until_unix_date"```. Existen registros desde el año 1727. |
| **sources** | Opcional, arreglo de string | Este parámetro establece las fuentes de datos de la búsqueda (ID de la fuente de datos). Establecer ```null``` para utilizar todas las fuentes disponibles. |
| **region** | Opcional, matriz JSON | Este parámetro establece la región / localidad específica de la búsqueda. Establecer ```null``` para retornar eventos de todas las regiones en las fechas elegidas. Consultar [historical.sasslaapis.records.request.region](https://github.com/sassla/Historical-Records-API/blob/main/README.md#historicalsasslaapisrecordsrequestregion) |
| **parameters** | Opcional, matriz JSON | Este parámetro establece los parámetros específicos de la búsqueda. Establecer ```null``` para retornar eventos de cualquier magnitud o profundidad ocurrido en las fechas elegidas. Consultar [historical.sasslaapis.records.request.parameters](https://github.com/sassla/Historical-Records-API/blob/main/README.md) |


### historical.sasslaapis.records.request.region

| Parámtero | Uso | Descripción |
|-----------|-----|-------------|
| **latitude** | Obligatorio, Double | Este parámetro establece la latitud de la región de búsqueda. |
| **longitude** | Obligatorio, Double | Este parámetro establece la longitud de la región de búsqueda. |
| **radius** | Obligatorio, número | Este parámetro establece el radio en kilómetros. |


### historical.sasslaapis.records.request.parameters

| Parámtero | Uso | Descripción |
|-----------|-----|-------------|
| **min-magnitude** | Opcional, Double | Este parámetro establece la magnitud mínima de la búsqueda. |
| **min-depth** | Opcional, Double | Este parámetro establece la profundidad mínima de la búsqueda en kilómetros. Considerar que existen profundidades negativas. Ej.: ```-0.050``` km. |



### Recurso: historical.sasslaapis.records.response 
Representación de respuesta: Lista de eventos filtrados en formato JSON.

```json
[{
        "event": {
            "date": "2017-09-19T13:14:39",
            "timestamp": 1505844879,

            "source": {
                "id": "SSN",
                "display_name": "Servicio Sismológico Nacional"
            },

            "parameters": {
                "magnitude": 7.1,
                "magnitude_type": "MW",
                "depth": 51.2,

                "location": {
                    "latitude": 18.3297,
                    "longitude": -98.6712,
                    "name": "8 km al Noroeste de Chiautla de Tapia, Puebla, México"
                }
            },

            "intensity-reports": {
                "count": 7400,
                "event_id": 1505844879
            }
        }
}]
```
#### Sintaxis de la respuesta

| Parámtero | Uso | Descripción |
|-----------|-----|-------------|
| **date**  | Obligatorio, string | Este parámetro especifica la fecha del evento sísmico en el siguiente formato: ```yyyy-MM-dd'T'HH:mm:ss```. La zona horaria varía por la región del evento. |
| **timestamp** | Obligatorio, número | Este parámetro especifica la fecha del evento sísmico en formato UNIX. |
| **source** | Obligatorio, matriz JSON | Consultar [historical.sasslaapis.records.response.source](https://github.com/sassla/Historical-Records-API/blob/main/README.md#recurso-historicalsasslaapisrecordsresponsesource) |
| **parameters** | Obligatorio, matriz JSON | Consultar [historical.sasslaapis.records.response.parameters](https://github.com/sassla/Historical-Records-API/blob/main/README.md#recurso-historicalsasslaapisrecordsresponseparameters) |
| **intensity-reports** | Obligatorio, matriz JSON | Consultar [historical.sasslaapis.records.response.intensity-reports](https://github.com/sassla/Historical-Records-API/blob/main/README.md#recurso-historicalsasslaapisrecordsresponseparametersintensity-reports) |


### historical.sasslaapis.records.response.source

| Parámtero | Uso | Descripción |
|-----------|-----|-------------|
| **id** | Obligatorio, string | Este parámetro especifica el identificador de la fuente de datos. Ej.: ```SSN, USGS```. |
| **display_name** | Obligatorio, string | Este parámetro especifica el nombre completo de la fuente de datos. Ej.: ```Servicio Sismológico Nacional``` |


### historical.sasslaapis.records.response.parameters


| Parámtero | Uso | Descripción |
|-----------|-----|-------------|
| **magnitude** | Obligatorio, Double | Este parámetro especifica la magnitud del evento sísmico. |
| **magnitude_type** | Opcional, string | Este parámetro especifica el tipo de magnitud calculada. Ej.: ```MW, ML, MWR, MWB```. Utilice ```MW``` por defecto. |
| **depth** | Obligatorio, Double | Este parámetro especifica la profundidad del foco sísmico en kilómetros. |
| **location** | Obligatorio, matriz JSON | [Consultar historical.sasslaapis.records.response.location](https://github.com/sassla/Historical-Records-API/blob/main/README.md#recurso-historicalsasslaapisrecordsresponseparameterslocation) |


### historical.sasslaapis.records.response.parameters.location

| Parámtero | Uso | Descripción |
|-----------|-----|-------------|
| **latitude** | Obligatorio, Double | Este parámetro especifica la latitud del evento. |
| **longitude** | Obligatorio, Double | Este parámetro especifica la longitud del evento. |
| **name** | Obligatorio, string | Este parámetro especifica la región / localidad donde se originó el evento sísmico. |


### historical.sasslaapis.records.response.intensity-reports

| Parámtero | Uso | Descripción |
|-----------|-----|-------------|
| **count** | Obligatorio, número | Este parámetro especifica el número de reportes de percepción generados por los usuarios desde SASSLA App |
| **event_id** | Obligatorio, número | Este parámetro especifica el identificador del evento sísmico para consultar los reportes de percepción asociados. Consultar Intensity-Reports-API. |


## Licencia
SASSLA-Historical-Records-API is licensed under the Apache License, version 2.0.
