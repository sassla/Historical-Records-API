# SASSLA Historical Records API
Consulta registros sísmicos históricos de agencias oficiales internacionales.

## General
[SASSLA](https://github.com/sassla/sassla) proveé esta herramienta para facilitar la consulta, búsqueda y filtro de eventos sísmicos registrados por las agencias oficiales alrededor del mundo. Es posible consultar registros de las siguientes agencias:

- [Servicio Sismológico Nacional](http://www.ssn.unam.mx/) - UNAM México (SSN)
- [United States Geological Survey](https://www.usgs.gov/) (USGS)

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
|-----------|---------------------|-------------|
| **date**  | Obligatorio, string | Este parámetro especifica la fecha del evento sísmico en el siguiente formato: ```yyyy-MM-dd'T'HH:mm:ss```. La zona horaria varía por la región del evento. |
| **timestamp** | Obligatorio, número | Este parámetro especifica la fecha del evento sísmico en formato UNIX. |
| **source** | Obligatorio, matriz JSON | Consultar historical.sasslaapis.records.response.source |
| **parameters** | Obligatorio, matriz JSON | Consultar historical.sasslaapis.records.response.parameters |
| **intensity-reports** | Obligatorio, matriz JSON | Consultar historical.sasslaapis.records.response.intensity-reports |

### Recurso: historical.sasslaapis.records.response.source

