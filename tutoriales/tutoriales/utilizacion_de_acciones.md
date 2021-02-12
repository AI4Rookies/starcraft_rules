# Creando nuestros jugadores

Una vez que conocemos la información que tenemos disponible, es posible utilizar esta información para definir las acciones a realizar, para ellos describiremos como realizar tres acciones básicas para el jugador: (1) seleccionar una unidad; (2) construir un edificio y (3) entrenar una unidad. 

**Paso 1: Seleccionando una unidad**

Para seleccionar una unidad es necesario utilizar la información del mapa con el objetivo de extraer la información referentes a las unidades de nuestra raza. Para ello deberemos implementar el siguiente código:


```
# Variables globales que define en tipo de unidades disponibles en la pantalla y el identificador de la unidad a seleccionar.  

UNIT_TYPE = features.SCREEN_FEATURES.unit_type.index
WORKER_ID = 45

# Identificador de la operación de selección
SELECT_POINT_OP = actions.FUNCTIONS.select_point.id

# Definición del modelo de ejecución de la acción
NOT_QUEUED_MODE = [0]
```

A continuación debemos definir el código que se corresponde al proceso de selección de la unidad de la siguiente manera. 

```
# Deberemos seleccionar las unidades disponible en la pantalla. 
# para ello realizaremos las siguientes opciones.

# Extraeremos todas las unidades disponibles en la pantalla. 
unit_type = obs.observation["feature_screen"][UNIT_TYPE]

# Seleccionaremos aquellas que son de tipo trabajador cuyo código está almacenado en la variables WORKER_ID. 
unit_y, unit_x = (unit_type == WORKER_ID).nonzero()

# De entre todas las unidades disponibles seleccionaremos el primero de los trabajadores. 
target = [unit_x[0], unit_y[0]]

# Ejecutaremos la acción en modo de no encolado.  
return actions.FunctionCall(SELECT_POINT_OP, [NOT_QUEUED_MODE, target])
```

La ejecución de acciones en Starcraft II se puede realizar mediante dos modalidades:

* NOT_QUEUED_MODE: Se corresponde con ejecución inmediata, por lo que se realizar antes que las acciones encoladas. 
* QUEUED_MODE: Se corresponde con la ejecución diferida en modo cola, de manera que la acción se ejecutará después de que se ejecuten el resto de acciones. 


**Paso 2: Construyendo un edificio**


**Paso 3: Entrenando una unidad**
