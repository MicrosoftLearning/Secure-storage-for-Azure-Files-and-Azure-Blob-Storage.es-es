---
demo:
  title: "Demostración 1:\_Creación y configuración de cuentas de almacenamiento."
  module: Guided Project - Azure Files and Azure Blobs
---
## Demostración: Creación y configuración de cuentas de almacenamiento. 

En esta demostración, se explorarán las cuentas de almacenamiento.

1. [Diapositiva auxiliar] Antes de comenzar esta demostración, puede que quiera analizar cómo se organiza el almacenamiento y los factores que se deben tener en cuenta. 

1. Acceda a **Azure Portal**.

1. En el cuadro de búsqueda, escriba **Cuentas de almacenamiento**. Cuando comience a escribir, la lista se filtrará en función de la entrada.

1. Seleccione **Cuentas de almacenamiento**.

1. Seleccione **Crear**.

1. Explique cómo Azure Portal proporciona una interfaz de asistente fácil de usar. Los elementos marcados con un asterisco rojo (*) son obligatorios.

1. Seleccione la **suscripción**.

1. Seleccione el **grupo de recursos**.

1. Escriba un nombre para la cuenta de almacenamiento. Analice las restricciones de nomenclatura de la cuenta de almacenamiento.

1. Seleccione la región de la cuenta de almacenamiento. Revise qué región deben usar los alumnos en el laboratorio. Más información sobre las [zonas geográficas de Azure](https://azure.microsoft.com/explore/global-infrastructure/geographies/)

1. [Diapositiva auxiliar] Seleccione el rendimiento **estándar**. Obtenga más información sobre los [tipos de cuentas de almacenamiento](https://learn.microsoft.com/azure/storage/common/storage-account-overview).

1. [Diapositiva auxiliar] Seleccione **Redundancia** como almacenamiento con **redundancia local**. Más información acerca de la [redundancia en Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-redundancy).

1. Vaya a la pestaña **Avanzado**. En la sección **Seguridad**, resalte esta configuración. Tenga en cuenta que solo estamos cubriendo algunas cosas para que el alumno comience en su primer laboratorio. 

    - **Requiera la transferencia segura para las operaciones de API de REST**. De forma predeterminada, las solicitudes de cuenta segura solo se aceptan si provienen de conexiones seguras. Para obtener más información, consulte [Transferencia segura](https://learn.microsoft.com/azure/storage/common/storage-require-secure-transfer).

    - **Habilitación del acceso a la clave de la cuenta de almacenamiento** Analice cómo esta configuración puede deshabilitar el acceso a la cuenta de almacenamiento. Por ejemplo, el acceso a la cuenta de almacenamiento del departamento de TI podría deshabilitarse. Analice la importancia de proteger la clave. Para obtener más información, consulte [Administrar claves de acceso de cuentas de almacenamiento](https://learn.microsoft.com/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).

    - **Versión de TLS mínima**. Explique que el servicio de capa de transporte es para proteger las comunicaciones a través de la red. TLS es una versión mejorada de SSL. Es posible que los desarrolladores le pregunten qué versiones están disponibles. Para obtener más información, consulte [Servicio de capa de transporte](https://learn.microsoft.com/azure/storage/common/transport-layer-security-configure-minimum-version).

1. Explique que otras pestañas se tratarán a medida que los alumnos avancen por los laboratorios.

1. Seleccione **Revisar** y asegúrese de que no haya errores de validación. Analice los posibles errores de validación. 

1. Seleccione **Crear** y espere mientras se implementa la cuenta de almacenamiento. Señale los mensajes de notificación.

1. Demuestre cómo **ir al recurso**. Analice otras formas de llegar al recurso.

>**Nota**: Los alumnos ahora deberían poder completar LAB_01.
