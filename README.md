#1. Conectar GitHub con Cloud Build
- Entrar a "Cloud Build" en GCP
- Entrar al apartado de "Repositorios"
- Entrar a "+ Crear conexión de Host"
- Configurar la conexión, asignando una región "Iowa" en este caso y asignarle un nombre para referirte a esta conexión
- Aceptar los permisos de conexión a GitHub
- Seleccionar una instalación de un perfil existente o configurar uno nuevo
- Una vez conectada te aparecerá la información desde "Repositorios" en "Cloud Build"
- Seleccionar "Vincular repositorio"
- Configurar la vinculación con la conexión que se acaba de crear y seleccionar el repositorio correspondiente

#2. Crear el archivo de configuración cloudbuild.yaml
- Añadir el archivo cloudbuild. yaml a la raiz del proyecto/repositorio y añadir las configuraciones
- ID proyecto: project-98b200ea-2317-4845-843
- Nombre Artifact: java-repo
- Nombre proyecto: java-hello-world
- Este archivo: Construye la imagen Docker, sube la imagen a Artifact Registry, despliega automáticamente en Cloud Run y la variable $COMMIT_SHA asegura que cada build tenga una imagen única.

#3. Crear el trigger en Cloud Build
- Ir a "Cloud Build"
- Entrar en al apartado de "Activadores"
- Entrar a "Crear activador"
- Configurar un nombre cualquiera, la región del proyecto (Iowa en este caso)
- Eveto -> Enviar a una rama
- Fuente -> Repositorios de Cloud Build
- Seleccionar el repositorio y la rama
- Configuración -> Archivo de configuración de Cloud Build (YAML o JSON)
- Ubicación -> Repositorio -> / cloudbuild.yaml
- Cuenta de servicio (seleccionar la que corresponda al proyecto)
- Ejecutar el activador (desde la sección de "Historial" aparecen todas las versiones de ejecución)
- Una vez este todo correcto en el activador se puede ir a "Cloud Run" y ahi aparecerá el contenedor correspondiente y la url para acceder a el.

En caso de tener problemas con el activador por temas de permisos 
- Entrar a "IAM" desde el buscador de GCP
- Entrar a "Cuentas de servicio"
- Seleccionar la cuenta que hayas seleccionado al crear el activador
- Dirigirse a la sección de "Permisos"
- Ingresar a "Administar acceso"
- Asignar los roles: Administrador de Cloud Run, Editor, Escritor de Artifact Registry, Escritor de registros, Invocador de Cloud Run, Receptor de Eventos de Eventarc y Usuario de cuenta de servicio
- Guardar y volver a ejecutar el activador
