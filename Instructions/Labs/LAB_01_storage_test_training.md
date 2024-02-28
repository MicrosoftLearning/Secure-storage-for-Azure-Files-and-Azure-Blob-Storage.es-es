---
lab:
  title: 'Ejercicio 1: Proporcionar almacenamiento para las pruebas y el aprendizaje del departamento de TI'
  module: Guided Project - Azure Files and Azure Blobs
---

El departamento de TI debe crear prototipos de diferentes escenarios de almacenamiento y entrenar al nuevo personal. El contenido no es lo suficientemente importante como para realizar una copia de seguridad y no es necesario restaurarlo si los datos se sobrescriben o quitan. Es preferible una configuración sencilla que se pueda cambiar fácilmente.

## Diagrama de la arquitectura
![Diagrama con una cuenta de almacenamiento.](../Media/task-1.png)

## Tareas de aptitudes
- Cree una cuenta de almacenamiento. 
- Configure las opciones básicas para la seguridad y las redes. 

## Instrucciones del ejercicio

## Crear un grupo de recursos y una cuenta de almacenamiento.

1. Cree e implemente un grupo de recursos para contener todos los recursos del proyecto. Más información sobre los [grupos de recursos](https://learn.microsoft.com/azure/azure-resource-manager/management/manage-resource-groups-portal).
    - En Azure Portal, busque y seleccione `Resource groups`.
    - Seleccione **+ Create** (+ Crear).
    - Asigne un **nombre** al grupo de recursos. Por ejemplo, `storagerg`.
    - Seleccione una **región**. Use esta región en todo el proyecto. 
    - Haga clic en **Revisar y crear** para validar el grupo de recursos.
    - Haga clic en **Crear** para implementar el grupo de recursos.

1. Cree e implemente una cuenta de almacenamiento para admitir las pruebas y el entrenamiento. Obtenga más información sobre [los tipos de cuentas de almacenamiento](https://learn.microsoft.com/azure/storage/common/storage-account-overview#types-of-storage-accounts)
    - En Azure Portal, busque y seleccione `Storage accounts`. 
    - Seleccione **+ Create** (+ Crear).
    - En la pestaña **Datos básicos**, seleccione el **Grupo de recursos**.
    - Proporcione el **nombre de la cuenta de almacenamiento**. El nombre de la cuenta de almacenamiento debe ser exclusivo en Azure. 
    - Establezca el **Rendimiento** en **Estándar**. 
    - Seleccione **Revisar** y, después, **Crear**. 
    - Espere a que se implemente la cuenta de almacenamiento y, a continuación, seleccione **Ir al recurso**.  

## Configure opciones sencillas en la cuenta de almacenamiento.

1. Los datos de esta cuenta de almacenamiento no requieren alta disponibilidad ni durabilidad. Es preferible una solución de almacenamiento de costo mínimo. Obtenga más información sobre [la redundancia de la cuenta de almacenamiento](https://learn.microsoft.com/azure/storage/common/storage-redundancy#locally-redundant-storage).
    - En la cuenta de almacenamiento, en la sección **Administración de datos**, seleccione la hoja **Redundancia**.
    - Seleccione **Almacenamiento con redundancia local (LRS)** en la lista desplegable **Redundancia**. 
    - Asegúrese de **Guardar** los cambios. 
    - Actualice la página y observe que el contenido solo existe en el centro de datos principal. 

1. La cuenta de almacenamiento solo debe aceptar solicitudes de conexiones seguras. Obtenga más información sobre el [requisito de una transferencia segura desde conexiones seguras](https://learn.microsoft.com/azure/storage/common/storage-require-secure-transfer)
    - En la sección **Configuración**, seleccione la hoja **Configuración**.
    - Asegúrese de que la opción **Se requiere transferencia segura** está **habilitada**. 

1. Los desarrolladores desean que la cuenta de almacenamiento use al menos la versión 1.2 de TLS. Obtenga más información sobre la [seguridad de la capa de transporte (TLS)](https://learn.microsoft.com//azure/storage/common/transport-layer-security-configure-minimum-version?tabs=portal)
    - En la sección **Configuración**, seleccione la hoja **Configuración**.
    - Asegurarse de que la **Versión mínima de TLS** esté establecida en **Versión 1.2**.  


1. Hasta que se vuelva a necesitar el almacenamiento, deshabilite las solicitudes a la cuenta de almacenamiento. Obtenga más información sobre cómo [deshabilitar las claves compartidas](https://learn.microsoft.com/azure/storage/common/shared-key-authorization-prevent?tabs=portal#disable-shared-key-authorization).
    - En la sección **Configuración**, seleccione la hoja **Configuración**.
    - Asegúrese de que la opción **Permitir el acceso a la clave de la cuenta de almacenamiento** esté **Deshabilitada**.
    - Asegúrese de **Guardar** los cambios. 

1. Asegúrese de que la cuenta de almacenamiento permite el acceso público desde todas las redes.  
    - En la sección **Seguridad y redes**, seleccione la hoja **Redes**.
    - Asegúrese de que **Acceso a la red pública** esté establecido en **Habilitado desde todas las redes**.
    - Asegúrese de **Guardar** los cambios. 

>**Nota**: Para practicar más, complete el módulo [Creación de una cuenta de Azure Storage](https://learn.microsoft.com/training/modules/create-azure-storage-account/). El módulo tiene un espacio aislado donde puede practicar la creación de una cuenta de almacenamiento.
