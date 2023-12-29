---
demo:
  title: 'Demostración 3: Creación y configuración de almacenamiento de archivos y redes de almacenamiento'
  module: Guided Project - Azure Files and Azure Blobs
--- 

## Demostración: Creación y configuración de almacenamiento de archivos y redes de almacenamiento

En esta demostración, explore las redes de almacenamiento y el almacenamiento de Azure Files.

> **Nota:** En esta demostración, creará una cuenta de almacenamiento y una red virtual con subred. Se pueden crear previamente para ahorrar tiempo. 

## Revise Azure Files y cree una cuenta de almacenamiento específica para recursos compartidos de archivos.

1. [Diapositiva auxiliar] Antes de comenzar la demostración, analice qué es Azure File Storage y cómo es diferente de Azure Blob Storage. Más información: [Escenarios de Azure Storage](https://learn.microsoft.com/azure/storage/common/storage-introduction).

1. Acceda a **Azure Portal**.

1. Cree una **nueva** cuenta de almacenamiento de Azure. Esta cuenta se usará para satisfacer los requisitos de los archivos compartidos.

1. [Diapositiva auxiliar] En **Rendimiento** , seleccione **Premium**. 

1. En **Tipo de cuenta prémium**, seleccione **Recurso compartido de archivos**. Los recursos compartidos de archivos premium están pensados para aplicaciones de recursos compartidos de archivos empresariales o de alto rendimiento. Nuestro requisito de escenario es para un recurso compartido de archivos corporativo. 

1. En **Redundancia**, seleccione **Almacenamiento con redundancia de zona**. Recuerde a los alumnos que se recomiendan para escenarios de alta disponibilidad y protege frente a errores del centro de datos.

1. Vaya a la pestaña **Protección de datos**.

1. Destaque que la opción **habilitar la eliminación temporal para recursos compartidos de archivos** está **habilitada**.

1. **Revise** la cuenta de almacenamiento y, después, seleccione **Crear**.

## Configure el recurso compartido de archivos.

1. Continúe en la cuenta de almacenamiento.

1. En la hoja **Almacenamiento de datos**, seleccione **Recursos compartidos de archivos**.

1. Seleccione **Recurso compartido de archivos** y asigne el siguiente nombre al recurso compartido de archivos: **finance**.

1. Analice la **capacidad aprovisionada** y cómo un recurso compartido de archivos premium se factura según el tamaño del recurso compartido, con independencia de la capacidad usada. Como tiene tiempo, comente otras configuraciones. 

1. Analice **Protocolo** y seleccione **SMB**.

1. Seleccione **Crear**.

## Establezca la configuración del recurso compartido de archivos y cree una instantánea.

1. Seleccione el recurso compartido de archivos **finance**.

1. Revise la configuración en la parte superior de la página. Por ejemplo, **Cargar** y **Cambiar el tamaño y el rendimiento**.

1. Analice el propósito de las instantáneas. Más información: [Instantáneas de recursos compartidos de archivos](https://learn.microsoft.com/azure/storage/files/storage-snapshots-files).

1. En la hoja **Operaciones**, seleccione **Instantáneas**.

1. Seleccione **Agregar instantánea** y después **Aceptar**. Agregar un comentario es opcional.

1. Los alumnos cargarán archivos, crearán instantáneas y los restaurarán en el laboratorio.

## Configure el acceso de red para el almacenamiento.

1. [Diapositiva auxiliar] Antes de configurar las redes de almacenamiento, analice las distintas opciones. Revise algunas de las opciones de redes anteriores que se han configurado. 

1. En el portal, busque **Redes virtuales**.

1. Use la pestaña **Datps básicos** para crear una red virtual denominada **corpnet**. Cree una **subred** llamada **finance**. Destaque que esta red ya está creada.

1. Vuelva a la cuenta de almacenamiento.

1. Seleccione **Redes** en la hoja **Seguridad y redes**.

1. Seleccione **Habilitado desde redes virtuales y direcciones IP seleccionadas**.

1. En la página **Agregar red**, agregue la red virtual **corpnet** y la subred **finance**.

1. **Habilite el punto de conexión**. Explique que un nuevo punto de conexión de servicio puede tardar hasta 15 minutos en crearse.

1. Revisela configuración del **firewall**.

1. Revise la sección **Enrutamiento de red** y compruebe que se está usando el enrutamiento de red de Microsoft.



1. Como tiene tiempo, demuestre brevemente el **explorador de almacenamiento**. 

>**Nota**: Los alumnos ahora deberían poder completar LAB_03. 
