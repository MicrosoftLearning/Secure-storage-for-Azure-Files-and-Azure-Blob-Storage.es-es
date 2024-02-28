---
lab:
  title: 'Ejercicio 02b: Proporcionar almacenamiento privado para documentos internos de la empresa'
  module: Guided Project - Azure Files and Azure Blobs
---


La empresa necesita almacenamiento para sus oficinas y departamentos. Este contenido es privado para la empresa y no debe compartirse sin consentimiento. Este almacenamiento requiere alta disponibilidad si hay una interrupción regional. La empresa quiere usar este almacenamiento para hacer una copia de seguridad del almacenamiento del sitio web público. 

## Diagrama de la arquitectura

![Diagrama con una cuenta de almacenamiento y dos contenedores de blobs.](../Media/task-3.png)

## Tareas de aptitudes
- Cree una cuenta de almacenamiento para los documentos privados de la empresa.
- Configure la redundancia de la cuenta de almacenamiento. 
- Configure una firma de acceso compartido para que los asociados tengan acceso restringido a un archivo. 
- Realice una copia de seguridad del almacenamiento del sitio web público.
- Implemente la administración del ciclo de vida para mover el contenido al nivel de acceso esporádico.

## Instrucciones del ejercicio

> **Nota**: Estas instrucciones requieren que haya completado **Lab 02a**: Proporcionar almacenamiento para documentos internos.

## Cree una cuenta de almacenamiento y configure una alta disponibilidad.

1. Cree una cuenta de almacenamiento para los documentos internos privados de la empresa.
    - En el portal, busque y seleccione **Cuentas de almacenamiento**.  
    - Seleccione **+ Create** (+ Crear). 
    - Seleccione el **grupo de recursos** que ha creado en el laboratorio anterior.   
    - Establezca el **Nombre principal de la cuenta de almacenamiento** en `private`. Agregue un identificador al nombre para asegurarse de que el nombre es único. 
    - Seleccione **Revisar** y, después, **cree** la cuenta de almacenamiento. 
    - Espere a que se implemente la cuenta de almacenamiento y, después, seleccione **Ir al recurso**.

1. Este almacenamiento requiere alta disponibilidad si hay una interrupción regional. Sin embargo, no se requiere acceso de lectura en una región secundaria. Configure el nivel de **redundancia** adecuado. 

    - En el panel Cuenta de almacenamiento, en la sección **Administración de datos**, seleccione la hoja **Redundancia**. 
    - Asegúrese de que el **almacenamiento con redundancia geográfica (GRS)** está seleccionado.
    - **Actualice** la página. 
    - Revise la información de ubicación principal y secundaria. 
    - Guarde los cambios mediante **Guardar**.

## Cree un contenedor almacenamiento, cargue un archivo y restrinja el acceso al archivo. 

1. Cree un contenedor de almacenamiento privado para los datos corporativos. 

    - En la cuenta de almacenamiento, en la sección **Almacenamiento de datos**, seleccione la hoja **Contenedores**. 
    - Seleccione **+ Contenedor**. 
    - Asegúrese de que el **Nombre** del contenedor es `private`.
    - Asegúrese de que el **Nivel de acceso público** sea **Privado (sin acceso anónimo)**.
    - Como tiene tiempo, revise la **configuración avanzada**, pero con los valores predeterminados. 
    - Seleccione **Crear**. 

1.  Para realizar pruebas, cargue un archivo en el contenedor **privado**. El tipo de archivo es indiferente. Una pequeña imagen o archivo de texto es una buena opción. Realice pruebas para asegurarse de que no es accesible de forma pública. 

    - Seleccione el contenedor.
    - Seleccione **Cargar**.
    - **Vaya a los archivos** y seleccione un archivo.
    - **Cargue** el archivo.
    - Seleccione el archivo cargado.
    - En la pestaña **Información general**, copie la **dirección URL**.
    - Pegue la **dirección URL** en una pestaña nueva del explorador. 
    - Compruebe que el archivo no se muestra y recibe un error. 

1. Un socio externo requiere acceso de lectura y escritura al archivo durante al menos las próximas 24 horas. Configure y pruebe una firma de acceso compartido (SAS). Más información acerca de las [firmas de acceso compartido](https://learn.microsoft.com/azure/storage/common/storage-sas-overview).

    - Seleccione el archivo blob cargado y vaya a la pestaña **Generar SAS**. 
    - En la lista desplegable **Permisos**, asegúrese de que el asociado solo tiene permisos de **lectura**.
    - Compruebe que la **Fecha y hora de inicio y expiración** es para las próximas 24 horas. 
    - Seleccione **Generar token SAS y URL**.
    - Copie la **dirección URL de SAS del blob** en una nueva pestaña del explorador.
    - Compruebe que puede acceder al archivo. Si ha cargado un archivo de imagen, se mostrará en el explorador. Se descargarán otros tipos de archivo.

## Configure los niveles de acceso de almacenamiento y la replicación de contenido.

1. Para ahorrar costes, después de 30 días, mueva los blobs del nivel de acceso frecuente al nivel de acceso esporádico. Para obtener más información, consulte [Ciclo de vida de Azure Blob Storage](https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-policy-configure?tabs=azure-portal).

    - Vuelva a la **cuenta de almacenamiento**.
    - En la sección **Información general**, observe que el **nivel de acceso predeterminado** está establecido en **Frecuente**. 
    - En la sección **Administración de datos**, seleccione la hoja **Administración del ciclo de vida**.
    - Seleccione **Agregar regla**. 
    - Asigne el nombre `movetocool` en **Nombre de la regla**.
    - Establezca el **Ámbito de la regla** en **Aplicar regla a todos los blobs de la cuenta de almacenamiento**.
    - Seleccione **Siguiente**.
    - Asegúrese de que **Última modificación** está seleccionada.
    - Establezca **Más de (días atrás)** en **30**.
    - En la lista desplegable **Después**, seleccione **Mover al almacenamiento de acceso esporádico**.
    - Como tiene tiempo, revise otras opciones de ciclo de vida en la lista desplegable. 
    - **Agregue** la regla.
  
1. Es necesario hacer una copia de seguridad de los archivos del sitio web público en otra cuenta de almacenamiento. [Más información sobre la [replicación de objetos](https://learn.microsoft.com/azure/storage/blobs/object-replication-configure?tabs=portal)].

    - En su cuenta de almacenamiento, **cree** un nuevo contenedor llamado `backup`. Use los valores predeterminados. Consulte Lab 02a si necesita instrucciones detalladas. 
    - Vaya a la cuenta de almacenamiento **publicwebsite**. Esta cuenta de almacenamiento se creó en el ejercicio anterior. 
        - En la sección **Administración de datos**, seleccione la hoja **Replicación de objetos**. 
        - Seleccione **Crear reglas de replicación**.
        - Establezca **Cuenta de almacenamiento de destino** en la cuenta de almacenamiento **privada**.
        - Establezca el **Contenedor de origen** en **público** y el **Contenedor de destino** en **copia de seguridad**.
        - **Cree** la regla de replicación. 
    - Opcionalmente, como tiene tiempo, cargue un archivo en el contenedor **público**. Vuelva a la cuenta de almacenamiento **privada** y actualice el contenedor de **copia de seguridad**. En unos minutos, el archivo de sitio web público aparecerá en la carpeta de copia de seguridad. 

>**Nota**: Para practicar más, complete el módulo [Configuración de Azure Blob Storage](https://learn.microsoft.com/training/modules/configure-blob-storage/). El módulo tiene una simulación de laboratorio interactiva en la que puede practicar más la creación de almacenamiento de blobs. 

