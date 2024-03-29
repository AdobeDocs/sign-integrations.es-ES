---
title: Guía de instalación de Veeva Vault
description: Guía de instalación para habilitar la integración de Adobe Sign con Veeva
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 5d61a428-06e4-413b-868a-da296532c964
source-git-commit: 76f1be575130e89d96dfe45f7343382b3a519903
workflow-type: tm+mt
source-wordcount: '4171'
ht-degree: 0%

---

# [!DNL Veeva Vault] Guía de instalación{#veeva-installation-guide}

[**Contactar con Asistencia técnica de Adobe Acrobat Sign**](https://adobe.com/go/adobesign-support-center)

## Resumen {#overview}

En este documento se explica cómo integrar Adobe Acrobat Sign con [!DNL Veeva Vault] plataforma. [!DNL Veeva Vault] es una plataforma de gestión de contenido empresarial (ECM) creada para las ciencias biológicas. Una &quot;Caja fuerte&quot; es un repositorio de contenido y datos con un uso típico para solicitudes de normativas, informes de investigación, solicitudes de subvenciones, contratación general y mucho más. Una sola empresa puede tener varias &quot;cajas fuertes&quot; que deben mantenerse por separado.

Los pasos de alto nivel para completar la integración son:

* Active su cuenta administrativa en Adobe Acrobat Sign (solo nuevos clientes).
* Cree objetos para realizar un seguimiento del historial de un ciclo de vida de acuerdo en Vault.
* Cree un nuevo perfil de seguridad.
* Configurar un grupo en Adobe Acrobat Sign para que contenga la [!DNL Veeva Vault] usuario de integración.
* Cree copias y campos de documento.
* Configure acciones web y actualice el ciclo de vida del documento.
* Crear configuración de usuario y rol de usuario de tipo de documento.
* Conecte Veeva Vault a Adobe Acrobat Sign mediante middleware.

>[!NOTE]
>
>El administrador de Adobe Sign debe realizar los pasos de configuración de Adobe Acrobat Sign en Adobe Acrobat Sign.

## Configurar [!DNL Veeva Vault] {#configure-veeva}

Para configurar [!DNL Veeva Vault] Para la integración con Adobe Acrobat Sign, debe implementar los pasos que se indican a continuación.

### Paso 1. Crear grupo {#create-group}

Para configurar Adobe Acrobat Sign para [!DNL Vault], un nuevo grupo denominado *Grupo de administradores de Adobe Sign* se crea. Este grupo se utiliza para establecer la seguridad de nivel de campo de documento para los campos relacionados con Adobe Acrobat Sign y debe incluir *Perfil de integración de Adobe Sign* de forma predeterminada.

![Imagen de los detalles del evento de firma](images/create-admin-group.png)

### Paso 2. Implementar el paquete {#deploy-package}

[Implementar el paquete](https://helpx.adobe.com/content/dam/help/en/sign-integrations-new/veeva-vault/PKG-AdobeSign-Integration-Veeva.zip) y sigue los pasos. Una vez implementado, el paquete crea:

* Objetos personalizados: Objeto Signature, objeto Signatory, objeto Signature Event, objeto Process Locker
* Diseño de página de objeto de firma
* Diseño de página del objeto Evento de firma
* Diseño de página de objeto firmante
* Diseño de página de objeto de bloqueador de procesos
* Diseño de página de objeto del registro de tareas de integración de Adobe Sign
* Tipo de representación de Adobe Sign
* Tipo de copia original
* Campo compartido signature__c
* Acción web de Adobe Sign
* Cancelar acción web de Adobe Sign
* Conjunto de permisos Acciones de administrador de Adobe Sign
* Perfil de seguridad de Adobe Sign Integration Profile
* Función de aplicación Función de administrador de Adobe Sign
* Grupo de tipos de documento &quot;Documento de Adobe Sign&quot;
* Objeto de registro Tarea de integración de Adobe Sign

#### Objeto Signature {#signature-object}

El objeto de firma se crea para almacenar información relacionada con el acuerdo. Un objeto Signature es una base de datos que contiene información en los siguientes campos específicos:

**Campos de objeto de firma**

| Campo | Etiqueta | Tipo | Descripción |
|:---|:---|:---|:------- | 
| external_id__c | Id De Acuerdo | Cadena (100) | Contiene el ID exclusivo del acuerdo de Adobe Acrobat Sign |
| file_hash__c | Hash de archivo | Cadena (50) | Contiene la suma de comprobación md5 del archivo enviado a Adobe Acrobat Sign |
| name__v | Nombre | Cadena (128) | Contiene el nombre del acuerdo |
| sender__c | Remitente | Objeto (usuario) | Contiene la referencia al usuario de Vault que ha creado el acuerdo |
| signature_status__c | Estado de firma | Cadena (75) | Mantiene el estado del acuerdo en Adobe Acrobat Sign |
| signature_type__c | Tipo de firma | Cadena (20) | Mantiene el tipo de firma del acuerdo en Adobe Acrobat Sign (ESCRITA o ESIGN) |
| start_date__c | Fecha de inicio | FechaHora | Fecha en la que el acuerdo se ha enviado para firmar |
| cancelation_date__c | Fecha de cancelación | FechaHora | Contiene la fecha en que se canceló el acuerdo. |
| completed_date__c | Fecha de finalización | FechaHora | Contiene la fecha en que se completó el acuerdo. |
| viewable_rendition_used__c | Representación visible utilizada | Booleano | Marca que indica si se ha enviado una copia visible para firmar. (de forma predeterminada, es true) |
| plugin_version__c | Versión del complemento | Texto (10) | Se utiliza para permitir el procesamiento adecuado de todos los acuerdos creados antes de implementar una nueva versión 4.0. Nota: Después de implementar la versión 4.0 de la aplicación web personalizada, este campo se establecerá en 4.0 cada vez que se cree un registro de firma. |
| external_environment__c | Entorno externo | Texto (20) | Contiene el nombre del entorno de Adobe Sign en el que se ha creado el acuerdo. |

![Imagen de detalles del objeto de firma](images/signature-object-details.png)

#### Objeto Signatory {#signatory-object}

El objeto de firmante se crea para almacenar información relacionada con los participantes en un acuerdo. Contiene información en los siguientes campos específicos:

**Campos de objeto firmante**

| Campo | Etiqueta | Tipo | Descripción |
|:---|:---|:---|:------- | 
| email__c | Correo electrónico | Cadena (120) | Contiene el ID exclusivo del acuerdo de Adobe Acrobat Sign |
| external_id__c | ID de participante | Cadena (80) | Contiene el identificador único de participante de Adobe Acrobat Sign |
| name__v | Nombre | Cadena (128) | Contiene el nombre del participante de Adobe Acrobat Sign |
| order__c | Orden | Número | Conserva el número de pedido del participante del acuerdo de Adobe Acrobat Sign |
| role_c | Función | Cadena (30) | Mantiene la función del participante del acuerdo de Adobe Acrobat Sign |
| signature__c | Firma | Objeto (firma) | Contiene la referencia al registro principal de la firma |
| signature_status__c | Estado de firma | Cadena (100) | Mantiene el estado del participante del acuerdo de Adobe Acrobat Sign |
| user__c | Usuario | Objeto (usuario) | Contiene la referencia al registro de usuario del firmante si el participante es un usuario de Vault |

![Imagen de los detalles del firmante](images/signatory-object-details.png)

#### Objeto Evento de firma {#signature-event}

El objeto Evento de firma se crea para almacenar la información relacionada con eventos de un acuerdo. Contiene información en los siguientes campos específicos:

Campos de objeto de evento de firma

| Campo | Etiqueta | Tipo | Descripción |
|:---|:---|:---|:-------- | 
| acting_user_email__c | Correo electrónico del usuario interino | Cadena | Contiene el correo electrónico del usuario de Adobe Acrobat Sign que realizó la acción que provocó el evento que se generó |
| acting_user_name__c | Nombre de usuario interino | Cadena | Contiene el nombre del usuario de Adobe Acrobat Sign que realizó la acción que provocó el evento |
| description__c | Descripción | Cadena | Contiene la descripción del evento de Adobe Acrobat Sign |
| event_date__c | Fecha del evento | FechaHora | Celebra la fecha y hora del evento de Adobe Acrobat Sign |
| event_type__c | Tipo de evento | Cadena | Realiza el tipo de evento de Adobe Acrobat Sign |
| name__v | Nombre | Cadena | Nombre del evento generado automáticamente |
| participant_comment__c | Comentario del participante | Cadena | Contiene el comentario del participante de Adobe Acrobat Sign, si lo hubiera |
| participant_email__c | Correo electrónico del participante | Cadena | Contiene el correo electrónico del participante de Adobe Acrobat Sign |
| participant_role__c | Función de participante | Cadena | Tiene la función de participante en Adobe Acrobat Sign |
| signature__c | Firma | Objeto (firma) | Contiene la referencia al registro principal de la firma |
| external_id__c | ID externo | Texto (200) | Contiene el identificador de evento del acuerdo generado por Adobe Sign. |

![Imagen](images/signature-event-object-details.png)

#### Objeto de bloqueo de proceso {#process-locker}

Se crea un objeto de bloqueador de procesos para bloquear el proceso de integración de Adobe Acrobat Sign. No requiere ningún campo personalizado.

![Imagen de los detalles del evento de firma](images/process-locker-details.png)

#### Objeto Log de Tareas de Integración con Adobe Sign {#task-log}

Cree el registro de tareas de integración de Adobe Sign (as_int_task_log__c). Es un objeto de gran volumen que se utiliza para realizar un seguimiento de la ejecución de AgreementsEventsSynchronizerJob y AgreementsEventsProcessingJob.
AgreementsEventsSynchronizerJob: Esta tarea garantiza que todos los eventos de acuerdo que faltan en Adobe Sign se creen como eventos de firma activos en Vault para todas las firmas creadas en Vault en los últimos N días.
AgreementsEventsProcessingJob: Esta tarea garantiza que todos los documentos con registros de eventos de firma activos se procesen en función del tipo de evento.

Campos de objeto del registro de tareas de integración de Adobe Sign

| Campo | Etiqueta | Tipo | Descripción |
|:--|:--|:--|:---------| 
| start_date__c | Fecha de inicio | FechaHora | Fecha de inicio de tarea |
| end_date__c | Fecha de finalización | FechaHora | Fecha de finalización de tarea |
| task_status__c | Estado de tarea | Lista de selección | Mantiene el estado de la tarea: <br /> Completado (task_completed__c) Completado con errores (task_completed_with_errors__c) Error (task_failed__c) |
| task_type__c | Tipo de tarea | Lista de selección | Tipo de tarea de retención: <br><br> Eventos del acuerdo Sincronización (agreements_events_sync__c) Eventos del acuerdo Procesamiento (agreements_events_processing__c) |
| messages__c | Mensaje | Largo (32000) | Retener mensaje de tarea |

![Imagen de detalles del objeto del registro de tareas](images/task-log.png)

![Imagen de campos de objeto del registro de tareas](images/task-log-fields.png)

Los objetos Signature, Signatory, Signature Event, Process Locker y Task Log que forman parte del paquete de implementación tienen habilitada de forma predeterminada la propiedad &#39;Auditar cambios de datos para este objeto&#39;.

**Nota:** Puede hacer que Vault capture cambios de datos de registro de objeto en registros de auditoría habilitando la opción Auditar cambios de datos. Esta configuración está desactivada de forma predeterminada. Una vez que haya habilitado esta opción y creado registros, ya no podrá deshabilitarla. Si esta configuración está desactivada y existen registros, sólo un propietario del depósito puede actualizarla.

#### **Mostrar participantes e historial para el objeto de firma** {#display-participants-history}

El objeto Signature que viene como parte del paquete de implementación viene con la [Diseño de página de detalles de firma](https://vvtechpartner-adobe-rim.veevavault.com/ui/#admin/content_setup/object_schema/pagelayout?t=signature__c&amp;d=signature_detail_page_layout__c). El diseño de página tiene secciones para los participantes y el historial.

* La *Participantes* tiene la sección Objetos relacionados que está configurada como se muestra en la imagen siguiente.

   ![Imagen](images/edit-related-objects.png)

* Puede editar las columnas que se mostrarán para los participantes, como se muestra a continuación.

   ![Imagen](images/set-columns-to-display.png)

* La *Historial* tiene la sección Objetos relacionados que está configurada como se muestra en la imagen siguiente.

   ![Imagen](images/edit-related-object-in-history.png)

* Puede editar las columnas que se mostrarán para el historial, como se muestra a continuación.

   ![Imagen](images/select-columns-to-display.png)

#### **Ver participantes e historial de auditoría del documento de Adobe Acrobat Sign** {#view-participants-audit-history}

* Para ver los participantes y el historial de auditoría del documento de Adobe Acrobat Sign, seleccione el vínculo en la sección &quot;Firma de Adobe&quot; del documento.

   ![Imagen](images/view-participants-audit-history.png)

* La página que se abre muestra los participantes y el historial del documento de Adobe Acrobat Sign, como se muestra a continuación.

   ![Imagen](images/participants-and-history.png)

* Consulte el seguimiento de auditoría para Firmar como se muestra a continuación.

   ![Imagen](images/audit-trail.png)

### Paso 3. Configurar perfiles de seguridad {#security-profiles}

La implementación correcta del paquete en el paso 2 crea el perfil de integración de Adobe Sign. El perfil de integración de Adobe Sign se asigna a la cuenta del sistema y la utiliza la integración al llamar a las API Vault. Este perfil permite permisos para:

* API Vault
* Leer, crear, editar y eliminar: Firma, Firmante, Eventos de firma y Procesar objetos bloqueadores

Debe actualizar el grupo de administración de Adobe Sign (creado en el paso 1) configurando el perfil de seguridad incluido en Perfil de integración de Adobe Sign, como se muestra en la imagen siguiente.

![Imagen de los detalles del evento de firma](images/security-profiles.png)

### Paso 4. Crear usuario {#create-user}

El usuario de la cuenta del sistema Vault de la integración con Adobe Acrobat Sign debe:

* Tener un perfil de integración de Adobe Sign
* Tener un perfil de seguridad
* Tener una política de seguridad específica que deshabilita el vencimiento de la contraseña
* Ser miembro del grupo de administración de Adobe Sign.

Para ello, siga estos pasos:

1. Cree un usuario de la cuenta del sistema Vault de la integración de Adobe Acrobat Sign.

   ![Imagen de los detalles del evento de firma](images/create-user.png)

2. Añada el usuario al grupo de administradores de Adobe Sign.

   ![Imagen de los detalles del evento de firma](images/add-user.png)

### Paso 5. Configurar grupo de tipo de documento {#create-document-type-group}

Al implementar el paquete de Adobe Acrobat Sign, se crea un registro de grupo de tipo de documento denominado &quot;Documento de Adobe Sign&quot;.

![Imagen de grupos de tipos de documento](images/document-type-groups.png)

Debe agregar este grupo de tipos de documento para todas las clasificaciones de documentos que sean aptas para el proceso de Adobe Acrobat Sign. Como la propiedad de grupo de tipo de documento no se hereda de tipo a subtipo ni de subtipo a nivel de clasificación, debe establecerse para cada clasificación de documento elegible para Adobe Acrobat Sign.

![Imagen de los detalles de edición del documento](images/document-edit-details.png)

**Nota:** Si el objeto Configuración de función de usuario no contiene el campo que hace referencia al objeto Grupo de tipo de documento, debe agregar el campo. Para ello, vaya a **[!UICONTROL Objeto]** > **[!UICONTROL Configuración de rol de usuario]** > **[!UICONTROL Fields]** y complete los pasos necesarios, como se muestra en la siguiente imagen.

![Imagen de la configuración de funciones de usuario](images/create-setup-field.png)

![Imagen de tipo de documento](images/document-type.png)

### Paso 6. Crear configuración de funciones de usuario {#create-user-role-setup}

Una vez que los ciclos de vida se hayan configurado correctamente, el sistema debe asegurarse de que DAC añade el usuario Administrador de Adobe Sign para todos los documentos que sean aptos para el proceso de Adobe Acrobat Sign. Para ello, cree el registro de configuración de funciones de usuario adecuado que especifique:

* Grupo de tipos de documento como documento de Adobe Sign
* Función de aplicación como función de administrador de Adobe Sign
* Usuario de integración

![Imagen de la configuración de funciones de usuario](images/user-role-setup.png)

### Paso 7. Configurar campos de documento {#create-fields}

La implementación del paquete crea el siguiente nuevo campo de documento compartido que es necesario para establecer la integración:

* Firma (signature__c)

![Imagen](images/document-fields.png)

Para configurar los campos del documento:

1. Vaya a la pestaña Configuración y seleccione **[!UICONTROL Campos de documento]** > **[!UICONTROL Campos compartidos]**.
1. En el campo Mostrar sección, seleccione **[!UICONTROL Crear sección de visualización]** y asignar **[!UICONTROL Firma de Adobe]** como etiqueta Sección.

   ![Imagen](images/create-display-section.png)

1. Para los campos de documento compartido (signature__c), actualice la sección de interfaz de usuario con **[!UICONTROL Firma de Adobe]** como etiqueta de sección.
1. Agregue los dos campos compartidos a todos los tipos de documento que sean elegibles para Adobe Acrobat Signature. Para ello, en la página Documento base, seleccione **[!UICONTROL Añadir]** > **[!UICONTROL Campo compartido existente]** en la esquina superior derecha.

   ![Imagen](images/create-document-fields.png)

   ![Imagen](images/add-existing-fields.png)

   ![Imagen](images/use-shared-fields.png)

1. Ambos campos deben tener una seguridad específica que solo permita a los miembros del grupo de administración de Adobe Sign actualizar sus valores.

   ![Imagen](images/security-overrides.png)

Desactivar superposiciones de depósito (disable_vault_overlays__v) es un campo compartido existente. Opcionalmente, el campo puede tener una seguridad específica que permita actualizar su valor solo a los miembros del grupo de administración de Adobe Sign.

### Paso 8. Declarar representaciones de documentos {#declare-renditions}

El nuevo tipo de copia denominado *Adobe Sign Rendition (adobe_sign_rendition__c)* Vault lo utiliza para cargar documentos firmados del PDF en Adobe Acrobat Sign. Debe declarar la copia de Adobe Sign para cada tipo de documento que sea apto para Adobe Acrobat Signature.

![Imagen de tipos de representación](images/rendition-type.png)

![Imagen](images/edit-details-clinical.png)

El nuevo tipo de copia denominado *Copia original* (original_rendition__c) lo utiliza la integración del depósito como nombre de la copia que se debe utilizar para almacenar la copia visible original si el documento firmado se importa como copia visible.

Debe declarar la copia original para cada tipo de documento que sea apto para Adobe Acrobat Signature.

![Imagen](images/original-rendition.png)

Opcionalmente, el almacén puede tener un nuevo tipo de copia Adobe de copia de pista de auditoría (adobe_audit_trail_rendition__c), que utiliza la integración del almacén para almacenar el informe de pista de auditoría de Adobe.

Siga los pasos que se indican a continuación para configurar la representación de pista de auditoría de Adobe:

1. Vaya a **Tipo de copia** > **Crear nuevo tipo de copia**.
Cree el nuevo tipo de copia como representación de pista de auditoría (adobe_audit_trail_rendition__c).

   ![Imagen](images/audit-trail-rendition-setup-1.png)

1. Para ver y descargar la representación de pista de auditoría de Adobe para el documento, declare *Representación de pista de auditoría de Adobe* para cada tipo de documento que sea apto para Adobe Acrobat Signature.

   ![Imagen](images/audit-trail-rendition-setup-2.png)

**Nota**: Puede elegir adjuntar el informe de auditoría a la copia firmada habilitando **[!UICONTROL Adjuntar informe de auditoría a la copia firmada]** y también mostrar la copia habilitando ****[!UICONTROL Mostrar representación de Acrobat Sign]**** en Configuración de la IU de administración.

![Imagen](images/audit-trail-rendition-setup-3.png)

Cuando un usuario opta por un acuerdo de firma digital con la configuración anterior, aparece un mensaje (como se muestra a continuación) que indica que Adobe Acrobat Sign utiliza PDF Portfolio para combinar informes de seguimiento de auditoría y de PDF firmados digitalmente.

Para ver el contenido del documento junto con la firma digital y el seguimiento de auditoría, no seleccione &quot;Adjuntar informe de auditoría a la copia firmada&quot; con &quot;Mostrar copia de Acrobat Sign&quot; en la IU del administrador para la firma digital.

Puede utilizar la representación de pista de auditoría de Adobe para descargar o ver la pista de auditoría de Adobe como una copia independiente.

![Imagen](images/audit-trail-rendition-setup-4.png)

### Paso 9. Actualizar acciones web {#web-actions}

La integración de Adobe Acrobat Sign y Vault requiere la creación y configuración de dos acciones web:

* **Crear Adobe Sign**: Crea o muestra el acuerdo de Adobe Acrobat Sign.

   Tipo: Destino del documento: Visualización en las credenciales de almacén: Activar credenciales de publ. de sesión mediante URL de publ. de mensaje: <https://api.na1.adobesign.com/api/gateway/veevavaultintsvc/partner/agreement?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&vaultid=${Vault.id}&useWaitPage=true>

   ![Imagen de create Adobe Sign](images/create-adobe-sign.png)

* **Cancelar Adobe Sign**: Cancela un acuerdo existente en Adobe Acrobat Sign y devuelve el estado de un documento al inicial.

   Tipo: Destino del documento: Visualización en las credenciales de almacén: Activar credenciales de publ. de sesión mediante URL de publ. de mensaje: : <https://api.na1.adobesign.com/api/gateway/veevavaultintsvc/partner/agreement/cancel?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&vaultid=${Vault.id}&useWaitPage=true>

   ![Imagen de cancelar Adobe Sign](images/cancel-adobe-sign.png)

### Paso 10. Actualizar ciclo de vida del documento {#document-lifecycle}

Para cada tipo de documento que pueda optar a la firma de Adobe, debe actualizar el ciclo de vida del documento correspondiente agregando nuevos estados y funciones de ciclo de vida.

El ciclo de vida del acuerdo de Adobe Acrobat Sign tiene los siguientes estados:

* BORRADOR
* AUTHORING o DOCUMENTS_NOT_YET_PROCESSED
* OUT_FOR_SIGNATURE o OUT_FOR_APPROVAL
* FIRMADO o APROBADO
* CANCELADO
* CADUCADO

Para actualizar el ciclo de vida del documento, siga estos pasos:

1. Agregar función de ciclo de vida. La función de aplicación de administrador de Adobe Sign se debe añadir a todos los ciclos de vida utilizados por los documentos que pueden optar a Adobe Acrobat Signature, como se muestra a continuación.

   ![Imagen de funciones de administrador del ciclo de vida](images/document-lifecycle-admin-role.png)

   La función de administrador debe crearse con las siguientes opciones:

   * Control dinámico de acceso habilitado.
   * Reglas de uso compartido de documentos que solo incluyen grupos de tipos de documento, como se muestra en la imagen siguiente.

   ![Imagen de la regla de uso compartido de Adobe Sign](images/adobe-sign-sharing-rule.png)

2. Crear estados del ciclo de vida. Para ello, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración]** > **[!UICONTROL Ciclos de vida del documento]** > **[!UICONTROL Ciclos de vida generales]** > **[!UICONTROL Estados]** > **[!UICONTROL Crear]**. A continuación, cree los siguientes estados:

   * En Adobe Sign Draft

   ![Imagen de la regla de uso compartido de Adobe Sign](images/create-draft-state.png)

   * En Adobe Sign Authoring

   ![Imagen de la regla de uso compartido de Adobe Sign](images/create-authoring-state.png)

   * En la firma de Adobe

   ![Imagen de la regla de uso compartido de Adobe Sign](images/create-signing-state.png)

3. Añada acciones de usuario a los siguientes estados enumerados.

   Cuando se envía un documento de Vault a Adobe Acrobat Sign, su estado debe corresponder al estado en el que se encuentra el acuerdo. Para ello, añada los siguientes estados en todos los ciclos de vida utilizados por los documentos que pueden optar a la firma de Adobe:

   * **Antes de la firma del Adobe** (Revisado): Es un nombre de marcador de posición para el estado desde el que se puede enviar el documento a Adobe Acrobat Sign. Según el tipo de documento, puede ser Estado de borrador o Revisado. La etiqueta de estado del documento se puede personalizar según los requisitos del cliente. Antes del Adobe El estado de firma debe definir las dos acciones de usuario siguientes:

      * Acción que cambia el estado del documento a *En Adobe Sign Draft* estado. El nombre de esta acción de usuario debe ser el mismo para todos los tipos de documento de cualquier ciclo de vida.
      * Acción que llama a la acción web &quot;Adobe Sign&quot;. Este estado debe tener una seguridad que permita a la función de administrador de Adobe Sign: ver documento, ver contenido, editar campos, editar relaciones, descargar origen, administrar representaciones visibles y cambiar estado.

      ![Imagen del estado del ciclo de vida 1](images/lifecycle-state1.png)

      * Modificar *Revisado* estado de Seguridad Atómica, estableciendo *En Adobe Sign Draft* de forma predeterminada a Oculto y solo Ejecutar para *Función de administrador de Adobe Sign*.
      **Nota:** Si *Función de administrador de Adobe Sign* función no forma parte de *Seguridad Atómica:Acciones del Usuario*, Añadir **[!UICONTROL Función de administrador de Adobe Sign]** seleccionando **[!UICONTROL Editar]**> **[!UICONTROL Anulación de rol]**. A continuación, agregue **Función de administrador de Adobe Sign** para *Revisado* Estado.

      ![Imagen](images/lifecycle-state-reviewed.png)
      ![Imagen](images/lifecycle-state-reviewed-1.png)
      ![Imagen](images/lifecycle-state-reviewed-2.png)

   * **En Adobe Sign Draft**: Es un nombre de marcador de posición para el estado que indica que el documento ya está cargado en Adobe Acrobat Sign y que su acuerdo está en estado BORRADOR. Es un estado obligatorio. Este estado debe definir las siguientes cinco acciones de usuario:

      * Acción que cambia el estado del documento a *En Adobe Sign Authoring* estado. El nombre de esta acción de usuario debe ser el mismo para todos los tipos de documento de cualquier ciclo de vida.
      * Acción que cambia el estado del documento a *En estado de firma de Adobe*. El nombre de esta acción de usuario debe ser el mismo para todos los tipos de documento de cualquier ciclo de vida.
      * Acción que cambia el estado del documento a *Adobe Sign cancelado* estado. El nombre de esta acción de usuario debe ser el mismo para todos los tipos de documento de cualquier ciclo de vida.
      * Acción que llama a la acción Web *Adobe Sign*.
      * Acción que llama a la acción Web *Cancelar Adobe Sign*. Este estado debe tener una seguridad que permita a la función de administrador de Adobe Sign: ver documento, ver contenido, editar campos, editar relaciones, descargar origen, administrar representaciones visibles y cambiar estado.

      ![Imagen del estado del ciclo de vida 2](images/lifecycle-state2.png)

      * Modificar *En Adobe Sign Draft* seguridad atómica del estado: acciones *Adobe Sign cancelado*, *En Adobe Sign Authoring*, *En la firma de Adobe* debe estar oculto para todos excepto para la función de administrador de Adobe Sign
      **Nota:** Si *Función de administrador de Adobe Sign* no forma parte de *Seguridad atómica: Acciones de usuario*, añadir **[!UICONTROL Función de administrador de Adobe Sign]** seleccionando **[!UICONTROL Editar]** > **[!UICONTROL Anulación de rol]**. A continuación, agregue **[!UICONTROL Función de administrador de Adobe Sign]** función para *En Adobe Sign Draft* Estado.

      ![Imagen](images/atomic-security.png)

   * **En Adobe Sign Authoring**: Es un nombre de marcador de posición para el estado que indica que el documento ya está cargado en Adobe Acrobat Sign y que su acuerdo está en estado AUTHORING o DOCUMENTS_NOT_YET_PROCESSED. Es un estado obligatorio. Este estado debe tener definidas las siguientes cuatro acciones de usuario:

      * Acción que cambia el estado del documento a estado Cancelado de Adobe Sign. El nombre de esta acción de usuario debe ser el mismo para todos los tipos de documento, independientemente del ciclo de vida.
      * Acción que cambia el estado del documento a En estado de firma de Adobe. El nombre de esta acción de usuario debe ser el mismo para todos los tipos de documento, independientemente del ciclo de vida.
      * Acción que llama a la acción web &quot;Adobe Sign&quot;
      * Acción que llama a la acción web &quot;Cancelar Adobe Sign&quot;. Este estado debe tener una seguridad que permita a la función de administrador de Adobe Sign: ver documento, ver contenido, editar campos, editar relaciones, descargar origen, administrar representaciones visibles y cambiar estado.

      ![Imagen del estado del ciclo de vida 3](images/lifecycle-state3.png)

      * Modificar *En Adobe Sign Authoring* seguridad atómica del estado: acciones *Adobe Sign cancelado* y *En la firma de Adobe* debe estar oculto para todos excepto para la función de administrador de Adobe Sign
      **Nota:** Si *Función de administrador de Adobe Sign* no forma parte de *Seguridad atómica: Acciones de usuario*, añadir **[!UICONTROL Función de administrador de Adobe Sign]** seleccionando **[!UICONTROL Editar]** > **[!UICONTROL Anulación de rol]**. A continuación, agregue **[!UICONTROL Función de administrador de Adobe Sign]** función para *En Adobe Sign Authoring* Estado.

      ![Imagen](images/adobe-sing-authoring.png)

   * **En la firma de Adobe**: Es un nombre de marcador de posición para el estado que indica que el documento está cargado en Adobe Acrobat Sign y que su acuerdo ya se ha enviado a los participantes (estado OUT_FOR_SIGNATURE o OUT_FOR_APPROVAL). Es un estado obligatorio. Este estado debe tener definidas las siguientes cinco acciones de usuario:

      * Acción que cambia el estado del documento a estado Cancelado de Adobe Sign. El estado de destino de esta acción puede ser cualquiera que sea el requisito del cliente y puede ser diferente para diferentes tipos. El nombre de esta acción de usuario debe ser el mismo para todos los tipos de documento, independientemente del ciclo de vida.
      * Acción que cambia el estado del documento a Rechazado de Adobe Sign. El estado de destino de esta acción puede ser cualquiera que sea el requisito del cliente y puede ser diferente para diferentes tipos. El nombre de esta acción de usuario debe ser el mismo para todos los tipos de documento, independientemente del ciclo de vida.
      * Acción que cambia el estado del documento a estado Firmado en Adobe. El estado de destino de esta acción puede ser cualquiera que sea el requisito del cliente y puede ser diferente para diferentes tipos. Sin embargo, el nombre de esta acción de usuario debe ser el mismo para todos los tipos de documento, independientemente del ciclo de vida.
      * Acción que llama a la acción Web *Adobe Sign*.
      * Acción que llama a Acción Web *Cancelar Adobe Sign*. Este estado debe tener una seguridad que permita a la función de administrador de Adobe Sign: ver documento, ver contenido, editar campos, editar relaciones, descargar origen, administrar representaciones visibles y cambiar estado.

      ![Imagen del estado del ciclo de vida 4](images/lifecycle-state4.png)

      * Modificar *En la firma de Adobe* seguridad atómica del estado: acciones *Adobe Sign cancelado*, *Adobe Sign rechazado* y *Adobe firmado* debe estar oculto para todos excepto para la función de administrador de Adobe Sign
      **Nota:** Si *Función de administrador de Adobe Sign* no forma parte de *Seguridad atómica: Acciones de usuario*, añadir **[!UICONTROL Función de administrador de Adobe Sign]** seleccionando **[!UICONTROL Editar]** > **[!UICONTROL Anulación de rol]**. A continuación, agregue **[!UICONTROL Función de administrador de Adobe Sign]** función para *En la firma de Adobe* Estado.

      ![Imagen](images/in-adobe-signing-2.png)

      * **Adobe firmado (aprobado)**: Es un nombre de marcador de posición para el estado que indica que el documento se ha cargado en Adobe Acrobat Sign y que su acuerdo se ha completado (estado FIRMADO o APROBADO). Es un estado obligatorio y puede ser un estado de ciclo de vida existente, como Aprobado.
Este estado no requiere acciones del usuario. Debe tener una seguridad que permita a la función de administrador de Adobe Sign: ver documentos, ver contenido y editar campos.

   El siguiente diagrama ilustra las asignaciones entre los estados del acuerdo de Adobe Acrobat Sign y del documento de Vault, donde el estado &quot;Antes de la firma del Adobe&quot; es Borrador.

   ![Imagen](images/sign-vault-mappings.png)

### Paso 11. Agregar etapa de Adobe Sign a Ciclo de vida general en grupos de etapa de ciclo de vida

![Imagen](images/add-adobe-sign-stage.png)

### Paso 12. Establecer permisos para la función de usuario en el estado del ciclo de vida

Debe establecer los permisos adecuados para cada función de usuario en el estado del ciclo de vida, como se muestra en la imagen siguiente.

![Imagen](images/set-user-role-permissions.png)

### Paso 13. Configurar la seguridad atómica en función del estado del documento y la función de usuario

![Imagen](images/set-atomic-security.png)

### Paso 14. Crear mensajes de documento para Adobe Sign Cancelar

![Imagen](images/create-cancel-message.png)

## Connect [!DNL Veeva Vault] a Adobe Acrobat Sign mediante middleware {#connect-middleware}

Tras completar la configuración de [!DNL Veeva Vault] y la cuenta de administrador de Adobe Acrobat Sign, el administrador debe crear una conexión entre las dos cuentas mediante el middleware. La [!DNL Veeva Vault] y la conexión de la cuenta de Adobe Acrobat Sign la inicia Adobe Acrobat Sign Identity y, a continuación, se utiliza para almacenar el[!DNL Veeva Vault] identidad.
Para la seguridad y estabilidad del sistema, el administrador debe utilizar un [!DNL Veeva Vault] sistema/servicio/cuenta de utilidad, como `adobe.for.veeva@xyz.com`, en lugar de una cuenta de usuario personal, como `bob.smith@xyz.com`.

Un administrador de cuentas de Adobe Acrobat Sign debe seguir los pasos que se indican a continuación para conectarse [!DNL Veeva Vault] a Adobe Acrobat Sign mediante middleware:

1. Vaya a la [Adobe Acrobat Sign para [!DNL Veeva Vault] Página de inicio](https://static.adobesigncdn.com/veevavaultintsvc/index.html).
1. Seleccionar **[!UICONTROL Inicio de sesión]** en la esquina superior derecha.

   ![Imagen de inicio de sesión de middleware](images/middleware_login.png)

1. Para autorizar el nivel de acceso a la aplicación, seleccione el ámbito de Acrobat Sign OAuth como **[!UICONTROL CUENTA]** o **[!UICONTROL AGRUPAR]**. A continuación, seleccione **[!UICONTROL Autorizar]**.

   ![Imagen](images/middleware_oauth.png)

1. En la página de inicio de sesión de Adobe Acrobat Sign que se abre, proporcione el correo electrónico y la contraseña del administrador de la cuenta y, a continuación, seleccione **[!UICONTROL Iniciar sesión]**.

   ![Imagen](images/middleware-signin.png)

   Después de iniciar sesión correctamente, la página muestra el ID de correo electrónico asociado y una pestaña Configuración, como se muestra a continuación.

   ![Imagen](images/middleware_settings.png)

1. Seleccione la **[!UICONTROL Configuración]** .

   La página Configuración muestra las conexiones disponibles y *No hay conexiones disponibles* en el caso de la primera configuración de conexión, como se muestra a continuación.

   ![Imagen](images/middleware_newconnection.png)

1. Seleccionar **[!UICONTROL Agregar conexión]** para agregar una nueva conexión.

1. En el cuadro de diálogo Agregar conexión que se abre, proporcione los detalles necesarios, incluidos los [!DNL Veeva Vault] credenciales.

   Las credenciales de Adobe Acrobat Sign se rellenan automáticamente desde el inicio de sesión inicial de Adobe Sign.

   ![Imagen](images/middleware_addconnection.png)

1. Seleccionar **[!UICONTROL Validar]** para validar los detalles de la cuenta.

   Cuando la validación se realice correctamente, aparecerá la notificación &quot;El usuario ha validado correctamente&quot;, como se muestra a continuación.

   ![Imagen](images/middleware_validated.png)

1. Para restringir el uso a un determinado grupo de Adobe Acrobat Sign, expanda el **[!UICONTROL Grupo]** y seleccione uno de los grupos disponibles.

   ![Imagen](images/middleware_group.png)

1. Para adjuntar un informe de auditoría a la copia firmada, seleccione la casilla de verificación **[!UICONTROL Adjuntar informe de auditoría a la copia firmada]**.

   ![Imagen](images/add-audit-report.png)

1. Para permitir el aprovisionamiento automático de usuarios en Adobe Acrobat Sign, seleccione la casilla de verificación **[!UICONTROL Aprovisionamiento automático de usuarios de Sign]**.

   **Nota:** El aprovisionamiento automático de nuevos usuarios de Adobe Acrobat Sign solo funciona si se ha habilitado en el nivel de cuenta de Adobe Acrobat Sign en Adobe Acrobat Sign, además de habilitar **[!UICONTROL Aprovisionamiento automático de usuarios de Sign]** para el[!DNL Veeva Vault] Integración con Adobe Acrobat Sign como muestra el administrador de cuentas de Adobe Acrobat Sign a continuación.

   ![Imagen](images/allow-auto-provisioning.png)

1. Para configurar Adobe Sign Rendition para que se muestre en Veeva en lugar de Original Rendition, seleccione la casilla de verificación **[!UICONTROL Mostrar representación de Acrobat Sign]**.

   ![Imagen](images/edit-connection-dispplay-adobe-sign-rendition.png)

1. Seleccionar **[!UICONTROL Guardar]** para guardar la nueva conexión.

   La nueva conexión aparece en la ficha Configuración y muestra la integración correcta entre [!DNL Veeva Vault] y Adobe Acrobat Sign.

   ![Imagen](images/middleware_setup.png)

