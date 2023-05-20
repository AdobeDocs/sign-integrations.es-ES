---
title: Notas de la versión de Adobe Sign para NetSuite
description: Obtenga más información sobre las nuevas funciones y los cambios que se incluyen en la versión actual de la integración de Adobe Sign para NetSuite.
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 6317723e-447a-4506-a621-4d967bdd6561
source-git-commit: 4d73ff36408283805386bd3266b683bc187d6031
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Notas de la versión de Adobe Sign para NetSuite

## Actualizar al paquete v4.0.4

4.0.4 está totalmente adaptado para usar dominios específicos de cuenta para todo el tráfico recién generado.

El icono de Adobe Sign se ha actualizado al nuevo gráfico.

## Versiones anteriores

### Adobe Sign para NetSuite 4.0.4

4.0.4 está totalmente adaptado para usar dominios específicos de cuenta para todo el tráfico recién generado.

El icono de Adobe Sign se ha actualizado al nuevo gráfico.

### Adobe Sign para NetSuite 4.0.2

Renombrado para **Adobe Sign** (desde *Servicios eSign de Adobe Document Cloud*)\
Ya lo ves *Adobe Sign* donde antes vio *Adobe de eSign Services* como prueba de la renovación de la marca.

### Adobe Sign para NetSuite 4.0.1

Debido a un error de regresión de API introducido cuando NetSuite realizó la actualización de su plataforma, se ha lanzado un nuevo paquete (v4.0.1).

Se recomienda a los clientes que actualicen al paquete más reciente.

### Adobe Sign para NetSuite 4.0

**Se ha añadido el aprovisionamiento automático de usuarios mediante NetSuite**

Se ha añadido una nueva preferencia personalizada para la versión 4.0. Cuando está activada, los usuarios que envían acuerdos en NetSuite se aprovisionan automáticamente con una cuenta de usuario de los servicios de eSign de Adobe Document Cloud.

**Certificado con &#39;Built for NetSuite&#39;**

Esta versión ha obtenido la certificación &quot;Desarrollado para NetSuite&quot; y cumple todas las prácticas recomendadas de diseño de NetSuite más recientes.

**Cambio de nombre a los servicios eSign de Adobe Document Cloud (desde EchoSign)**

Ahora puede ver los servicios eSign de Adobe Document Cloud (o servicios eSign de Adobe para abreviar), donde anteriormente veía Adobe EchoSign como prueba de la renovación de la marca.

**Implementación de una seguridad mejorada con OAuth**

Para mejorar la seguridad de los datos, los servicios de eSign ahora utilizan OAuth 2.0 para autenticar su cuenta de servicios de eSign de Adobe Document Cloud en NetSuite. Este nuevo protocolo permite a NetSuite comunicarse con los servicios de eSign sin solicitar la contraseña de dichos servicios. Como la información confidencial no se comparte directamente entre las aplicaciones, es menos probable que su cuenta se vea comprometida. Esta mejora no afecta a su implementación, pero debe realizar una configuración única para autorizar que su paquete NetSuite se comunique con Adobe Document Cloud. Esto se hace durante el proceso de instalación. Para los clientes que actualicen desde una versión anterior del paquete (v3.5.9 y versiones anteriores), la clave de API utilizada anteriormente se sustituye por un token de OAuth generado durante el proceso de autorización.

**Se han migrado los servicios de eSign de las API SOAP a las API REST.**

Para mejorar la eficacia, la flexibilidad y la velocidad de procesamiento, los servicios eSign de Adobe Document Cloud y, en consecuencia, la integración de la versión 4.0 para NetSuite, han migrado de API basadas en SOAP a API basadas en REST.

### Adobe Sign para NetSuite 3.0

**Funciones avanzadas de participante: aprobador**

* Uno o más destinatarios pueden marcarse como aprobadores en un acuerdo
* Los aprobadores deben revisar y aprobar el documento
* También se puede solicitar a los aprobadores que rellenen los datos del acuerdo antes de aprobarlo

**Vista previa del documento o arrastrar y soltar campos de formulario antes de enviar**

Previsualiza el acuerdo o arrastra y suelta campos de formulario antes de enviarlos para su firma

**Enviar recordatorio al firmante actual**

Enviar recordatorio inmediato al firmante actual

**Directivas avanzadas de autenticación de firmantes**

* **Autenticación basada en conocimientos:** Responder preguntas para verificar la identidad del firmante
   * Requiere que los firmantes demuestren su identidad respondiendo a preguntas tomadas de cientos de bases de datos públicas y comerciales
   * El nombre en la firma se toma del nombre autenticado del usuario y no se puede cambiar en el momento de la firma
   * Con tecnología RSA
   * El uso de KBA está limitado por cuenta y mes. Ponte en contacto con el departamento de ventas para obtener más información.

* **Identidad web:** Inicie sesión con Facebook, LinkedIn, Google u otro servicio web de terceros antes de firmar.

   * El firmante solo puede firmar después de comprobar su identidad mediante un servicio web de terceros.
   * El nombre en la firma se toma del servicio web pro!le del usuario y no se puede cambiar en el momento de la firma
   * El seguimiento de auditoría captura los detalles de verificación de identidad

* **Contraseña de una sola vez**
   * Aplique métodos de autenticación para firmantes internos o externos o para todos los firmantes. Los firmantes externos deben utilizar una contraseña o una autenticación basada en conocimientos, mientras que los firmantes internos no

**Preferencias personalizadas adicionales**

* Añadir PDF firmado como vínculo a la URL o como archivo adjunto alojado en NetSuite
* Agregar pista de auditoría al registro del acuerdo cuando se firme un acuerdo de $er
* Usar el contacto de transacción como firmante de forma predeterminada, en lugar del correo electrónico del cliente
* Conceder a los remitentes la opción de marcar a los destinatarios como aprobadores

**Archivos de transacción**

Puede seleccionar archivos para adjuntar de la transacción actual con la nueva lista desplegable &quot;Archivos de transacción&quot;.

**Certificación de Adobe PDF para todos los documentos de EchoSign**

* Todos los archivos de PDF enviados o descargados desde EchoSign se certifican con un certificado digital de Adobe EchoSign
* Acrobat o Reader muestra el certificado que garantiza que el documento no se ha alterado para mayor confianza y tranquilidad

**Recopilar documentos complementarios**

* Los remitentes pueden recopilar documentos complementarios adicionales de los firmantes durante la firma, como el permiso de conducir, el certificado empresarial, etc.
* Los documentos recopilados pasan a formar parte del registro oficial del acuerdo firmado

**Campos de datos condicionales**

* Definir la lógica condicional para los campos del acuerdo
* Las condiciones pueden basarse en los valores de uno o varios campos del acuerdo
* Las condiciones se pueden definir mediante la interfaz de usuario de creación de formularios de arrastrar y soltar o mediante etiquetas de texto
* Al firmante se le presentan los campos apropiados al firmar un documento en función de las condiciones de firma.

**Mejoras adicionales en los campos de formulario de EchoSign**

* Menús desplegables
* Enmascaramiento de campos
* Botones de opción
* Creación de etiquetas de texto más cortas para mantener la estructura del documento
