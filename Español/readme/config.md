---
icon: wrench
---

# Configuración

El archivo `config.yml` tiene muchas opciones para editar el comportamiento de tu servidor, como establecer el sistema de elecciones.

En la configuración, encontrarás muchas cosas. Se explica dentro de la configuración.

Puedes ver la configuración predeterminada completa a continuación:

```yml
# ============================================================================
#  TownyElections - Configuración
# ============================================================================
#  Un sistema de elecciones formal y configurable para pueblos de Towny.
#  Documentación y soporte: ver README.md
# ============================================================================

# No editar. Usado internamente para migrar la configuración en las actualizaciones.
config-version: 1

# Configuración general del plugin.
general:
  # Idioma para el archivo de mensajes (messages_<locale>.yml). Por defecto "en".
  locale: "en"
  # Si es true, se registra información de depuración adicional en la consola.
  debug: false
  # Habilitar estadísticas de uso anónimas a través de bStats (https://bstats.org).
  metrics: true

# ----------------------------------------------------------------------------
#  Comprobador de actualizaciones
# ----------------------------------------------------------------------------
# Al iniciar, TownyElections puede verificar las versiones estables más recientes en GitHub Releases
# (se ignoran las versiones beta y alpha). La verificación se ejecuta de forma asíncrona y nunca
# bloquea el servidor. Solo registra en la consola y, opcionalmente, notifica a los
# administradores al unirse. Nunca descarga ni instala nada.
update-checker:
  # Interruptor principal para la verificación de actualizaciones de GitHub Releases.
  enabled: true
  # Repositorio de GitHub en formato propietario/nombre.
  github-repository: "vingaming1113/TownyElections"
  # Notificar a los jugadores con townyelections.admin cuando se unan si existe una actualización.
  notify-admins-on-join: true

# ----------------------------------------------------------------------------
#  Configuración de elecciones
# ----------------------------------------------------------------------------
election:
  # Cuánto dura la *fase de nominación/campaña*, durante la cual los residentes pueden
  # registrarse como candidatos. Acepta una duración como: 30s, 10m, 2h, 3d, 1w.
  nomination-duration: "2d"

  # Cuánto dura la *fase de votación* una vez que las nominaciones cierran.
  voting-duration: "3d"

  # Número mínimo de candidatos requeridos para que una elección proceda a la votación.
  # Si se registran menos candidatos, la elección se cancela (o gana automáticamente, ver
  # "auto-win-single-candidate").
  min-candidates: 2

  # Número máximo de candidatos permitidos por elección. 0 = ilimitado.
  max-candidates: 0

  # Si solo un candidato se registra y min-candidates fallaría, ¿debe ese candidato ganar automáticamente?
  auto-win-single-candidate: true

  # Número mínimo de residentes que un pueblo debe tener antes de que una elección pueda realizarse.
  min-town-residents: 2

  # Cada residente puede emitir este número de votos por elección (normalmente 1).
  votes-per-resident: 1

  # Si es true, los jugadores pueden cambiar su voto mientras la fase de votación está abierta.
  allow-vote-changes: true

  # Si es true, los residentes pueden ver los recuentos de votos en vivo durante la votación. Si es false, los
  # recuentos se ocultan hasta que la elección concluye (voto secreto).
  public-live-results: true

  # ¿Pueden los candidatos votar por sí mismos?
  allow-self-vote: false

  # Sistema electoral utilizado para recolectar y contar los votos:
  #   PLURALITY - cada votante elige un candidato; el más votado gana
  #   RANKED_CHOICE - los votantes clasifican a los candidatos en orden de preferencia
  #                   (/election vote First Second Third ...). El conteo se ejecuta en
  #                   rondas de segunda vuelta instantánea: el candidato más débil
  #                   es eliminado y sus votos se transfieren a la siguiente preferencia
  #                   de cada votante hasta que alguien obtenga la mayoría.
  #   APPROVAL - los votantes aprueban cualquier número de candidatos
  #              (/election vote Alice Bob ...); el más aprobado gana
  # El sistema se bloquea cuando comienza una elección. Cambiar este valor nunca
  # reinterpreta las papeletas de una elección ya en curso.
  voting-system: "PLURALITY"

  # Estrategia de desempate cuando los principales candidatos están empatados:
  #   RANDOM - elegir un ganador aleatorio de los candidatos empatados
  #   EARLIEST - el candidato que se registró primero gana
  #   INCUMBENT - el alcalde actual gana si está empatado, de lo contrario RANDOM
  #   RUNOFF - iniciar una nueva ronda de votación corta entre los candidatos empatados
  #   NONE - declarar sin ganador (elección anulada)
  tie-breaker: "RUNOFF"

  # Duración de una ronda de votación de desempate (solo se usa cuando tie-breaker es RUNOFF).
  runoff-duration: "1d"

  # Iniciar automáticamente una nueva elección en cada pueblo elegible en un intervalo fijo.
  # Establecer enabled a false para ejecutar solo elecciones iniciadas manualmente a través de comandos.
  auto-schedule:
    enabled: true
    # Intervalo entre el *final* de una elección y el inicio automático de la
    # siguiente (por pueblo). Ejemplo: 30d para un ciclo mensual.
    interval: "14d"

  # Si es true, se cargará/recompensará el dinero de la cuenta de economía del pueblo (requiere una economía).
  # Puramente opcional.
  economy:
    # Costo para que un residente se registre como candidato. 0 = gratis.
    candidacy-cost: 10.0
    # Recompensa pagada al ganador de la nada (0 = deshabilitado).
    winner-reward: 500.0

  # Límite de votos por IP para prevenir el abuso de cuentas alternativas. Cuando está habilitado,
  # una cuenta por huella (IP) puede obtener una papeleta, hasta el número configurado de huellas.
  # Las direcciones IP se hashean (SHA-256). Solo se guardan los hashes y los UUIDs de los votantes,
  # por lo que la protección sigue siendo efectiva después de reiniciar el servidor.
  ip-vote-limit:
    # Interruptor principal para el límite de votos por IP. false = deshabilitado (comportamiento actual).
    enabled: false
    # Número máximo de huellas de IP distintas permitidas para votar en una elección.
    # 0 = ilimitado (efectivamente deshabilitado incluso si enabled: true).
    max-votes: 0

# ----------------------------------------------------------------------------
#  Configuración de campaña
# ----------------------------------------------------------------------------
campaign:
  # Longitud máxima (caracteres) del mensaje de campaña de un candidato.
  max-message-length: 128
  # Mensaje de campaña predeterminado utilizado cuando un candidato no establece ninguno.
  default-message: "I would be honored to serve this town."
  # Longitud máxima (caracteres) del nombre de un partido escrito con /election party.
  # Esto protege la salida del chat y el autocompletado con pestañas de etiquetas muy largas.
  max-party-name-length: 32
  # Partido predeterminado mostrado hasta que un candidato elige uno.
  # Esto es a lo que los jugadores vuelven cuando usan /election party leave.
  default-party-name: "Independent"
  # Si es true, el partido predeterminado se oculta de /election parties y los resúmenes de resultados del partido.
  # Los candidatos aún mantienen la etiqueta en las listas de candidatos.
  hide-default-party-from-standings: false
  # Número máximo de partidos no predeterminados que pueden existir en una elección activa.
  # 0 = ilimitado. Esto solo limita la creación de etiquetas de partidos completamente nuevas.
  # Los jugadores siempre pueden unirse a un partido que ya existe o dejarlo para volver al predeterminado.
  max-parties: 0
  # Si es true, los candidatos no pueden cambiar su mensaje de campaña, perfil, partido o
  # color del partido una vez que la fase de votación ha comenzado. Estos solo se pueden editar
  # durante la fase de nominación. Establecer a false para permitir ediciones en cualquier momento.
  lock-edits-during-voting: true

  # Una lista de bloqueo simple. Los mensajes de campaña que contienen alguna de estas subcadenas
  # (insensibles a mayúsculas y minúsculas) son rechazados.
  blocked-words:
    - "slur1"
    - "slur2"

# ----------------------------------------------------------------------------
#  Recompensas para el ganador - lo que recibe el candidato elegido
# ----------------------------------------------------------------------------
# Cuando una elección concluye, el ganador recibe los rangos de pueblo de Towny configurados
# y (opcionalmente) se convierte en alcalde. Los rangos deben existir en el townyperms.yml de Towny
# (los predeterminados incluyen: helper, councillor, sheriff, treasurer, etc. y los rangos personalizados
# que defines). Los rangos no válidos se omiten con una advertencia en la consola.
winner:
  # Convertir al candidato ganador en el alcalde del pueblo. Esto transfiere la alcaldía.
  set-as-mayor: true

  # Rangos de pueblo de Towny para otorgar al ganador de una *elección de pueblo*. Estos se mapean a
  # los nodos de permiso definidos en el townyperms.yml de Towny (por ejemplo, administración de parcelas).
  grant-town-ranks:
    - "assistant"

  # Si es true, los rangos otorgados por una victoria electoral previa se retiran del
  # titular saliente de la oficina cuando un nuevo ganador asume el cargo. Se aplica a los rangos de
  # pueblo para elecciones de pueblo y a los rangos de nación para elecciones de nación.
  revoke-previous-winner-ranks: false

  # Comandos adicionales de consola nativos/Bukkit para ejecutar cuando se decide un ganador.
  # Marcadores de posición: {winner} {winner_uuid} {winner_party} {party} {town} {votes} {total_votes}
  # Se ejecuta desde la consola. Ideal para LuckPerms, transmisiones, dar objetos, etc.
  # Dejar vacío para no ejecutar nada. Ejemplos (descomentar para usar):
  #   - "lp user {winner} parent addtemp mayor 30d"
  #   - "give {winner} minecraft:golden_helmet 1"
  commands-on-win: []

  # Comandos para ejecutar para cada candidato *perdedor* cuando la elección concluye.
  # Marcadores de posición: {loser} {loser_uuid} {loser_party} {party} {town} {votes}
  commands-on-loss: []

# ----------------------------------------------------------------------------
#  Personalización de comandos
# ----------------------------------------------------------------------------
# Cambia el nombre de los subcomandos de /election a lo que mejor se adapte a tu servidor.
# Las claves son nombres de acciones internas; los valores son lo que los jugadores escriben en el chat.
# Ejemplo: establecer parties: "blocs" para que /election blocs liste las posiciones de los partidos.
# Mantén cada literal único para que los comandos puedan resolverse sin ambigüedad.
commands:
  run: "run"          # registrarse como candidato
  withdraw: "withdraw"  # retirarse de la carrera
  campaign: "campaign"  # establecer tu mensaje de campaña
  profile: "profile"    # establecer tu perfil/biografía de candidato
  party: "party"        # unirse, crear, salir o renombrar un partido como admin
  parties: "parties"  # listar las posiciones actuales de los partidos
  vote: "vote"          # emitir un voto
  status: "status"      # ver el estado actual de la elección
  candidates: "candidates"  # listar candidatos
  results: "results"    # ver los resultados de la última elección concluida
  start: "start"        # (admin) iniciar una elección
  stop: "stop"          # (admin) terminar la votación temprano y contar
  cancel: "cancel"      # (admin) cancelar una elección sin ganador
  reload: "reload"      # (admin) recargar la configuración
  help: "help"
  nation: "nation"      # prefijo para apuntar a tu nación, por ejemplo /election nation vote

# ----------------------------------------------------------------------------
#  Notificaciones
# ----------------------------------------------------------------------------
notifications:
  # Transmitir el inicio/fin de la elección a todo el servidor (además de al pueblo).
  broadcast-server-wide: false
  # Recordar a los votantes que no han votado, este tiempo antes de que termine la votación.
  # Establecer a "0" para deshabilitar los recordatorios.
  voting-reminder-before-end: "6h"
  # Notificar a los residentes cuando inicien sesión si hay una elección activa en la que pueden
  # participar.
  notify-on-join: true

```
