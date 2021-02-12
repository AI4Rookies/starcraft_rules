# Extracción de datos

La información referente al estado del juego se denomina observaciones y será generada en cada una de la iteraciones del juego (step). Mediante esta información se puede obtener toda la información que el sistema de communicación puede extraer del juego. Esta información será accesible através del objeto obs de la función step. Este objeto contiene un gran conjunto de información referente a la localización de las unidades, el estado del jugador, etc. Para poder acceder a esta información se deberá utilizar la siguiente variables:

```
obs.observation
```

Que es un diccionario que nos permite acceder a los diferentes conjuntos de datos indicando el nombre de la propiedad a la que queramos acceder. La lista de posibles propiedades es la siguiente: 

*  single_select
*  multi_select
*  build_queue
*  cargo
*  production_queue
*  last_actions
*  cargo_slots_available
*  home_race_requested
*  away_race_requested
*  map_name
*  feature_screen
*  feature_minimap
*  action_result
*  alerts
*  game_loop
*  score_cumulative
*  score_by_category
*  score_by_vital
*  player
*  control_groups
*  upgrades
*  available_actions

Donde las propiedades más importantes son: (1) feature_screen que nos ofrece información sobre la pantalla del juego; (2) feature_minimap que nos ofrece información sobre el minimapa y (3) player que nos ofrece información sobre nuestro jugador. Por ejemplo si quisieramos mostrar la información del jugador deberiamos incluir el siguiente fragmento de código:

```
info = obs.observation["player"]
print(info)
```

Que mostraría un vector con la siguiente información:

```
[ 1 50  0 12 15  0 12  0  0  0  0]
```

cuyo significado es el siguiente:

```
['player_id', 'minerals', 'vespene', 'food_used', 'food_cap', 'food_army', 'food_workers', 'idle_worker_count', 'army_count', 'warp_gate_count', 'larva_count']
```

A la hora de desarrollar un agente es muy importante analizar que información tenemos disponibles y cual no para así poder decidir que acciones debemos aplicar. 
