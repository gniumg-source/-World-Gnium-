Documentación de GitHub
Seguridad y calidad del código/Dependabot/Actualizaciones de versión del dependabot/Configuración de actualizaciones de versiones
Configuración de las actualizaciones de versiones de Dependabot
Puedes configurar tu repositorio para que el Dependabot actualice automáticamente los paquetes que utilizas.

¿Quién puede utilizar esta característica?
Users with write access

En este artículo
Acerca de las actualizaciones de versión para las dependencias
Para habilitar Dependabot version updates, comprueba un archivo de configuración dependabot.yml en el directorio .github del repositorio. El Dependabot levanta entonces las solicitudes de extracción para mantener actualizadas las dependencias que configures. Para cada dependencia del administrador de paquete que quieras actualizar, debes especificar la ubicación de los archivos de manifiesto de dicho paquete, así como la periodicidad en la que quieres buscar actualizaciones para las dependencias listadas en esos archivos. Para obtener información sobre cómo habilitar las actualizaciones de seguridad, consulta Configuración de actualizaciones de seguridad de Dependabot.

Cuando habilitas las actualizaciones de versión por primera vez, podrías tener muchas dependencias desactualizadas y algunas podrían estar varias versiones debajo de la última. Dependabot verifica las dependencias que estén desactualizadas tan pronto se habilita. Podrías ver nuevas solicitudes de extracción para las actualizaciones de versión después de algunos minutos de haber agregado el archivo de configuración, dependiendo de la cantidad de archivos de manifiesto para los cuales configuras las actualizaciones. El Dependabot también ejecutará una actualización en los cambios subsecuentes al archivo de configuración.

Para facilitar la administración y revisión de las solicitudes de incorporación de cambios, Dependabot genera un máximo de cinco solicitudes de incorporación de cambios para comenzar a actualizar a las dependencias a su versión más reciente. Si fusionas algunas de estas primeras solicitudes de cambios en la siguiente actualización programada, aquellas restantes se abrirán en la siguiente actualización, hasta ese máximo. Puede cambiar el número máximo de solicitudes de incorporación de cambios abiertas si establece la opción de configuración open-pull-requests-limit.

Para reducir aún más el número de solicitudes de cambios que puedes ver, puedes usar la opción de configuración groups para agrupar conjuntos de dependencias (por ecosistema de paquetes). Después, Dependabot genera una única solicitud de cambios para actualizar tantas dependencias como sea posible en el grupo a las versiones más recientes al mismo tiempo. Para más información, consulta Optimización de la creación de solicitudes de cambios para actualizaciones de versión de Dependabot.

A veces, debido a una configuración incorrecta o a una versión incompatible, es posible que veas un error en la ejecución de Dependabot. Al cabo de 15 errores de ejecución, Dependabot version updates omitirá las ejecuciones programadas posteriores hasta que desencadenes manualmente una comprobación de actualizaciones desde el gráfico de dependencia. Las Dependabot security updates se seguirán ejecutando de la forma habitual.

De forma predeterminada, Dependabot version updates solo mantiene actualizadas las dependencias directas que se han definido explícitamente en un manifiesto. Puedes decidir recibir actualizaciones de dependencias indirectas definidas en archivos de bloqueo. Para más información, consulta Control de qué dependencias actualiza Dependabot.

Cuando ejecutas actualizaciones de versión o de seguridad, algunos ecosistemas deberán poder resolver todas las dependencias de su fuente para verificar que las actualizaciones sean exitosas. Si tus archivos de manifiesto o de bloqueo contienen cualquier dependencia privada, el Dependabot deberá poder acceder a la ubicación en la que se hospedan dichas dependencias. Los propietarios de las organizaciones pueden otorgar acceso al Dependabot para los repositorios privados que contengan dependencias para un proyecto dentro de la misma organización. Para más información, consulta Administrar la configuración de seguridad y análisis de su organización. Puede configurar el acceso a los registros privados en el archivo de configuración dependabot.yml de un repositorio. Para más información, consulta Configuración del acceso a registros privados para Dependabot. Adicionalmente, el Dependabot no es compatible con dependencias privadas de GitHub para todos los administradores de paquetes. Para más información, consulta Ecosistemas y repositorios admitidos por Dependabot y Compatibilidad de lenguajes de GitHub.

Habilitar las Dependabot version updates
Dependabot version updates se habilita mediante la confirmación de un archivo de configuración dependabot.yml en el repositorio. Si habilitas la característica en la página de configuración, GitHub crea un archivo básico que puedes editar; de lo contrario, puedes crear el archivo mediante cualquier editor de archivos.

En GitHub, navegue hasta la página principal del repositorio.

Debajo del nombre del repositorio, haz clic en  Settings. Si no puedes ver la pestaña "Configuración", selecciona el menú desplegable  y, a continuación, haz clic en Configuración.

Captura de pantalla de un encabezado de repositorio en el que se muestran las pestañas. La pestaña "Configuración" está resaltada con un contorno naranja oscuro.
En la sección "Security" de la barra lateral, haz clic en  Advanced Security.

En "Dependabot", a la derecha de"Dependabot version updates", haz clic en Enable para abrir un archivo de configuración dependabot.yml básico en el directorio .github del repositorio. For information about the options you can use to customize how Dependabot maintains your repositories, see Referencia de opciones de Dependabot.

YAML
# To get started with Dependabot version updates, you'll need to specify which
# package ecosystems to update and where the package manifests are located.

version: 2
updates:
- package-ecosystem: "" # See documentation for possible values
  directory: "/" # Location of package manifests
  schedule:
    interval: "weekly"
Agrega un version. Esta clave es necesaria. El archivo debe comenzar por version: 2.

Opcionalmente, si tienes dependencias en un registro privado, agrega una sección registries que contenga los detalles de autenticación. Para más información, consulta Configuración del acceso a registros privados para Dependabot.

Agrega una sección updates con una entrada para cada administrador de paquetes que quieras que monitoree el Dependabot. Esta clave es necesaria. La utilizas para configurar la forma en que el Dependabot actualiza las versiones o las dependencias de tu proyecto. Cada entrada configura los ajustes de actualización para un administrador de paquetes en particular. Para más información, consulta Acerca del archivo dependabot.yml en la "referencia de opciones de Dependabot".

Para cada administrador de paquete, utiliza:

package-ecosystem para especificar el administrador de paquetes. Para más información sobre los administradores de paquetes admitidos, consulta package-ecosystem.
directories o directory para especificar la ubicación de varios archivos de manifiesto o definición. Para más información, consulta Definición de varias ubicaciones para archivos de manifiesto.
schedule.interval para especificar la frecuencia con la que se comprueban las nuevas versiones.
Compruebe el archivo de configuración dependabot.yml en el directorio .github del repositorio.

Archivo dependabot.yml de ejemplo
En el siguiente archivo dependabot.yml de ejemplo se configuran actualizaciones de versión para tres administradores de paquetes: npm, Docker y GitHub Actions. Cuando se registra este archivo, el Dependabot revisa los archivos de manifiesto en la rama predeterminada par ver si hay dependencias desactualizadas. Si encuentra dependencias desactualizadas, levantará solicitudes de extracción contra la rama predeterminada para actualizar estas dependencias.

YAML
# Basic `dependabot.yml` file with
# minimum configuration for three package managers

version: 2
updates:
  # Enable version updates for npm
  - package-ecosystem: "npm"
    # Look for `package.json` and `lock` files in the `root` directory
    directory: "/"
    # Check the npm registry for updates every day (weekdays)
    schedule:
      interval: "daily"

  # Enable version updates for Docker
  - package-ecosystem: "docker"
    # Look for a `Dockerfile` in the `root` directory
    directory: "/"
    # Check for updates once a week
    schedule:
      interval: "weekly"

  # Enable version updates for GitHub Actions
  - package-ecosystem: "github-actions"
    # Workflow files stored in the default location of `.github/workflows`
    # You don't need to specify `/.github/workflows` for `directory`. You can use `directory: "/"`.
    directory: "/"
    schedule:
      interval: "weekly"
En el ejemplo anterior, si las dependencias de Docker estuvieran muy desactualizadas, tal vez quisieras comenzar con una programación de tipo daily hasta que las dependencias estén bien actualizadas y, posteriormente, tomar una programación semanal.

Habilitar las actualizaciones de versión en las bifurcaciones
Si quieres habilitar las actualizaciones de versión en las bifurcaciones, hay un paso extra que debes tomar. Las actualizaciones de versión no se habilitan automáticamente en las bifurcaciones cuando existe un archivo de configuración dependabot.yml. Esto garantiza que los dueños de la bifurcación no habiliten las actualizaciones de versión accidentalmente cuando suben cambios, incluyendo el archivo de configuración dependabot.yml del repositorio original.

En una bifurcación, también necesitas habilitar explícitamente el Dependabot.

En GitHub, navegue hasta la página principal del repositorio.

Debajo del nombre del repositorio, haz clic en  Settings. Si no puedes ver la pestaña "Configuración", selecciona el menú desplegable  y, a continuación, haz clic en Configuración.

Captura de pantalla de un encabezado de repositorio en el que se muestran las pestañas. La pestaña "Configuración" está resaltada con un contorno naranja oscuro.
En la sección "Security" de la barra lateral, haz clic en  Advanced Security.

En "Dependabot, a la derecha de "Dependabot version updates", haz clic en Enable para permitir que Dependabot inicie actualizaciones de versión.

Revisar el estado de las actualizaciones de versión
Después de habilitar las actualizaciones de versión, se rellena la pestaña Dependabot del gráfico de dependencias del repositorio. En esta pestaña se muestra qué administradores de paquetes Dependabot están configurados para supervisar y cuándo los datos Dependabot comprueban por última vez las nuevas versiones.

Captura de pantalla de la página Gráfico de dependencias. La pestaña con el nombre "Dependabot", está resaltada con un contorno naranja.

Para más información, consulta Listar dependencias configuradas para las actualizaciones de versión.

Inhabilitar las Dependabot version updates
Puedes inhabilitar las actualizaciones de versión completamente si eliminas el archivo dependabot.yml de tu repositorio. Normalmente, tal vez quieras inhabilitar las actualizaciones temporalmente para una o más dependencias o administradores de paquete.

Administradores de paquetes: deshabilítalo estableciendo open-pull-requests-limit: 0 o comentando el package-ecosystem correspondiente en el archivo de configuración.
Dependencias específicas: deshabilítalas agregando los atributos ignore para los paquetes o aplicaciones que quieras excluir de las actualizaciones.
Cuando inhabilitas las dependencias, puedes utilizar comodines para empatar con un conjunto de bibliotecas relacionadas. También puedes especificar qué versiones excluir. Esto es particularmente útil si necesitas bloquear actualizaciones en una biblioteca, el trabajo pendiente para apoyar un cambio sustancial en su API, pero quieres quieres obtener cualquier arreglo de seguridad para la versión que utilices.

Ejemplo de inhabilitar las actualizaciones de versión para algunas dependencias
En este archivo dependabot.yml de ejemplo se incluyen ejemplos de las formas diferentes para inhabilitar las actualizaciones en algunas dependencias, mientras que se permite que otras actualizaciones continuen.

# `dependabot.yml` file with updates
# disabled for Docker and limited for npm

version: 2
updates:
  # Configuration for Dockerfile
  - package-ecosystem: "docker"
    directory: "/"
    schedule:
      interval: "weekly"
      # Disable all pull requests for Docker dependencies
    open-pull-requests-limit: 0

  # Configuration for npm
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
    ignore:
      # Ignore updates to packages that start with 'aws'
      # Wildcards match zero or more arbitrary characters
      - dependency-name: "aws*"
      # Ignore some updates to the 'express' package
      - dependency-name: "express"
        # Ignore only new versions for 4.x and 5.x
        versions: ["4.x", "5.x"]
      # For all packages, ignore all patch updates
      - dependency-name: "*"
        update-types: ["version-update:semver-patch"]
Para más información sobre cómo comprobar las preferencias de omisión existentes, consulta Referencia de opciones de Dependabot.
