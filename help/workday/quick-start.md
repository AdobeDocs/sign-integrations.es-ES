---
title: Guía de inicio rápido de Workday
description: Una guía de inicio rápido para los clientes que deseen utilizar Adobe Sign en sus entornos Workday.
uuid: 10bf8ee8-9075-44d1-a836-e454950e2d9a
products: Adobe Sign
content-type: reference
discoiquuid: 13135c88-4c39-4707-b7ba-63ff94769258
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 8b6fa8b4-e240-4ebe-ae2a-8807d75a6c69
source-git-commit: 2cc0ea55ee7dca3682896c61c85eec29a555339c
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 0%

---

# [!DNL Workday] Guía de inicio rápido{#workday-quick-start-guide}

[**Contactar con Asistencia técnica de Adobe Sign**](https://www.adobe.com/go/adobesign-support-center)

## Resumen {#overview}

Este documento está diseñado para ayudar [!DNL Workday] los administradores entienden cómo personalizar la [!DNL Workday] Procesos empresariales para incluir Adobe Sign y obtener firmas electrónicas. Para utilizar Adobe Sign en [!DNL Workday], debe saber cómo crear y modificar [!DNL Workday] elementos como:

* [!UICONTROL Business Process Framework]
* Configuración y configuración del inquilino
* Informes y [!DNL Workday] Integración de Studio

## Acceso a Adobe Sign en [!DNL Workday] {#access-adobe-sign}

[!UICONTROL Función de firma electrónica de Adobe Sign] aparece como [!UICONTROL Paso Revisar documento] acción dentro de la [!UICONTROL Business Process Framework (BPF)] y como tarea Distribuir documentos.

## [!UICONTROL Paso Revisar documento] {#review-document-step}

Adobe Sign para [!DNL Workday] se expone a través del [!UICONTROL Paso Revisar documento] que puede añadir a cualquiera de los más de 400 procesos empresariales de [!DNL Workday], incluidos [!UICONTROL Oferta], [!UICONTROL Distribuir documentos y tareas], [!UICONTROL Proponer compensación]y mucho más.

Puede consultar la [[!DNL Workday] artículos de la comunidad sobre [!UICONTROL Paso Revisar documento]](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg).

Hay una relación 1:1 entre [!UICONTROL [!UICONTROL Paso Revisar documento]s] y las transacciones facturables con Adobe Sign. Puede combinar varios documentos dentro de un mismo [!UICONTROL Paso Revisar documento] y se presentan como un único paquete para su firma.

**Nota**: Solo un *Dinámico* documento se puede hacer referencia dentro de un [!UICONTROL Paso Revisar documento].

Para definir una función [!UICONTROL Paso Revisar documento]:

1. Insertar un [!UICONTROL Paso Revisar documento].
1. Especifique los grupos (roles) que pueden actuar sobre el [!UICONTROL Paso Revisar documento].

![Pasos del proceso empresarial](images/insert-review-doc-steptornm-575.png)

Para configurar el [!UICONTROL Paso Revisar documento]:

1. Especifique el *[!UICONTROL Tipo de integración de firma electrónica]* as *[!UICONTROL Firmar electrónicamente por Adobe]*.

1. Agregue filas a la cuadrícula de firma.

   * La cuadrícula de firma especifica el orden en el que se envía el documento para su firma. Cada fila puede contener una o más funciones y cada fila representa un paso en el proceso de firma.
   * Se notifica a cada miembro del rol dentro de un paso determinado que hay un evento de firma pendiente.
   * Una vez que una sola persona de la función firma, el paso de fila se completa y el documento se mueve al siguiente paso de fila.
   * Cuando se hayan firmado todas las filas, el [!UICONTROL Paso Revisar documento] se ha completado.

1. Especifique el documento que se va a firmar. Si el documento es un [!UICONTROL Ofrecer BP], puede utilizarlo desde el paso Generar documento. De lo contrario, elija un documento o informe existente.

1. Repita el paso 3 para todos los documentos que necesite.

   ![Configurar Paso Revisar Documento](images/configure-rd-stepsmaller-575.png)

1. Opcionalmente, añada un &quot;usuario de redirección&quot; para capturar las acciones &quot;rechazar firmar&quot;. Cuando los usuarios rechazan, [!DNL Workday] redirige los documentos a un grupo de seguridad configurado para su revisión.

En el menú de acciones relacionadas de un [!UICONTROL Paso Revisar documento], seleccione **[!UICONTROL Proceso empresarial]** > **[!UICONTROL Mantener redirección]**. A continuación, seleccione una de las siguientes opciones:

* **[!UICONTROL Enviar atrás]**: Para permitir que los miembros del grupo de seguridad envíen un paso atrás a un paso anterior del proceso empresarial. El proceso empresarial se reinicia a partir de ese paso.
* **[!UICONTROL Ir al paso siguiente]**: Para permitir que los miembros del grupo de seguridad reenvíen un paso al siguiente paso del proceso empresarial.
* **[!UICONTROL Grupos de seguridad]**: Para redirigir pasos en el flujo del proceso empresarial. Los grupos de seguridad que se muestran en este mensaje se seleccionan en la directiva de seguridad del proceso empresarial de la sección Redirigir.

## Notas de los pasos del proceso empresarial {#business-process-step-notes}

La [!UICONTROL Business Process Framework] es poderoso; sin embargo, debe asegurarse de que:

* Cada proceso empresarial debe tener un paso de finalización, que es ideal al final del proceso empresarial.

* Se establece un paso de finalización en el menú de acciones relacionadas del icono de búsqueda. Esto solo es posible mientras se &quot;visualiza&quot; la PA y no mientras se &quot;edita&quot;.

* Cada paso del proceso empresarial se ejecuta secuencialmente.

   Puede cambiar el orden de un paso cambiando el valor de orden. Por ejemplo, para insertar un paso entre los elementos &quot;c&quot; y &quot;d&quot;, especifique un nuevo elemento como &quot;ca&quot;.

### Ejemplo: oferta {#example-offer}

La Oferta BP es un subproceso del [!UICONTROL BP dinámico de aplicación de trabajo] que debe configurarse para ejecutar la oferta de PA. Se activa cuando el estado de la aplicación de trabajo se mueve a &quot;[!UICONTROL Oferta]&quot; o &quot;[!UICONTROL Hacer oferta]&quot;.

En el ejemplo siguiente, un [!UICONTROL Paso Revisar documento] está utilizando un paso de documento dinámico para Norteamérica y Japón.

![Ejemplo de [!DNL Workday] Proceso empresarial](images/bp-for-offersmaller-575.png)

Este proceso empresarial realiza lo siguiente:

* Pide al iniciador del proceso empresarial que proponga una compensación para el candidato (paso b).
* Utiliza una condición de paso para comprobar si el país actual NO es Japón.

   Si es true, ejecuta el paso &quot;ba&quot;, que utiliza un documento en inglés.

   Si es false, ejecuta el paso &quot;bb&quot;, que utiliza un documento en japonés.

* Define el proceso de firma en el [!UICONTROL Paso Revisar documento] &quot;bc&quot;.
* Define el punto de decisión para realizar una oferta en el paso de finalización requerido &quot;d&quot;.

El documento dinámico que se genera en el paso &quot;ba&quot; se denomina [!UICONTROL Carta de oferta] y contiene un único bloque de texto denominado [!UICONTROL Oferta rápida]. Puede añadir varios bloques de texto, como encabezado, saludo, compensación, stock, cierre, condiciones, etc., según sea necesario.

![[!DNL Workday] ver página de documento](images/offer-letter-575.png)

La carta de oferta dinámica siguiente se crea en el [!DNL Workday] editor de texto enriquecido. Los elementos resaltados en *gris* son [!DNL Workday] objetos proporcionados que hacen referencia a datos contextuales.

Artículos en {{brackets}} son [Etiquetas de texto de Adobe](https://adobe.com/go/adobesign_text_tag_guide).

![Ejemplo de formulario dinámico](images/script.png)

Dentro del [!UICONTROL Paso Revisar documento], se hace referencia al documento dinámico desde el paso anterior y se define el proceso secuencial de firma mediante dos grupos de firma.

El comportamiento que se muestra a continuación enruta el documento generado dinámicamente primero al responsable de contratación y, a continuación, al candidato.

![[!DNL Workday] grupos de firma definidos](images/configure-rd-stepsmaller-575.png)

### Ejemplo: Distribuir documentos {#example-distribute-documents}

Introducido en [!DNL Workday] 30, la tarea Distribuir documentos o tareas de forma masiva se puede utilizar para enviar un único documento a un grupo grande (&lt;20K) de firmantes individuales. Se limita a una única firma por documento. La creación de una distribución se realiza accediendo a la[!UICONTROL Crear distribución de documentos o tareas]’ de la barra de búsqueda.

Ejemplo: Enviar un formulario de elección de equidad de empleado a todos los responsables con [!UICONTROL Servicios modernos globales]. Si lo desea, puede filtrarlo a responsables individuales.

También puede acceder al **Ver Distribuir documentos o tareas** para realizar un seguimiento del progreso de la distribución.

![](images/create-distributedocumentsortasks.png)

### Ejemplo: Informes {#example-reporting}

[!DNL Workday] cuenta con una infraestructura de informes muy completa. Para ver los detalles del proceso de Adobe Sign, inspeccione los elementos del *Evento Revisar documento*.

A continuación se muestra un informe personalizado simple que se puede ejecutar en todos los procesos empresariales que buscan transacciones de Adobe Sign y su estado.

![Ejemplo de [!DNL Workday] Informe personalizado](images/review-document-eventsmaller-575.png)

El siguiente informe se generó examinando los procesos de ofertas, incorporación y compensación propuesta dentro de un inquilino de implementación.

Puede ver:

* Los documentos enviados para firmar
* El paso de BP asociado
* La siguiente persona esperando firma

![Ejemplo de [!DNL Workday] Informe con tres objetos](images/workday-reportsmaller-575.png)

## Documentos firmados {#signed-documents}

La [!DNL Workday] El ciclo de firma suprime todas las notificaciones por correo electrónico de Adobe Sign. Se informa a los usuarios de las acciones pendientes en sus [!DNL Workday] bandeja de entrada.

Una vez que todos los grupos de firma han firmado un documento, se distribuye una copia del documento firmado a todos los miembros del grupo de firma por correo electrónico.

Para suprimir este comportamiento, puede ponerse en contacto con su [!UICONTROL Adobe Sign Success Manager] o el [Equipo de soporte de Adobe Sign](https://adobe.com/go/adobesign-support-center).

Dentro [!DNL Workday], puede acceder a los documentos firmados en el registro de proceso completo. Usted puede encontrar:

* Documentos de Worker en el perfil de Worker y
* Documentos del candidato (cartas de oferta) en el perfil del candidato.

La siguiente imagen muestra una carta de oferta firmada para el candidato Chris Foxx.

![Ejemplo [!DNL Workday] carta oferta](images/offer.png)

## Asistencia {#support}

### [!DNL Workday] apoyo {#workday-support}

[!DNL Workday] es el propietario de la integración y debe ser su primer punto de contacto para preguntas sobre el ámbito de la integración, solicitudes de funciones o problemas en el funcionamiento diario de la integración.

La [!DNL Workday] tiene varios artículos útiles sobre cómo solucionar problemas de integración y generar documentos:

* [Solucionar problemas de integraciones de firma electrónica](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [Paso Revisar documentos](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [Generación dinámica de documentos](https://community.workday.com/node/176443)
* [Sugerencias para la configuración de generación de documentos](https://community.workday.com/node/183242)

### Compatibilidad con Adobe Sign {#adobe-sign-support}

Adobe Sign es el socio de integración y se debe contactar con él si la integración no consigue obtener firmas o si falla la notificación de firmas pendientes.

Los clientes de Adobe Sign deben ponerse en contacto con su [!UICONTROL Customer Success Manager] para obtener ayuda. Alternativamente, [!UICONTROL Asistencia técnica de Adobe] Se puede contactar por teléfono: 1-866-318-4100, espere a la lista de productos y escriba: 4 y, a continuación, 2 (si se solicita).

* [Adición de etiquetas de texto de Adobe a documentos](https://www.adobe.com/go/adobesign_text_tag_guide)

<!--
[Download PDF](images/adobe-sign-for-workday-quick-start-guide-2016.pdf)
-->
