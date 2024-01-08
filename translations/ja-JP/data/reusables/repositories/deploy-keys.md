You can launch projects from a repository on {% ifversion ghae %}{% data variables.product.product_name %}{% else %}{% data variables.product.product_location %}{% endif %} to your server by using a deploy key, which is an SSH key that grants access to a single repository. {% data variables.product.product_name %} attaches the public part of the key directly to your repository instead of a personal account, and the private part of the key remains on your server. 詳しい情報については「[デプロイメントのデリバリー](/rest/guides/delivering-deployments)」を参照してください。