---
title: Notas de la versión de Adobe Sign para NetSuite
description: Obtenga más información sobre las nuevas funciones y los cambios que se incluyen en la versión actual de la integración de Adobe Sign para NetSuite.
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 6317723e-447a-4506-a621-4d967bdd6561
source-git-commit: f8d0bc748872e675dc1c638eb4050efe9e3147ef
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 5%

---

# Notas de la versión de Adobe Sign para NetSuite

## Actualizar al paquete v4.0.4

4.0.4 está totalmente adaptado para usar dominios específicos de la cuenta para todo el tráfico recién generado.

El icono de Adobe Sign se ha actualizado al nuevo gráfico.

## Versiones anteriores

### Adobe Sign para NetSuite 4.0.4

4.0.4 está totalmente adaptado para usar dominios específicos de la cuenta para todo el tráfico recién generado.

El icono de Adobe Sign se ha actualizado al nuevo gráfico.

### Adobe Sign para NetSuite 4.0.2

Se ha cambiado la marca a **Adobe Sign** (de *Adobe Document Cloud eSign services*)\
Ahora ve *Adobe Sign* donde anteriormente veía *Adobe eSign Services* como evidencia de la renovación de la marca.

### Adobe Sign para NetSuite 4.0.1

Debido a un error de regresión de API introducido cuando NetSuite realizó la actualización de su plataforma, se ha lanzado un nuevo paquete (v4.0.1).

Se recomienda a los clientes actualizar al paquete más reciente.

### Adobe Sign para NetSuite 4.0

**Adición del aprovisionamiento automático de usuarios mediante NetSuite**

Se ha añadido una nueva preferencia personalizada para la versión 4.0. Cuando está activada, los usuarios que envían acuerdos en NetSuite se aprovisionan automáticamente con una cuenta de usuario de los servicios de Adobe Document Cloud eSign.

**Certificados con &#39;Creados para NetSuite&#39;**

Esta versión obtuvo la certificación &quot;Construido para NetSuite&quot; y cumple con todas las prácticas recomendadas de diseño de NetSuite más recientes.

**Se ha cambiado la marca a los servicios eSign de Adobe Document Cloud (desde EchoSign)**

Ahora verá los servicios eSign de Adobe Document Cloud (o los servicios eSign de Adobe para abreviar), donde anteriormente veía Adobe EchoSign como evidencia de la renovación de la marca.

**Se ha implementado una seguridad mejorada con OAuth**

Para mejorar la seguridad de los datos, los servicios de eSign ahora utilizan OAuth 2.0 para autenticar su cuenta de servicios de Adobe Document Cloud eSign dentro de NetSuite. Este nuevo protocolo permite a NetSuite comunicarse con los servicios de eSign sin solicitar la contraseña de los servicios de eSign. Como la información confidencial no se comparte directamente entre aplicaciones, la cuenta estará menos expuesta a riesgos. Esta mejora no afecta a su implementación, pero debe realizar una configuración única para autorizar que su paquete NetSuite se comunique con el Adobe Document Cloud. Esto se lleva a cabo durante el proceso de instalación. Para los clientes que actualicen desde una versión anterior del paquete (v3.5.9 y anteriores), la clave de API utilizada anteriormente se sustituye por un token de OAuth generado durante el proceso de autorización.

**Se han migrado los servicios de eSign de las API de SOAP a las API de REST**

Para mejorar la eficiencia, la flexibilidad y la velocidad de procesamiento, los servicios eSign de Adobe Document Cloud y, en consecuencia, la integración v4.0 para NetSuite, han migrado de las API basadas en SOAP a las basadas en REST.

### Adobe Sign para NetSuite 3.0

**Funciones avanzadas de los participantes: aprobador**

* Uno o más destinatarios se pueden marcar como aprobadores en un acuerdo
* Los aprobadores deben revisar y aprobar el documento
* Los aprobadores también pueden tener que rellenar datos en el acuerdo antes de aprobarlo

**Vista previa de los campos de documento o arrastrar y soltar formulario antes de enviarlo**

Vista previa del acuerdo o arrastrar y soltar campos de formulario antes de enviarlos para firmar

**Enviar recordatorio al firmante actual**

Enviar recordatorio inmediato al firmante actual

**Directivas avanzadas de autenticación del firmante**

* **Autenticación basada en conocimientos:** responder preguntas para verificar la identidad del firmante
   * Requiere que los firmantes demuestren su identidad respondiendo a preguntas tomadas de cientos de bases de datos públicas y comerciales
   * El nombre de la firma se toma del nombre autenticado del usuario y no se puede cambiar en el momento de la firma
   * Con tecnología RSA
   * El uso de KBA es limitado por cuenta y mes. Póngase en contacto con Ventas para obtener más información.

* **Identidad web:** inicie sesión con Facebook, LinkedIn, Google u otro servicio web de terceros antes de firmar.

   * El firmante solo puede firmar después de verificar su identidad mediante un servicio web de terceros.
   * El nombre de la firma se toma del servicio web del usuario pro!le y no se puede cambiar en el momento de la firma
   * El seguimiento de auditoría captura los detalles de verificación de la identidad

* **Contraseña de una vez**
   * Aplicar métodos de autenticación para los firmantes internos o externos o para todos los firmantes. Los firmantes externos deben utilizar una contraseña o una autenticación basada en conocimientos, mientras que los firmantes internos no

**Preferencias personalizadas adicionales**

* Añadir PDF firmado como vínculo a la URL o como archivo adjunto alojado en NetSuite
* Agregar seguimiento de auditoría al acuerdo registra un acuerdo de $er firmado
* Usar el contacto de transacción como firmante de forma predeterminada, en lugar del correo electrónico del cliente
* Otorgar a los remitentes la opción de marcar a los destinatarios como aprobadores

**Archivos de transacción**

Puede seleccionar los archivos que desea adjuntar de la transacción actual con la nueva lista desplegable &quot;Archivos de transacción&quot;.

**Certificación de Adobe PDF para todos los documentos de EchoSign**

* Todos los archivos de PDF enviados o descargados de EchoSign están certificados con un certificado digital de Adobe EchoSign
* Acrobat o Reader muestra la certificación que garantiza que el documento no ha sido manipulado para mayor confianza y tranquilidad

**Recopilar documentos compatibles**

* Los remitentes pueden recopilar documentos de apoyo adicionales de los firmantes durante la firma, como un permiso de conducir, un certificado de empresa y mucho más.
* Los documentos recopilados forman parte del registro oficial del acuerdo firmado

**Campos de datos condicionales**

* Definición de lógica condicional para campos de acuerdo
* Las condiciones se pueden basar en valores para uno o varios campos del acuerdo
* Las condiciones se pueden deshacer mediante la interfaz de usuario de creación de formularios de arrastrar y soltar o mediante etiquetas de texto
* Al firmar un documento, el firmante recibe los campos correspondientes en función de las condiciones de eliminación

**Mejoras adicionales en los campos de formularios de EchoSign**

* Menús desplegables
* Enmascaramiento de campos
* Botones de opción
* Creación de etiquetas de texto más cortas para mantener la estructura del documento
