---
title: Acceder a GitHub utilizando la autenticación de dos factores
intro: 'Cuando habilitas la 2FA, se te pedirá que proporciones tu código de 2FA así como tu contraseña al momento de iniciar sesión en {% data variables.product.product_name %}.'
redirect_from:
  - /articles/providing-your-2fa-security-code
  - /articles/providing-your-2fa-authentication-code
  - /articles/authenticating-to-github-using-fido-u2f-via-nfc
  - /articles/accessing-github-using-two-factor-authentication
  - /github/authenticating-to-github/accessing-github-using-two-factor-authentication
  - /github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa/accessing-github-using-two-factor-authentication
versions:
  fpt: '*'
  ghes: '*'
  ghec: '*'
topics:
  - 2FA
shortTitle: Acceso a GitHub con 2FA
---

Al tener la autenticación de dos factores habilitada, necesitarás proporcionar el código de autenticación cuando accedes a {% data variables.product.product_name %} a través de tu buscador. Si accedes a {% data variables.product.product_name %} utilizando otros métodos, tales como la API o la línea de comandos, necesitarás utilizar una forma alterna de autenticación. Para obtener más información, consulta la sección "[Acerca de la autenticación en {% data variables.product.prodname_dotcom %}](/github/authenticating-to-github/about-authentication-to-github)".

## Proporcionar un código 2FA al iniciar sesión en el sitio web

Después de iniciar sesión en {% data variables.product.product_name %} con tu contraseña, se te pedirá que brindes un código de autenticación desde un mensaje de texto de {% ifversion fpt or ghec %} o {% endif %} tu app TOTP.

{% data variables.product.product_name %} solo te pedirá que brindes tu código de autenticación 2FA nuevamente si has cerrado sesión, estás usando un dispositivo nuevo o si caduca tu sesión.

### Generar un código a través de una aplicación TOTP

Si decides configurar una autenticación de dos factores mediante una aplicación TOTP en tu smartphone, puedes generar un código de autenticación para {% data variables.product.product_name %} en cualquier momento. En la mayoría de los casos, el lanzamiento de la aplicación generará un código nuevo. Deberías consultar la documentación de la aplicación para conocer las instrucciones específicas.

Si eliminas las aplicaciones móviles después de configurar la autenticación de dos factores, deberás proporcionar tu código de recuperación para obtener acceso a tu cuenta. Para obtener más información, consulta "[Recuperar tu cuenta si perdiste las credenciales de autenticación de dos factores](/articles/recovering-your-account-if-you-lose-your-2fa-credentials)"

{% ifversion fpt or ghec %}

### Recibir un mensaje de texto

Si configuras una autenticación de dos factores mediante mensajes de texto, {% data variables.product.product_name %} te enviará un mensaje de texto con tu código de autenticación.

### Verificar con {% data variables.product.prodname_mobile %}

Si instalaste e iniciaste sesión en {% data variables.product.prodname_mobile %}, podrías elegir autenticarte con {% data variables.product.prodname_mobile %} para la autenticación bifactorial.

1. Inicia sesión en {% data variables.product.product_name %} con tu buscador, utilizando tu usuario y contraseña.
2. Si agregaste una llave de seguridad a tu cuenta, primero se te pedirá insertar y utilizar una llave de seguridad. Para omitir el uso de una llave de seguridad, haz clic en **Autenticarse con {% data variables.product.prodname_mobile %}**. ![El reto de autenticación bifactorial en {% data variables.product.product_name %} con "Autenticarse con {% data variables.product.prodname_mobile %}" resaltado](/assets/images/help/2fa/2fa-select-mobile.png)
3. {% data variables.product.product_name %} te enviará una notificación push para verificar tu intento de inicio de sesión. Abrir la notificación push o abrir la app de {% data variables.product.prodname_mobile %} mostrará un mensaje que te pide aprobar o rechazar este intento de inicio de sesión.
  {% note %}

  **Nota:**: Este mensaje podría requerir que ingreses un número de dos dígitos que se muestra dentro del buscador en el que iniciaste sesión.

  {% endnote %}

  ![El reto de autenticación bifactorial con {% data variables.product.prodname_mobile %} que requiere una entrada de dos dígitos](/assets/images/help/2fa/2fa-mobile-number-challenge.png)

    - Cuando apruebes el intento de inicio de sesión utilizando {% data variables.product.prodname_mobile %}, tu buscador completará el inicio de sesión automáticamente.
    - Si rechazas el intento de inicio de sesión, se prevendrá la finalización de la autenticación. Para obtener más información, consulta la sección "[Mantener tus datos y tu cuenta seguros](/authentication/keeping-your-account-and-data-secure)".

{% endif %}

## Usar autenticación de dos factores con la línea de comando

Después de que habilitas la 2FA, ya no utilizarás tu contraseña para acceder a {% data variables.product.product_name %} en la línea de comandos. En vez de esto, utiliza el Administrador de Credenciales de Git, un token de acceso personal o una llave SSH.

### Autenticarse en la línea de comandos utilizando el Administrador de Credenciales de Git

El [Administrador de Credenciales de Git](https://github.com/GitCredentialManager/git-credential-manager/blob/main/README.md) es un asistente seguro de credenciales de Git que se ejecuta en Windows, macOS y Linux. Para obtener más información sobre los asistentes de credenciales de Git, consulta la sección [Evitar la repetición](https://git-scm.com/docs/gitcredentials#_avoiding_repetition) en el libro de Pro Git.

Las instrucciones de configuración pueden variar dependiendo del sistema operativo de tu computadora. Para obtener más información, consulta la sección [Descargar e instalar](https://github.com/GitCredentialManager/git-credential-manager/blob/main/README.md#download-and-install) en el repositorio GitCredentialManager/git-credential-manager.

### Autenticación en la línea de comando mediante HTTPS

Después de haber habilitado 2FA, debes crear un token de acceso personal para usar una contraseña al autenticar a {% data variables.product.product_name %} en la línea de comando mediante las URL HTTPS.

Cuando se te solicite el nombre de usuario y la contraseña en la línea de comando, usa tu nombre de usuario {% data variables.product.product_name %} y el token de acceso personal. La indicación de la línea de comando no especificará que debes ingresar tu token de acceso personal cuando se te solicite la contraseña.

Para obtener más información, consulta la sección "[Crear un token de acceso personal](/github/authenticating-to-github/creating-a-personal-access-token)".

### Autenticar en la línea de comandos mediante SSH

La habilitación de 2FA no cambia el modo de autenticar a {% data variables.product.product_name %} en la línea de comando mediante las URL SSH. Para obtener más información sobre cómo establecer y usar una clave SSH, consulta "[Conectar a {% data variables.product.prodname_dotcom %} con SSH](/articles/connecting-to-github-with-ssh/)".

## Usar autenticación de dos factores para acceder a un repositorio mediante Subversion

Cuando accedas a un repositorio mediante Subversion, debes proporcionar un token de acceso personal en lugar de ingresar tu contraseña. Para obtener más información, consulta la sección "[Crear un token de acceso personal](/github/authenticating-to-github/creating-a-personal-access-token)".

## Solución de problemas

Si pierdes el acceso a tus credenciales de autenticación de dos factores, puedes usar tus códigos de recuperación u otro método de recuperación (si has configurado uno) para recuperar el acceso a tu cuenta. Para obtener más información, consulta "[Recuperar tu cuenta si pierdes tus credenciales de 2FA](/articles/recovering-your-account-if-you-lose-your-2fa-credentials)".

Si tu autenticación falla varias veces, es posible que desees sincronizar el reloj de tu teléfono con tu proveedor móvil. Frecuentemente, esto involucra la verificación de la opción "Establecer automáticamente" en el reloj de tu teléfono, en lugar de brindar tu propia zona horaria.

## Leer más

- "[Acerca de la autenticación de dos factores](/articles/about-two-factor-authentication)"
- [Configurar autenticación de dos factores](/articles/configuring-two-factor-authentication)"
- [Configurar métodos de recuperación de autenticación de dos factores](/articles/configuring-two-factor-authentication-recovery-methods)"
- [Recuperar tu cuenta si pierdes tus credenciales de autenticación de dos factores](/articles/recovering-your-account-if-you-lose-your-2fa-credentials)"