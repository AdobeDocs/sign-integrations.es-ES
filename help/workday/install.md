---
title: Guía de instalación de Workday
description: Guía de instalación para activar la integración de Adobe Sign con Workday
uuid: 56478222-fe66-4fa5-aac3-0ecdf2863197
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
discoiquuid: 29d55a25-6e2f-4c59-ae7c-c21bb82cecba
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Acrobat Sign, Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 8f12b524-2123-45d4-98d5-b2b23580a5ea
source-git-commit: b326a9afa2c16333d390cac3b30a2c7c741a4360
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 23%

---

# [!DNL Workday] Guía de instalación{#workday-installation-guide}

[**Contactar con el servicio de soporte técnico de Adobe Sign**](https://adobe.com/go/adobesign-support-center_es)

## Información general {#overview}

En este documento se explica cómo integrar Adobe Sign en su [!DNL Workday] inquilino. Para utilizar Adobe Sign en [!DNL Workday], necesitas saber cómo crear y modificar [!DNL Workday] elementos como:

* Marco del proceso empresarial
* Configuración del inquilino
* Informes y [!DNL Workday] integración de estudio

Los pasos de alto nivel para completar la integración son:

* Activar la cuenta administrativa en Adobe Sign (solo nuevos clientes)
* Configurar un grupo en Adobe Sign para que contenga la [!DNL Workday] usuario de integración
* Establecer la relación de OAuth entre [!DNL Workday] y Adobe Sign

## Activar la cuenta de Adobe Sign {#activating-your-adobe-sign-account}

Los clientes existentes con cuentas establecidas pueden saltar al [Configurar Adobe Sign para [!DNL Workday]](#config) tema.

Para los clientes que son nuevos en Adobe Sign y no tienen un inicio de sesión anterior, un especialista en incorporación de Adobes proporciona su cuenta (en Adobe Sign) para [!DNL Workday]. Una vez completado el proceso, recibirá un correo electrónico de confirmación, como se muestra a continuación.

![Imagen del mensaje de correo electrónico de bienvenida de Adobe Sign](images/welcome-email-2020.png)

Debe seguir las instrucciones del correo electrónico para inicializar su cuenta y acceder a su Adobe Sign [!UICONTROL Inicio] página.

![Página del tablero de Adobe Sign](images/classic-home.png)

## Configurar Adobe Sign para [!DNL Workday] {#config}

Para configurar Adobe Sign para [!DNL Workday], debe generar los dos objetos dedicados siguientes en el sistema Adobe Sign:

* **A [!DNL Workday] grupo**: [!DNL Workday] requiere un &quot;grupo&quot; dedicado en la cuenta de Adobe Sign para habilitar la funcionalidad de integración. El grupo Adobe Sign se utiliza para controlar únicamente el [!DNL Workday] uso de Adobe Sign. Cualquier otro uso potencial, como Salesforce.com o Arriba no se ve afectado. Las notificaciones por correo electrónico se eliminan en [!DNL Workday] para que el [!DNL Workday] los usuarios solo reciben notificaciones en sus [!DNL Workday] bandeja de entrada.

* **Un usuario de autenticación que contenga la clave de integración**: A [!DNL Workday] El grupo debe tener solo un administrador de nivel de grupo, que sea el titular autorizado de la clave de integración. Se recomienda que el administrador utilice una dirección de correo electrónico funcional como `HR@MyDomain.com` en lugar de un correo electrónico personal para reducir el riesgo de que el usuario quede desactivado en el futuro y, por lo tanto, se desactive la integración.

### Crear un usuario y un grupo en Adobe Sign {#create-a-user-and-group-in-adobe-sign}

Para crear un usuario en Adobe Sign:

1. Inicie sesión en Adobe Sign como administrador de la cuenta..
1. Vaya a **[!UICONTROL Cuenta]** > **[!UICONTROL Usuarios]**.
1. Haga clic en ![plus icon image](images/icon_plus.png) para crear un nuevo usuario.

   ![Imagen de la ruta de navegación para crear un usuario nuevo](images/navigate-to-group-unbranded.png)

1. En el cuadro de diálogo que se abre, proporcione los detalles del nuevo usuario:

   * Proporcione un correo electrónico funcional al que pueda acceder.
   * Introduzca un valor apropiado para Nombre y Apellidos.
   * Seleccionar **[!UICONTROL Crear un nuevo grupo para este usuario]** del grupo de usuarios.
   * Proporcione el **[!UICONTROL Nuevo nombre de grupo]** con un nombre intuitivo como *[!DNL Workday]*.

   ![Panel Crear usuario](images/create-user.png)

1. Haga clic en **[!UICONTROL Guardar]**.

   Te lleva de vuelta al [!UICONTROL Usuarios] que muestra el nuevo usuario con una **[!UICONTROL CREADO]** estado.

   ![Una vista del nuevo usuario creado](images/post-user-creation.png)

Para verificar la dirección de correo electrónico del usuario con el estado &quot;Creado&quot;:

1. Inicie sesión en el correo electrónico del nuevo usuario.
2. Busque el correo electrónico de bienvenida de Adobe Sign.
3. Haz clic donde dice **[!UICONTROL Haga clic aquí para establecer la contraseña]**.
4. Establezca la contraseña.

Una vez verificada la dirección de correo electrónico, el estado del usuario cambia de [!UICONTROL CREADO] para [!UICONTROL ACTIVO].

![Imagen del nuevo usuario activado](images/actived-users-575.png)

### Definir el usuario de autenticación {#define-the-authenticating-user}

Para ascender al nuevo usuario en la [!DNL Workday] grupo:

1. Vaya a la [!UICONTROL Usuarios] (si aún no existe).
2. Haga doble clic en el usuario en la [!DNL Workday] grupo.

   Esto abre un [!UICONTROL Editar] para los permisos de usuario.

3. Compruebe el **[!UICONTROL Administrador de grupo]**.
4. Haga clic en **[!UICONTROL Guardar]**.

![](images/user-permissions-edit1-575.png)

## Configure el [!DNL Workday] inquilino {#configure-workday}

Para completar la conexión entre [!DNL Workday] inquilino y Adobe Sign, tenemos que establecer una relación de confianza entre los servicios. Una vez hecho esto, podemos añadir un paso de Revisar documento que permita realizar el proceso de firma a través de Adobe Sign.

>[!NOTE]
>
>Adobe Sign se comercializa como Adobe Document Cloud en todo el [!DNL Workday] ambiente.

Para establecer la relación de confianza:

1. Inicie sesión en [!DNL Workday] como administrador de cuentas.
1. Abra el **[!UICONTROL Editar configuración del inquilino: procesos empresariales]** página.
1. Busque la sección [!UICONTROL Configuración de firma electrónica]:

   ![](images/esignature_configurations.png)

1. Haga clic en **[!UICONTROL Autenticar con Adobe]**.

   Esto inicia la secuencia de autenticación de OAuth2.0.

1. Cuando se le solicite, proporcione las credenciales del administrador del grupo de Adobe Sign que creó anteriormente.
1. Apruebe el acceso a Adobe Sign.

>[!NOTE]
>
>Asegúrese de cerrar sesión por completo en cualquier otra instancia de Adobe Sign antes de continuar.

Una vez realizada la conexión, se activa la opción Configuración de Adobe habilitada y puede comenzar a usar Adobe Sign con [!DNL Workday].

### Configurar el paso Revisar documento {#configure-review}

El documento para el paso Revisar documento puede ser uno de los siguientes:

* Un documento estático
* Documento generado por un paso de Generar documento en el mismo proceso empresarial
* Un informe con formato creado con el [!DNL Workday] Report Designer

Puede agregar cualquiera de estos documentos con [Etiquetas de texto de Adobe](https://adobe.com/go/adobesign_text_tag_guide_es) para controlar el aspecto y la posición de los componentes específicos de firma de Adobe. El origen del documento debe especificarse dentro de la definición de procesos empresariales. No es posible cargar un documento específico mientras el proceso empresarial está en ejecución.

La capacidad de tener grupos de firmantes serializados es única en Adobe Sign con un paso Revisar documento. Esto permite especificar grupos basados en roles que firman secuencialmente. Adobe Sign no admite grupos de firma paralelos.

Si necesita ayuda para configurar el paso Revisar documento, consulte la [Guía de inicio rápido](https://adobe.com//go/adobesign_workday_quick_start){target=&quot;_blank&quot;}.

## Soporte {#support}

### [!DNL Workday] apoyo {#workday-support}

[!DNL Workday] es el propietario de la integración y debe ser el primer punto de contacto para plantear preguntas sobre el ámbito de la integración, solicitudes de funciones o problemas sobre el funcionamiento diario de la integración.

Puede referirse a lo siguiente [!DNL Workday] artículos de la comunidad sobre cómo solucionar problemas de integración y generar documentos:

* [Solucionar problemas de integraciones de firma electrónica](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [Paso Revisar documentos](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [Generación dinámica de documentos](https://community.workday.com/saml/login?destination=/articles/176443)
* [Sugerencias para generar documentos](https://community.workday.com/node/183242)

### Compatibilidad con Adobe Sign {#adobe-sign-support}

Adobe Sign es el socio de la integración y debe ponerse en contacto con el mismo si la integración no puede obtener firmas o si la notificación de firmas pendientes falla.

Los clientes de Adobe Sign deben ponerse en contacto con el administrador de satisfacción del cliente (CSM) para obtener asistencia. También puede ponerse en contacto con el servicio de asistencia técnica de Adobe por teléfono: llame al 1-866-318-4100, espere a la lista de productos y luego introduzca 4 y 2 (tal y como se lo pidan).

* [Adición de etiquetas de texto de Adobe a los documentos](https://adobe.com/go/adobesign_text_tag_guide)
* [Revisar la configuración del documento y los ejemplos](https://www.adobe.com//go/adobesign_workday_quick_start)

## Preguntas habituales {#faq}

### ¿Por qué no se actualiza el estado en? [!DNL Workday] ¿incluso cuando el documento está totalmente firmado? {#why-is-the-status-not-being-updated-within-workday-even-the-document-is-fully-signed}

El estado del documento en [!DNL Workday] puede que no se refleje si el candidato no hace clic en el icono[!UICONTROL Enviar]&#39; después de iniciar sesión en Adobe Sign.

Según [!DNL Workday] tarea Comprobar estado de firma electrónica: Para iniciar el proceso, el usuario puede enviar la tarea Bandeja de entrada asociada.

Según [!DNL Workday] Desarrollo: La firma original completa el proceso sólo si el usuario envía la tarea de bandeja de entrada después de firmar el documento. Después de firmar, el iframe se cierra y se redirige al usuario a la misma tarea, donde puede hacer clic en el icono [!UICONTROL Enviar] para completar el proceso.
