---
title: Versiones del producto y ciclo de vida de integraciones de Adobe Sign
description: Obtenga información sobre las versiones de integraciones de Adobe Sign y el ciclo de vida de soporte
audience: External
products: Adobe Sign
type: Documentation
solution: Acrobat Sign, Adobe Sign
role: User, Developer
topic: Integrations
exl-id: c1f22848-7951-4066-84d4-f8cf6c2f3a6f
source-git-commit: b326a9afa2c16333d390cac3b30a2c7c741a4360
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 40%

---

# Versiones del producto y ciclo de vida {#version}

La convención de versiones de Adobe Sign y el ciclo de vida de soporte de los servicios integrados se alinean con otros productos de Adobe que tal vez conozca.

## Números de versión

La versión del paquete utiliza un sistema de numeración de tres partes para identificar el número de compilación secuencial de la versión publicada y la importancia relativa de la actualización en cuanto al contenido nuevo o modificado.

El número de versión sigue este patrón: N.m.p

Donde, N = Versión principal; m = Versión secundaria; p = Versión con parches.

Por ejemplo, la versión 23.2.1 de un paquete de integración indica lo siguiente:

* Versión principal: 23
* Versión secundaria: 2
* Versión del parche: 1

A medida que los ingenieros desarrollan nuevas &quot;compilaciones&quot; del paquete, aumentan el número de versión según la naturaleza de las actualizaciones del código.

* Los cambios de versión principales implican una adición significativa de funciones o un cambio importante en los sistemas principales.
* Las actualizaciones de versiones secundarias incluyen actualizaciones de funciones menores y parches de seguridad. Adobe Sign puede requerir una actualización a la versión de parches más reciente en caso de actualizaciones de seguridad o para solucionar un problema sobre el que se ha informado.
* Las versiones de parches son casi exclusivamente correcciones de errores y ajustes en la interfaz de usuario.

>[!NOTE]
>
>Todas las versiones no se distribuyen al público, ya que el producto itera en el desarrollo. Por lo tanto, puede haber saltos significativos en la versión de parche entre versiones.

Los administradores deben mantener su versión actualizada para garantizar que la cuenta tenga acceso completo a todas las funciones y que se apliquen parches a todos los problemas de seguridad conocidos. Adobe Sign puede requerir una actualización a la versión de parches más reciente en caso de problemas de seguridad o para solucionar un problema crítico del sistema.

## Ciclo de vida de soporte de versión

El ciclo de vida de soporte de la versión de un producto de integración de Adobe Sign se define en función de la versión principal del paquete e indica el intervalo de tiempo durante el cual Adobe Sign respalda activamente la versión individual de la integración.

Adobe Sign admite la versión actual de un paquete y las dos versiones principales anteriores (incluidas todas las actualizaciones secundarias y de parches relacionadas). Las versiones principales se expresan de la siguiente manera:

* Versión actual (N): la versión principal más reciente del paquete
* Versión anterior (N-1): la versión principal anterior a la más reciente
* Última versión compatible (N-2): dos versiones principales por detrás de la versión actual

Por ejemplo, si la versión actual del paquete es la 23.2.1:

* La versión principal actual (N) es la 23
* La versión principal anterior (N-1) de este paquete es la 22
* La última versión principal compatible (N-2) de este paquete es la 21
* Las versiones principales anteriores a la 21.0.0 no serán compatibles

![Gráfico de versiones](images/version_chart.png)

## Ciclo de vida del servicio de versión

El ciclo de vida del servicio de la versión define el ámbito completo de cuándo se puede utilizar el servicio. La cronología coincide con el ciclo de vida de soporte de la versión con la adición de un período de gracia de 90 días que permite a los clientes completar su actualización.

* Durante el período de gracia de una versión no compatible, solo se proporciona soporte para actualizar a una versión más nueva, no para mantener una versión no compatible.
* Después del período de gracia, la versión queda fuera de servicio

* Adobe Sign no aceptará solicitudes de versiones que no estén en servicio
* Una vez que la integración se actualice a la versión actual, las comunicaciones entre Adobe Sign y la integración se reanudarán normalmente.

![Período de cierre](images/shutdown_period.png)

Si tiene cualquier pregunta, póngase en contacto con su distribuidor o con Asistencia al cliente.
