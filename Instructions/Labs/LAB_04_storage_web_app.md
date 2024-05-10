---
lab:
  title: 'Ejercicio 4: Proporcionar almacenamiento para una nueva aplicación de empresa.'
  module: Guided Project - Azure Files and Azure Blobs
---
La empresa está diseñando y desarrollando una nueva aplicación. Los desarrolladores deben asegurarse de que solo se tiene acceso al almacenamiento mediante claves e identidades administradas. Los desarrolladores quieren usar el control de acceso basado en roles. Para ayudar con las pruebas, se necesita almacenamiento inmutable protegido. 

## Diagrama de la arquitectura

![Diagrama con una cuenta de almacenamiento, identidades administradas y un almacén de claves.](../Media/task-5.png)

## Tareas de aptitudes

- Cree una cuenta de almacenamiento y una identidad administrada.
- Proteja el acceso a la cuenta de almacenamiento con un almacén de claves y una clave.
- Configure el cifrado de la cuenta de almacenamiento para usar claves administradas por el cliente en el almacén de claves.
- Configure una directiva de retención basada en el tiempo y un ámbito de cifrado.

## Instrucciones del ejercicio

## Cree una cuenta de almacenamiento y una identidad administrada.

1. Proporcione una cuenta de almacenamiento para la aplicación web. 
    - En el portal, busque y seleccione **Cuentas de almacenamiento**. 
    - Seleccione **+ Create** (+ Crear).
    - Para **Grupo de recursos**, seleccione **Crear nuevo**. Asigne un **nombre** al grupo de recursos y seleccione **Aceptar** para guardar los cambios.
    - Proporcione el **nombre de la cuenta de almacenamiento**. El nombre debe ser único y cumplir con los requisitos de nomenclatura.
    - Vaya a la pestaña **Cifrado**.
    - Active la casilla de **Habilitar cifrado de infraestructura**.
    - Observe la advertencia, *Esta opción no se puede cambiar después de crear esta cuenta de almacenamiento.*
    - Seleccione **Revisar + crear**.
    - Espere a que se implemente el recurso.

1. Habilite una identidad de servicio administrada para la aplicación web.  Más información [sobre las identidades administradas](https://learn.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).

    - Busque y seleccione **Identidades administradas**.
    - Seleccione **Crear**.
        - Seleccione el **grupo de recursos**. 
        - Asigne un nombre a la identidad administrada.
    - Seleccione **Revisar y crear** y, a continuación, **Crear**. 

1. Asigne los permisos correctos a la identidad administrada. La identidad solo necesita leer y enumerar contenedores y blobs. Obtenga más información sobre [cómo asignar roles de Azure](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-portal).
    
    - Busque y seleccione su **cuenta de almacenamiento**.
    - Seleccione la hoja **Control de acceso (IAM)**.
    - En el centro de la página, seleccione **Agregar asignación de roles**.
    - En la página **Roles de funciones de trabajo**, busque y seleccione el rol **Lector de datos de Blob Storage**. 
    - En la página **Miembros**, seleccione **Identidad administrada**.
    - Seleccione **Seleccionar miembros** y, en la lista desplegable **Identidad administrada**, seleccione **Identidad administrada asignada por el usuario**.
    - Seleccione la identidad administrada que creó en el paso anterior. 
    - Haga clic en **Seleccionar** y, a continuación, **en Revisar y asignar** el rol. 
    - Seleccione **Revisar y asignar** una segunda vez para agregar la asignación de roles.
    - Ahora se puede acceder a la cuenta de almacenamiento mediante una identidad administrada con los permisos Lector de datos de Blob Storage. 

## Protección del acceso a la cuenta de almacenamiento con un almacén de claves y una clave

1. Para crear el almacén de claves y la clave necesarios para esta parte del laboratorio, la cuenta de usuario debe tener permisos de Administrador del almacén de claves. Obtenga más información sobre cómo [proporcionar acceso a las claves, certificados y secretos del almacén de claves con un control de acceso basado en roles](https://learn.microsoft.com/azure/key-vault/general/rbac-guide?tabs=azure-cli).
    - En el portal, busque y seleccione **Grupos de recursos**. 
    - Seleccione el **grupo de recursos**, y luego seleccione la hoja **Control de acceso (IAM)**.
    - En el centro de la página, seleccione **Agregar asignación de roles**.
    - En la página **Roles de función del trabajo**, busque y seleccione el rol **Administrador de almacén de claves**.
    - En la página **Miembros**, seleccione **Usuario, grupo o entidad de servicio**.
    - Seleccione **Seleccionar miembros**.
    - Busque su cuenta de usuario y selecciónela. En la esquina superior derecha del portal, aparece su cuenta de usuario.
    - Haga clic en **Seleccionar** y, a continuación, en **Revisar y asignar**.
    - Seleccione **Revisar y asignar** una segunda vez para agregar la asignación de roles.
    - Ya puede continuar con el laboratorio.

1. Cree un almacén de claves para almacenar las claves de acceso. 

    - En el portal, busque y seleccione **Almacenes de claves**.
    - Seleccione **Crear**.
    - Seleccione el **grupo de recursos**.
    - Proporcione el **nombre** del almacén de claves. El nombre debe ser único.
    - Asegúrese de que en la pestaña **Configuración de acceso** está seleccionado el **control de acceso basado en rol (recomendado) de Azure**. 
    - Seleccione **Revisar + crear**.
    - Espere hasta que se complete la validación y seleccione **Crear**.
    - Una vez que la implementación se haya completado, seleccione **Ir al recurso**.
    - En la hoja **Información general**, asegúrese de que la protección contra la **eliminación temporal** y **purga** están **habilitadas**. 

1. Cree una clave administrada por el cliente en el almacén de claves. 

    - En el **almacén de claves**, en la sección **Objetos**, seleccione la hoja **Claves**.
    - Haga clic en **Generar/importar** y asigne un **Nombre** a la clave.
    - Tome los valores predeterminados para el resto de los parámetros y **Cree** la clave.

## Configure el cifrado de la cuenta de almacenamiento para usar claves administradas por el cliente en el almacén de claves.

1. Para poder completar los pasos siguientes, debe asignar el rol de usuario de cifrado del servicio criptográfico de Key Vault a la identidad administrada. Obtenga más información sobre cómo [usar una identidad administrada asignada por el sistema para autorizar el acceso](https://learn.microsoft.com/azure/storage/common/customer-managed-keys-configure-existing-account?tabs=azure-portal#use-a-system-assigned-managed-identity-to-authorize-access)
    - En el portal, busque y seleccione **Grupos de recursos**. 
    - Seleccione el **grupo de recursos**, y luego seleccione la hoja **Control de acceso (IAM)**.
    - En el centro de la página, seleccione **Agregar asignación de roles**.
    - En la página **Roles de funciones de trabajo**, busque y seleccione el rol **Usuario de cifrado del servicio criptográfico de Key Vault**.
    - En la página **Miembros**, seleccione **Identidad administrada**.
    - Seleccione **Seleccionar miembros** y, en la lista desplegable **Identidad administrada**, seleccione **Identidad administrada asignada por el usuario**.
    - Seleccione su identidad administrada.  
    - Haga clic en **Seleccionar** y, a continuación, en **Revisar y asignar**.
    - Seleccione **Revisar y asignar** una segunda vez para agregar la asignación de roles.
    
1. Configure la cuenta de almacenamiento para usar claves administradas por el cliente en su almacén de claves. Obtenga más información sobre las [claves administradas por el cliente en una cuenta de almacenamiento existente](https://learn.microsoft.com/azure/storage/common/customer-managed-keys-configure-existing-account?WT.mc_id=Portal-Microsoft_Azure_Storage&tabs=azure-portal)
    - Vuelva a la cuenta de almacenamiento.
    - En la sección **Seguridad y redes**, seleccione la hoja **Cifrado**.
    - Seleccione **Claves administradas por el cliente**.
    - **Seleccione un almacén de claves y una clave**. Seleccione su almacén de claves y la clave.
    - Para confirmar su elección, use **Seleccionar**. 
    - Asegúrese de que el **Tipo de identidad** es **Asignado por el usuario**.
    - **Seleccione una identidad**
    - Seleccione la identidad administrada y, a continuación, seleccione **Agregar**. 
    - Guarde los cambios mediante **Guardar**.
    - Si recibe un error que indica que la identidad no tiene los permisos correctos, espere un minuto e inténtelo de nuevo. 

## Configure una directiva de retención basada en el tiempo y un ámbito de cifrado.

1. Los desarrolladores requieren un contenedor de almacenamiento donde el administrador no puede modificar los archivos. Obtenga más información sobre el [almacenamiento inmutable de blobs](https://learn.microsoft.com/azure/storage/blobs/immutable-storage-overview)

    - Vaya a su **cuenta de almacenamiento**.
    - En la sección **Almacenamiento de datos**, seleccione la hoja **Contenedores**. 
    - Cree un contenedor denominado **hold**. Use los valores predeterminados. Asegúrese de **crear** el contenedor. 
    - Cargue un archivo en el contenedor. 
    - En la sección **Configuración**, seleccione la hoja **Directiva de acceso**. 
    - En la sección **Blob Storage inmutable**, seleccione **+ Agregar directiva**. 
    - En **Tipo de directiva**, seleccione **Retención basada en tiempo**. 
    - Establezca el **Período de retención** en **5 días**. 
    - Asegúrese de **Guardar** los cambios. 
    - Intente **eliminar** el archivo en el contenedor. 
    - Compruebe que no se **pudo eliminar blobs** debido a la directiva.  

1. Los desarrolladores requieren un ámbito de cifrado que permita el cifrado de infraestructura. Obtenga más información sobre el [cifrado de infraestructura](https://learn.microsoft.com/azure/storage/common/infrastructure-encryption-enable?tabs=portal).

    - Vuelva a la cuenta de almacenamiento. 
    - En la hoja **Seguridad y redes**, seleccione **Cifrado**.
    - En la pestaña **Ámbitos de cifrado**, seleccione **Agregar**.
    - Asigne un **nombre** al ámbito de cifrado. 
    - El **tipo de cifrado** es **clave administrada por Microsoft**.
    - Establezca el **cifrado de infraestructura** en **Habilitar**.
    - **Cree** el ámbito de cifrado
    - Vaya su cuenta de almacenamiento y cree un nuevo contenedor.
    - Observe que en la página **Nuevo contenedor**, aparece el **Nombre** y el **nivel de acceso Público**.
    - Observe que en la sección **Avanzado** puede seleccionar el **ámbito de cifrado** que creó y aplicarlo a todos los blobs del contenedor. 


>**Nota**: Para practicar más, complete el módulo [Protección y aislamiento del acceso a recursos de Azure mediante grupos de seguridad de red y puntos de conexión de servicio](https://learn.microsoft.com/training/modules/secure-and-isolate-with-nsg-and-service-endpoints/). El módulo tiene un espacio aislado donde podrá practicar más al restringir el acceso al almacenamiento.
