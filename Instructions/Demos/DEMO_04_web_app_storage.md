---
demo:
  title: 'Demostración 4: Creación y configuración del cifrado y el acceso seguro a aplicaciones'
  module: Guided Project - Azure Files and Azure Blobs
--- 

## Demostración: Creación y configuración del cifrado y el acceso seguro a aplicaciones. 

En esta demostración, explore el cifrado y la seguridad de aplicaciones.

> **Nota:** En esta demostración, creará una identidad administrada, un almacén de claves y una clave. Para ahorrar tiempo, es posible que quiera crear previamente estos recursos. 

## Cree un almacén de claves, una clave y una identidad administrada.

1. Cree una nueva cuenta de almacenamiento de Azure.. Se usará para mostrar características de almacenamiento seguras.

1. [Diapositiva auxiliar] Antes de empezar, revise cómo la nueva aplicación para desarrolladores debe acceder de forma segura al almacenamiento que necesita. Una identidad administrada accede a la aplicación. La identidad administrada usa una clave de cifrado que se almacena en Azure Key Vault. Azure Key Vault es un servicio en la nube que se usa para administrar claves, secretos y certificados. Este proceso reemplaza la necesidad de almacenar información de seguridad en el código de la aplicación.  No todos los alumnos pueden estar familiarizados con estos conceptos.

1. Cree una **identidad administrada**. Más información: [Identidades administradas](https://learn.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview).

1. Cree un **almacén de claves** con los valores predeterminados. Más información: [Azure Key Vault](https://learn.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).

1. Espere a que se implemente el contenedor y haga clic en **Ir al recurso**.

1. En la hoja **Objetos**, destaque las **claves, los secretos y los certificados**.

1. Seleccione **Claves** y, luego, elija **+ Generar/Importar**.

1. Asigne un **nombre** a la clave y, a continuación, **cree** la clave. Use los valores predeterminados.

## Configure la cuenta de almacenamiento para la identidad administrada y el almacén de claves y asigne permisos.

1. Vuelva a la cuenta de almacenamiento.

1. En la hoja **Seguridad y redes**, seleccione **Cifrado**.

    - Seleccione **Claves administradas por el cliente**. Analice la diferencia entre una clave administrada por Microsoft y las claves administradas por el cliente. Por ejemplo, se usa una clave administrada por Microsoft para el cifrado y descifrado automático de almacenamiento. Una aplicación podría usar una clave administrada por el cliente. Más información: [claves administradas por el cliente](https://learn.microsoft.com/azure/storage/common/customer-managed-keys-overview)

    - En **Tipo de almacén de claves**, seleccione **almacén de claves**. Las claves se pueden almacenar en software (almacén de claves) o en hardware (módulo de seguridad de hardware). Usamos el almacén de claves.

    - Seleccione su **almacén de claves** y la **clave**.

    - En **Tipo de identidad**, seleccione **Identidad administrada asignada por el sistema**. Este es el valor predeterminado que configura la identidad administrada para que pueda acceder al almacén de claves.

1. [Diapositiva auxiliar] En este momento, ha dado acceso a la identidad administrada al almacén de claves y ha asociado la identidad a la cuenta de almacenamiento. Use la identidad administrada del sitio web para acceder a la cuenta de almacenamiento. Consulte más información sobre la [asignación de roles de Azure](https://learn.microsoft.com/azure/role-based-access-control/role-assignments).

1. En la cuenta de almacenamiento, seleccione **Control de acceso (IAM)**. Más información sobre los [roles integrados de Azure](https://learn.microsoft.com/azure/role-based-access-control/built-in-roles)

    - Seleccione **Agregar** y, luego, **Agregar asignación de roles**. En la pestaña **Tipo de asignación**, señale que estamos asignando un rol de posición de trabajo.

    - Vaya a la pestaña **Rol** y busque **blob**. Seleccione el rol **Lector de datos de Blob Storage**.

    - Vaya a la pestaña **Miembros** y asigne acceso a la **identidad administrada**.

    - Seleccione **Seleccionar miembros** y seleccione la **identidad administrada asignada por el usuario**.

## Configure el almacenamiento inmutable.

1. [Diapositiva auxiliar] Los desarrolladores necesitan una manera de almacenar datos críticos para la empresa que no se pueden modificar ni eliminar durante un tiempo especificado por el usuario. El almacenamiento inmutable le permite proteger los datos de ser sobrescritos o eliminados. Analice las directivas de retención basadas en el tiempo y las directivas de suspensión legal. Más información: [Almacenamiento inmutable](https://learn.microsoft.com/azure/storage/blobs/immutable-storage-overview).

1. En la **cuenta de almacenamiento**, seleccione la hoja **Contenedor**.

1. **Cree** un contenedor denominado **hold** y **cargue** un archivo.

1. Acceda al contenedor **hold**y seleccione la hoja **Directiva de acceso**.

1. En la sección **Blob Storage inmutable**, seleccione **+ Agregar directiva**.

1. En **Tipo de directiva**, seleccione **Retención basada en tiempo**.

1. Establezca el **Período de retención** en **5 días**.

1. Asegúrese de **Guardar** los cambios.

1. Intente quitar el archivo en el contenedor.

1. Compruebe que no puede eliminar el archivo debido a la directiva.

## Configure un ámbito de cifrado para el cifrado de infraestructura.

1. Los desarrolladores también deben definir el ámbito del cifrado de infraestructura en el nivel de contenedor. Analice los ámbitos de cifrado y el cifrado de infraestructura. Más información: [Ámbitos de cifrado](https://learn.microsoft.com/azure/storage/blobs/encryption-scope-overview).

1. Continúe en **cuenta de almacenamiento**.

1. En la sección **Seguridad y redes**, seleccione **Cifrado**.

1. Vaya a la pestaña **Ámbito de cifrado** y seleccione **+ Agregar**.

1. Asigne un **nombre** al **ámbito de cifrado**.

1. Compruebe que el **cifrado de infraestructura** está **habilitado**. Señale la nota: “Esta opción no se puede cambiar después de crear este ámbito de cifrado”.

>**Nota**: Ahora, los alumnos deberían poder completar LAB_04. 
