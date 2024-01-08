---
title: Agregar un gerente de facturación a tu organización
intro: 'Un *gerente de facturación* es un usuario que administra los parámetros de facturación de tu organización, como la actualización de la información de pago. Esta es una gran opción si los miembros regulares de tu organización habitualmente no tienen acceso a los recursos de facturación.'
redirect_from:
  - /articles/adding-a-billing-manager-to-your-organization
  - /github/setting-up-and-managing-organizations-and-teams/adding-a-billing-manager-to-your-organization
versions:
  fpt: '*'
  ghec: '*'
topics:
  - Organizations
  - Teams
  - Billing
shortTitle: Agregar un gerente de facturación
---

Los miembros del equipo Propietarios de tu organización pueden permitir que los *gerentes de facturación* proporcionen permisos a las personas. Una vez que una persona acepta la invitación para convertirse en gerente de facturación para tu organización, puede invitar a otras personas para convertirse en gerentes de facturación.

{% note %}

**Nota:**Los gerentes de facturación no utilizan licencias pagadas en la suscripción de tu organización.

{% endnote %}

## Permisos para los gerentes de facturación

Los gerentes de facturación pueden:

- Actualizar o bajar la categoría de la cuenta
- Agregar, actualizar o eliminar métodos de pago
- Ver historial de pagos
- Descargar recibos
- Ver, invitar y eliminar gerentes de facturación
- Iniciar, modificar o cancelar los patrocionios

Además, todos los gerentes de facturación recibirán recibos de facturación por correo electrónico en la fecha de facturación de la organización.

Los gerentes de facturación**no** pueden:

- Crear o acceder repositorios en tus organizaciones
- Ver miembros privados de tu organización
- Ser visto en la lista de los miembros de la organización
- Comprar, editar o cancelar suscripciones para aplicaciones de {% data variables.product.prodname_marketplace %}

{% tip %}

**Sugerencia:** Si tu organización [requiere que los miembros, gerentes de facturación y colaboradores externos usen autenticación de dos factores](/articles/requiring-two-factor-authentication-in-your-organization), el usuario debe habilitar la autenticación de dos factores antes de que puedan aceptar tu invitación para convertirse en gerentes de facturación para la organización.

{% endtip %}

## Invitar a un gerente de facturación

{% ifversion ghec %}
{% note %}

**Nota:** Si tu organización le pertenece a una cuenta empresarial, no podrás invitar a los gerentes de facturación a nivel de esta. Para obtener más información, consulta "[Acerca de las cuentas de empresa](/admin/overview/about-enterprise-accounts)".

{% endnote %}
{% endif %}

La persona invitada recibirá una invitación por correo electrónico solicitándole que se convierta en gerente de facturación para tu organización. Una vez que la persona invitada hace clic en el enlace de aceptación en el correo electrónico de la invitación, se agregarán automáticamente a la organización como gerentes de facturación. Si todavía no tienen una cuenta GitHub, deberán iniciar sesión para una cuenta, y se agregarán automáticamente a la organización como gerentes de facturación luego de crear una cuenta.

{% data reusables.organizations.billing-settings %}
1. Debajo de "Administración de la facturación", junto a "Gerentes de facturación", haz clic en **Agregar**. ![Invitar gerente de facturación](/assets/images/help/billing/settings_billing_managers_list.png)
6. Escribe el nombre de usuario o la dirección de correo electrónico de la persona a la que deseas agregar y haz clic en **Send invitation** (Enviar invitación). ![Página Invitar gerente de facturación](/assets/images/help/billing/billing_manager_invite.png)

## Leer más

- "[Invitar a las personas para que administren tu empresa](/enterprise-cloud@latest/admin/user-management/managing-users-in-your-enterprise/inviting-people-to-manage-your-enterprise)"{% ifversion fpt %} en la documentación de {% data variables.product.prodname_ghe_cloud %}{% endif %}