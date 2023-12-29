---
demo:
  title: 'Demostración 2: Creación y configuración de Blob Storage'
  module: Guided Project - Azure Files and Azure Blobs
---


## Demostración: Creación y configuración de Blob Storage

En esta demostración, se explorará Blob Storage.

## Revise la configuración de Blob Storage

1. [Diapositiva auxiliar] Antes de comenzar la demostración, revise los usos y la organización de Blob Storage. ¿Cuál de nuestros grupos empresariales necesitará Blob Storage?

1. Acceda a **Azure Portal**.

1. Puede seguir usando la cuenta de almacenamiento anterior. 

1. Seleccione la pestaña **Información general**.

1. [Diapositiva auxiliar] En la sección **Blob service**, resalte la opción **Nivel de acceso predeterminado**. Explique cómo el contenido corporativo puede estar en el nivel de acceso frecuente. La información de auditoría podría estar en el nivel de acceso esporádico. Los registros o los recursos de marketing estacional podrían estar en el nivel de archivo. Más información: [Niveles de acceso para Blob Storage](https://docs.microsoft.com/azure/storage/blobs/access-tiers-overview).

1. [Diapositiva auxiliar] En la sección **Blob service**, resalte la configuración de **eliminación temporal**. Esto sería importante para el sitio web público en caso de que algo se elimine o sobrescriba accidentalmente. Los alumnos practicarán la eliminación temporal en el laboratorio. Para obtener más información, consulte [Eliminación temporal de blob](https://learn.microsoft.com/azure/storage/blobs/soft-delete-blob-overview).

1. En la sección **Blob service**, señale configuración de **control de versiones**. Esto puede ser importante para el departamento de marketing. Es posible que sea necesario realizar un seguimiento de los recursos del producto.

## Cree un contenedor de blobs, cargue un archivo y configure el acceso.

1. En la cuenta de almacenamiento, busque la hoja **Almacenamiento de datos**.

1. Seleccione **Contenedores** y, a continuación, seleccione **+ Contenedor**.

1. Proporcione un **nombre** para el contenedor:
2. **public**. Este es el almacenamiento del sitio web público.

1. Asegúrese de establecer el nivel de acceso público en **Contenedor (acceso de lectura anónimo para contenedores y blobs)**. Describa brevemente los niveles de acceso. Esto se trata con más detalle en la última demostración. 

1. Seleccione **Crear**.

1. Espere a que se implemente el contenedor y continúe trabajando en el **contenedor público**.

1. **Cargue un blob**. Como tiene tiempo, analice las opciones. 

1. Seleccione el **archivo cargado** y **copie la dirección URL**.

1. Abra una **nueva pestaña del explorador**, pegue la dirección URL y asegúrese de que se muestra el archivo cargado.

1. Vuelva al contenedor **Público** y **cambie el nivel de acceso** a **Privado (sin acceso anónimo)**.

1. **Actualice la pestaña URL** y confirme que ahora **se deniega** el acceso al recurso.

## Configure la administración del ciclo de vida.

1. [Diapositiva auxiliar] Comience con una explicación de la administración del ciclo de vida. El grupo de marketing tiene recursos de productos que es estacional. Por ejemplo, la ropa de invierno y la línea de accesorios. Este contenido se puede archivar hasta la próxima temporada. El archivado de contenido es fácil de lograr con una regla de administración del ciclo de vida. Para obtener más información, consulte [Directivas de administración del ciclo de vida de blobs](https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-overview).

1. Continúe trabajando en la cuenta de almacenamiento.

1. En la sección **Administración de datos**, seleccione **Administración del ciclo de vida**.

1. En la pestaña **Detalles**, asigne el nombre **movetoarchive** a la regla.

1. Analice el **ámbito de la regla** y cómo puede **limitar blobs con filtros**. Por ejemplo, para solo mover el contenido en el contenedor específico.

1. Vaya a la pestaña **Blobs base**.

1. Analice cómo la regla moverá automáticamente los blobs en función de la última modificación o los creados hace más de un número de días concreto.

1. Abra la lista desplegable **Entonces** y analice las opciones. Intente proporcionar ejemplos basados en nuestro escenario de laboratorio. Por ejemplo, es posible que el departamento de TI quiera que los blobs se eliminen después de 30 días porque es una cuenta de prueba.

## Configure el acceso limitado al contenido.

1. Revise los casos de uso para el acceso limitado. Por ejemplo, el contenido corporativo debe compartirse con proveedores o asociados de terceros. El acceso puede estar limitado a un período de tiempo y una acción específicos (lectura, escritura). Para obtener más información, consulte [Firmas de acceso compartido](https://learn.microsoft.com/azure/storage/common/storage-sas-overview).

1. Continúe con la **cuenta de almacenamiento**.

1. En la sección **Seguridad y redes**, seleccione **Firma de acceso compartido**.

1. Revise los **servicios permitidos** y los **tipos de recursos permitidos**. Explique que un SAS se puede limitar a una cuenta de almacenamiento, un contenedor, un archivo o un archivo de blob individual.

1. Revise los **permisos permitidos**.

1. Seleccione **Blob y contenedor** y **Lectura**.

1. Revise las configuraciones **Inicio** y **fecha y hora de expiración**.

1. Seleccione **Generar la cadena de conexión y SAS**.

1. Guarde los cambios mediante **Guardar**. 

1. Copie la **dirección URL de SAS de Blob service** en una nueva pestaña del explorador.

1. Analice cómo se muestra el contenido aunque se trate de un contenedor privado.

## Configuración de la replicación de objetos de blob 

1. [Diapositiva auxiliar] Antes de continuar con la demostración, revise los casos de uso de la replicación de objetos de blob. Por ejemplo, es necesario crear una copia de seguridad del contenido del sitio web público. Explique que las cuentas de almacenamiento pueden estar en diferentes regiones de Azure, pero eso no es necesario. Para obtener más información, consulte [Replicación de objetos](https://learn.microsoft.com/azure/storage/blobs/object-replication-overview).

1. Cree una **nueva** cuenta de almacenamiento.

1. **Cree ** un **contenedor** y una **copia de seguridad** en la cuenta de almacenamiento.

1. Vuelva a la primera cuenta de almacenamiento y al contenedor **público**. 

1. En la hoja **Administración de datos**, seleccione **Replicación de objetos**.

1. Seleccione **Crear reglas de replicación**.

    - Cuenta de almacenamiento de destino: su segunda cuenta de almacenamiento

    - Contenedor de origen: **público**

    - Contenedor de destino: **copia de seguridad**

1. **Cree** la regla. Explique que el contenedor de origen puede tardar entre 5 y 10 minutos en replicarse. Explique que los alumnos tardarán ese tiempo en el laboratorio. 

> **Nota:** Los alumnos ahora deberían poder completar LAB_02a y LAB_02b. 

  
