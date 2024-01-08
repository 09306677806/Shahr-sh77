{% data variables.product.prodname_GH_advanced_security %} is available for enterprise accounts on {% data variables.product.prodname_ghe_cloud %}{% ifversion ghae %}, {% data variables.product.prodname_ghe_managed %},{% endif %} and {% data variables.product.prodname_ghe_server %}.{% ifversion fpt or ghec %} Some features of {% data variables.product.prodname_GH_advanced_security %} are also available for public repositories on {% data variables.product.prodname_dotcom_the_website %}. For more information, see "[About GitHub's products](/github/getting-started-with-github/githubs-products)."{% else %} For more information about upgrading your {% data variables.product.prodname_ghe_server %} instance, see "[About upgrades to new releases](/admin/overview/about-upgrades-to-new-releases)" and refer to the [{% data variables.enterprise.upgrade_assistant %}](https://support.github.com/enterprise/server-upgrade) to find the upgrade path from your current release version.{% endif %}