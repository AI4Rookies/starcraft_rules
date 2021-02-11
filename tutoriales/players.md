# Creando nuestros jugadores

Una vez que hemos instalado y comprobado que nuestro sistema funciona correctamente podemos empezar a crear nuestro bots. 

**Paso 1: La estructura del agent (jugador)**

Para desarrollar nuestro jugador vamos a utilizar python como lenguaje de programación. Para ello tendremos que crear nuestro jugador en la carpeta agents que encuentra dentro del código que descargamos del repositorio de DeepMind en el tutorial anterior. Para construir nuestro bots podemos crear un agente desde cero o podemos extender el agente base que está disponible en la carpeta agent que tiene el siguiente código:

```
# Librerías básicos de python 
from __future__ import absolute_import
from __future__ import division
from __future__ import print_function

# Carga de funcionalidades de los conectores de la librerías pysc2
# para poder interactuar con el juego. 

from pysc2.lib import actions

# Estructura del agente que es de tipo objeto.
class BaseAgent(object):

  # Método de creación. En este método podeis incluir todo aquellos que creais necesario al inicio del juego.
  # Por ejemplo: variables especiales que nos servirán para tomar decisiones. 
  # Por ejemplo: el proceso de carga de nuestro algoritmo de Inteligencia Artificial. 
  
  def __init__(self):
    self.reward = 0
    self.episodes = 0
    self.steps = 0
    self.obs_spec = None
    self.action_spec = None

  def setup(self, obs_spec, action_spec):
    self.obs_spec = obs_spec
    self.action_spec = action_spec
  
  def reset(self):
    self.episodes += 1

  # Método de ejecución de acciones: Este es el método más importante ya que es el método mediante el cual 
  # podemos ejecutar nuestras acciones y obtener la puntuación obtenida tras la ejecución de la anterior 
  # o las anteriores. 
  
  def step(self, obs):
    self.steps += 1
    self.reward += obs.reward
    return actions.FunctionCall(actions.FUNCTIONS.no_op.id, [])
    
  # Dentro de este método deberemos incluir nuestros comportamientos
  # que ejecutaremos mediante la función FunctionCall del objeto actions el cual tiene una serie de reglas:
  # 1. Sólo se puede ejecutar una acción. 
  # 2. La acción debe ser una acción válida.
  
```
Para conocer cuales son las acciones disponibles se pueden comprobar directamente en el código fuente del juego en el siguiente [enlace](https://github.com/deepmind/pysc2/blob/master/pysc2/lib/actions.py).

*  move_camera que nos permite mover la camara del juego. 
*  select_idle_worker que nos permite seleccionar un jugador ocioso. 

**Paso 2: Ejecutando nuestros agentes**

Una vez que tenemos claro el código de nuestro agentes. Podemos ejecutarlos con diferentes opciones. El programa agent que ejecuta el agente nos permite seleccionar 
las diferentes opciones. 

```
  --action_space: <FEATURES|RGB|RAW>: Which action space to use. Needed if you
    take both feature and rgb observations.
  --agent: Which agent to run, as a python path to an Agent class.
    (default: 'pysc2.agents.random_agent.RandomAgent')
  --agent2: Second agent, either Bot or agent class.
    (default: 'Bot')
  --agent2_name: Name of the agent in replays. Defaults to the class name.
  --agent2_race: <random|protoss|terran|zerg>: Agent 2's race.
    (default: 'random')
  --agent_name: Name of the agent in replays. Defaults to the class name.
  --agent_race: <random|protoss|terran|zerg>: Agent 1's race.
    (default: 'random')
  --[no]battle_net_map: Use the battle.net map version.
    (default: 'false')
  --bot_build: <random|rush|timing|power|macro|air>: Bot's build strategy.
    (default: 'random')
  --difficulty: <very_easy|easy|medium|medium_hard|hard|harder|very_hard|cheat_v
    ision|cheat_money|cheat_insane>: If agent2 is a built-in Bot, it's strength.
    (default: 'very_easy')
  --[no]disable_fog: Whether to disable Fog of War.
    (default: 'false')
  --feature_minimap_size: Resolution for minimap feature layers.
    (default: '64,64')
  --feature_screen_size: Resolution for screen feature layers.
    (default: '84,84')
  --game_steps_per_episode: Game steps per episode.
    (an integer)
  --map: Name of a map to use.
  --max_agent_steps: Total agent steps.
    (default: '0')
    (an integer)
  --max_episodes: Total episodes.
    (default: '0')
    (an integer)
  --parallel: How many instances to run in parallel.
    (default: '1')
    (an integer)
  --[no]profile: Whether to turn on code profiling.
    (default: 'false')
  --[no]render: Whether to render with pygame.
    (default: 'true')
  --rgb_minimap_size: Resolution for rendered minimap.
  --rgb_screen_size: Resolution for rendered screen.
  --[no]save_replay: Whether to save a replay at the end.
    (default: 'true')
  --step_mul: Game steps per agent step.
    (default: '8')
    (an integer)
  --[no]trace: Whether to trace the code execution.
    (default: 'false')
  --[no]use_feature_units: Whether to include feature units.
    (default: 'false')
  --[no]use_raw_units: Whether to include raw units.
    (default: 'false')
```

Por ejemplos, si yo quisiera ejecutar un agente con las siguientes opciones:

* Agente: Agente base
* Raza: Terrans
* Sin niebla de guerra
* Mapa: Mapa sencillo de 64x64. 
* Número de ejecuciones del agente: 10 iteraciones. 

```
python -m pysc2.bin.agent --map Simple64 --agent pysc2.agents.base_agent.BaseAgent --max_agent_steps 10 --agent_race terran --disable_fog
```


**Paso 3: Creando nuestro primer agente**

Para crear nuestro primer agente lo mejor es copiar el archivo del agente básico y darle un nuevo nombre. En mi caso lo voy a llamar simple agent. Una vez que lo hayamos creamos tenemos que compilar de nuevo el sistema de starcraft para que podamos utilizar nuestro agente mediante la utilización del siguiente comando:

```
python -m pysc2.bin.agent --map Simple64 --agent2 pysc2.agents.simple_agent.SimpleAgent
```

Una vez que hemos compilado el sistema de comunicación podemos ejecutar nuestro agente mediante el siguiente comando:

```
python -m pysc2.bin.agent --map Simple64 --agent2 pysc2.agents.simple_agent.SimpleAgent
```
