---
lab:
  title: 'Ejercicio 3: Proporcionar almacenamiento de archivos compartidos para las oficinas de la empresa'
  module: Guided Project - Azure Files and Azure Blobs
---


La empresa está dispersa geográficamente con oficinas en diferentes ubicaciones.  Estas oficinas necesitan una forma de compartir archivos y de difundir información. Por ejemplo, el departamento financiero necesita confirmar la información de los costes de auditoría y cumplimiento. Estos recursos compartidos de archivos deben ser fáciles de acceder y cargar sin demora. Solo se debe tener acceso a algunos contenidos desde redes virtuales corporativas determinadas.


## Diagrama de la arquitectura

![Diagrama con una cuenta de almacenamiento, un recurso compartido de archivos y un directorio.](../Media/task-4.png)

## Tareas de aptitudes
- Cree una cuenta de almacenamiento específicamente para recursos compartidos de archivos. 
- Configure un recurso compartido de archivos y un directorio.  
- Configure instantáneas y practique la restauración de archivos. 
- Restrinja el acceso a una red virtual y una subred específicas. 

## Instrucciones del ejercicio

>**Nota**: Para completar este laboratorio, necesitará una [suscripción de Azure](https://azure.microsoft.com/free/).

## Cree y configure una cuenta de almacenamiento en Azure Files. 

1. Cree una cuenta de almacenamiento para los archivos compartidos del departamento financiero.  Obtenga más información sobre las cuentas de almacenamiento para [implementaciones de Azure Files](https://learn.microsoft.com/azure/storage/files/storage-files-planning#management-concepts)

    - En el portal, busque y seleccione `Storage accounts`.
    - Seleccione **+ Create** (+ Crear).
    - Para **Grupo de recursos**, seleccione **Crear nuevo**. Asigne un **nombre** al grupo de recursos y seleccione **Aceptar** para guardar los cambios. 
    - Proporcione el **nombre de la cuenta de almacenamiento**. Asegúrese de que el nombre cumple los requisitos de nomenclatura. 
    - Establezca **Rendimiento** en **Premium**.
    - Establezca el **tipo de cuenta Premium** en **Recursos compartidos de archivos**.
    - Establezca la **Redundancia** en **Almacenamiento con redundancia de zona**.
    - Seleccione **Revisar** y, a continuación, **cree** la cuenta de almacenamiento.
    - Espere a que se implemente el recurso.
    - Haga clic en **Go to resource** (Ir al recurso). 

## Cree y configure un recurso compartido de archivos y con un directorio.

1. Cree un recurso compartido de archivos para la oficina corporativa. Obtenga más información sobre los [niveles de Azure File](https://learn.microsoft.com/azure/storage/files/storage-files-planning#storage-tiers).

    - En la cuenta de almacenamiento, en la sección **Almacenamiento de datos**, seleccione la hoja **Recursos compartidos de archivos**. 
    - Haga clic en **+ Recurso compartido de archivos** y proporcione un **Nombre**.
    - Revise las otras opciones, pero tome los valores predeterminados.
    - Seleccione **Crear**

1. Agregue un directorio al recurso compartido de archivos del departamento de finanzas. Para futuras pruebas, cargue un archivo. 

    - Seleccione el recurso compartido de archivos y haga clic en **+ Agregar directorio**. 
    - Asigne el nombre `finance` al directorio nuevo.
    - Seleccione **Examinar** y, después, seleccione el directorio **finance**.
    - Observe que puede **agregar directorios** para organizar aún más el recurso compartido de archivos.
    - **Cargue** un archivo de su elección. 

## Configure y pruebe las instantáneas.

1. De forma similar al almacenamiento de blobs, debe protegerse frente a la eliminación accidental de archivos. Decide usar instantáneas. Obtenga más información sobre las [instantáneas de archivos](https://learn.microsoft.com/azure/storage/files/storage-snapshots-files).
    
    - Seleccione su recurso compartido de archivos.
    - En la sección **Operaciones**, seleccione la hoja **Instantáneas**. 
    - Seleccione **+ Agregar instantánea**. El comentario es opcional. Seleccione **Aceptar**.
    - Seleccione la instantánea y compruebe que se incluyen el directorio de archivos y el archivo cargado.
  
1. Practique el uso de instantáneas para restaurar un archivo.
    - Vuelva al **recurso compartido de archivos**.
    - **Vaya** al directorio de archivos. 
    - Seleccione el archivo cargado y, en el panel **Propiedades**, haga clic en **Eliminar**. Seleccione **Sí** para confirmar la eliminación. 
    - Seleccione la hoja **Instantánea** y, a continuación, haga clic en la instantánea. 
    - Vaya al archivo que quiera restaurar.
    - Seleccione el archivo y, a continuación, seleccione **Restaurar**.
    - Proporcione un **nombre de archivo restaurado**. 
    - Compruebe que el directorio de archivos tiene el archivo restaurado.  

## Configure la restricción del acceso de almacenamiento a las redes virtuales seleccionadas.

1. Las tareas de esta sección requieren una red virtual con subred. En un entorno de producción, estos recursos ya estarían creados.
    - Busque y seleccione **Redes virtuales**.
        - Seleccione **Crear**. Seleccione el grupo de recursos. y asigne un **nombre** a la red virtual.
        - Tome los valores predeterminados para otros parámetros, seleccione **Revisar y crear** y, a continuación, **Crear**.
        - Espere a que se implemente el recurso.
        - Haga clic en **Go to resource** (Ir al recurso). 
    - En la sección **Configuración**, seleccione la hoja **Subredes**.
        - Seleccione la subred **default**.
        - En la sección **Puntos de conexión de servicio**, en la lista desplegable **Servicios**, seleccione **Microsoft.Storage**.
        - No realice ningún cambio.    
        - Asegúrese de **Guardar** los cambios. 
   
1. Solo se debe tener acceso a la cuenta de almacenamiento desde la red virtual que acaba de crear. Obtenga más información sobre el uso de [puntos de conexión de almacenamiento privados](https://learn.microsoft.com/azure/storage/common/storage-private-endpoints).

    - Vuelva a la **cuenta de almacenamiento de archivos**. 
    - En la sección **Seguridad y redes**, seleccione la hoja **Redes**.
        - Cambie el **Acceso de red pública** a **Habilitado desde redes virtuales y direcciones IP seleccionadas**.
        - En la sección **Redes virtuales**, seleccione **Agregar red virtual existente**.
        - Seleccione la red virtual y la subred y, después, seleccione **Agregar**.
        - Asegúrese de **Guardar** los cambios. 
    - Seleccione el **Navegador de almacenamiento** y vaya al recurso compartido de archivos. 
    - Compruebe el mensaje *no está autorizado para realizar esta operación*. No se está conectando desde la red virtual. 


>**Nota**: Para practicar más, complete el módulo [Configuración de la seguridad de Azure Storage](https://learn.microsoft.com/training/modules/configure-storage-security/). El módulo tiene una simulación de laboratorio interactiva en la que puede practicar la creación de almacenamiento seguro. 

## Ampliar el aprendizaje con Copilot

Copilot puede ayudarte en tu recorrido de aprendizaje. Copilot puede proporcionar información técnica básica, pasos de alto nivel, ventajas y desventajas, ayuda para solucionar problemas, casos de uso, ejemplos de codificación y mucho más. Para acceder a Copilot, abre un explorador Edge y elige Copilot (arriba a la derecha). Dedique unos minutos a probar estas indicaciones.
+ ¿Qué es Azure File Storage y en qué se diferencia de Azure Blob Storage? ¿Cómo se decide cuál usar?
+ ¿Cuáles son las distintas formas de proteger el contenido de los archivos de Azure?

## Más información con el aprendizaje autodirigido

+ [Configurar Azure Files y Azure File Sync](https://learn.microsoft.com/en-us/training/modules/configure-azure-files-file-sync/). En este módulo, aprenderás a configurar recursos compartidos de archivos de Azure e instantáneas de recursos compartidos de archivos.

## Puntos clave

Enhorabuena por completar el laboratorio. Estas son las principales conclusiones del laboratorio. 
+ Azure Files le ofrece recursos compartidos de archivos en la nube totalmente administrados, a los que se puede obtener acceso mediante el protocolo Bloque de mensajes del servidor (SMB) estándar, el protocolo Network File System (NFS) y la API de REST de Azure Files.
+ Azure Files proporciona la capacidad de tomar instantáneas de recursos compartidos de SMB y NFS. Las instantáneas de recursos compartidos capturan el estado del recurso compartido en ese momento dado. Las instantáneas de recurso compartido solo proporcionan protección a nivel de archivo.
+ Puedes configurar un punto de conexión de cuenta de almacenamiento para acceder directamente al recurso compartido de archivos de Azure. Puntos de conexión para restringir el acceso de red a tu cuenta de almacenamiento.

