---
title: Enabling GitHub.com repository search from your private enterprise environment
shortTitle: Search GitHub.com from enterprise
intro: 'You can connect your personal accounts on {% data variables.product.prodname_dotcom_the_website %} and your private {% data variables.product.prodname_enterprise %} environment to search for content in certain {% data variables.product.prodname_dotcom_the_website %} repositories{% ifversion fpt or ghec %} from your private environment{% else %} from {% data variables.product.product_name %}{% endif %}.'
redirect_from:
  - /articles/enabling-private-githubcom-repository-search-in-your-github-enterprise-account
  - /articles/enabling-private-github-com-repository-search-in-your-github-enterprise-server-account
  - /articles/enabling-private-githubcom-repository-search-in-your-github-enterprise-server-account
  - /articles/enabling-githubcom-repository-search-in-github-enterprise-server
  - /github/searching-for-information-on-github/enabling-githubcom-repository-search-in-github-enterprise-server
  - /github/searching-for-information-on-github/getting-started-with-searching-on-github/enabling-githubcom-repository-search-in-github-enterprise-server
versions:
  ghes: '*'
  ghae: '*'
topics:
  - GitHub search
---

## About search for {% data variables.product.prodname_dotcom_the_website %} repositories from {% data variables.product.product_name %}

You can search for designated private repositories on {% data variables.product.prodname_ghe_cloud %} from {% data variables.product.product_location %}{% ifversion ghae %} on {% data variables.product.prodname_ghe_managed %}{% endif %}. For more information about searching across environments, see "[About searching on GitHub](/github/searching-for-information-on-github/getting-started-with-searching-on-github/about-searching-on-github#searching-repositories-on-githubcom-from-your-private-enterprise-environment)."

## 必要な環境

An enterprise owner for {% data variables.product.product_name %} must enable {% data variables.product.prodname_github_connect %} and {% data variables.product.prodname_unified_search %} for private repositories. 詳しい情報については「[Enterpriseでの{% data variables.product.prodname_unified_search %}の有効化](/admin/configuration/configuring-github-connect/enabling-unified-search-for-your-enterprise)」を参照してください。

## Enabling {% data variables.product.prodname_dotcom_the_website %} repository search from {% data variables.product.product_name %}

1. Sign into {% data variables.product.product_name %} and {% data variables.product.prodname_dotcom_the_website %}.
1. {% data variables.product.product_name %} にあるページの右上隅でプロフィール画像をクリックしてから、[**Settings**] をクリックします。 ![ユーザバーの [Settings（設定）] アイコン](/assets/images/help/settings/userbar-account-settings.png)
{% data reusables.github-connect.github-connect-tab-user-settings %}
{% data reusables.github-connect.connect-dotcom-and-enterprise %}