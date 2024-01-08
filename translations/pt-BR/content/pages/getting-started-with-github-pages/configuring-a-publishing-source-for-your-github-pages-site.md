---
title: Configurar uma fonte de publicação para o site do GitHub Pages
intro: '{% ifversion pages-custom-workflow %}You can configure your {% data variables.product.prodname_pages %} site to publish when changes are pushed to a specific branch, or you can write a {% data variables.product.prodname_actions %} workflow to publish your site.{% else%}If you use the default publishing source for your {% data variables.product.prodname_pages %} site, your site will publish automatically. You can also choose to publish your site from a different branch or folder.{% endif %}'
redirect_from:
  - /articles/configuring-a-publishing-source-for-github-pages
  - /articles/configuring-a-publishing-source-for-your-github-pages-site
  - /github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
product: '{% data reusables.gated-features.pages %}'
permissions: 'People with admin or maintainer permissions for a repository can configure a publishing source for a {% data variables.product.prodname_pages %} site.'
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Pages
shortTitle: Configurar fonte de publicação
---

## About publishing sources

{% data reusables.pages.pages-about-publishing-source %}

{% data reusables.pages.private_pages_are_public_warning %}

## Publishing from a branch

1. Make sure the branch you want to use as your publishing source already exists in your repository.
{% data reusables.pages.navigate-site-repo %}
{% data reusables.repositories.sidebar-settings %}
{% data reusables.pages.sidebar-pages %}
{% ifversion pages-custom-workflow %}
1. Under "Build and deployment", under "Source", select **Deploy from a branch**.
1. Under "Build and deployment", under "Branch", use the **None** or **Branch** drop-down menu and select a publishing source.

   ![Menu suspenso para selecionar uma fonte de publicação](/assets/images/help/pages/publishing-source-drop-down.png)
{% else %}
3. Em "{% data variables.product.prodname_pages %}", use o menu suspenso **Nenhum** ou **Branch** e selecione uma fonte de publicação. ![Menu suspenso para selecionar uma fonte de publicação](/assets/images/help/pages/publishing-source-drop-down.png)
{% endif %}
4. Opcionalmente, use o menu suspenso para selecionar uma pasta para sua fonte de publicação. ![Menu suspenso para selecionar uma pasta para a fonte de publicação](/assets/images/help/pages/publishing-source-folder-drop-down.png)
5. Clique em **Salvar**. ![Botão para salvar alterações nas configurações da fonte de publicação](/assets/images/help/pages/publishing-source-save.png)

### Troubleshooting publishing from a branch

{% data reusables.pages.admin-must-push %}

Se você escolher a pasta `docs` em qualquer branch como fonte de publicação e, em seguida, remover a pasta `/docs` desse branch do repositório, seu site não vai criar e você receberá uma mensagem de erro de criação de página para uma pasta `/docs` que está faltando. Para obter informações, consulte [Solucionar problemas de erros de criação do Jekyll para sites do {% data variables.product.prodname_pages %}](/articles/troubleshooting-jekyll-build-errors-for-github-pages-sites#missing-docs-folder)".

{% ifversion build-pages-with-actions %}

O seu sitede {% data variables.product.prodname_pages %} será sempre implantado com a execução de um fluxo de trabalho {% data variables.product.prodname_actions %}, mesmo que você tenha configurado seu site {% data variables.product.prodname_pages %} para ser criado usando uma ferramenta de CI diferente. A maioria dos fluxos de trabalho de CI externos fazem "implantação" no GitHub Pages, fazendo commit da saída da compilação no branch de `gh-pages` do repositório, e normalmente, incluem um arquivo `.nojekyll`. Quando isso acontecer, o fluxo de trabalho de {% data variables.product.prodname_actions %} detectará o estado de que o branch não precisa de uma etapa de criação e seguirá as etapas necessárias para implantar o site em servidores de {% data variables.product.prodname_pages %}.

Para encontrar possíveis erros com a compilação ou implantação, você pode verificar a execução do fluxo de trabalho para o seu site de {% data variables.product.prodname_pages %} revisando a execução do fluxo de trabalho do seu repositório. Para obter mais informações, consulte "[Visualizar histórico de execução de fluxo de trabalho](/actions/monitoring-and-troubleshooting-workflows/viewing-workflow-run-history)". Para obter mais informações sobre como executar novamente o fluxo de trabalho em caso de erro, consulte "[Executar novamente fluxos de trabalho e trabalhos](/actions/managing-workflow-runs/re-running-workflows-and-jobs)".

{% endif %}

{% ifversion pages-custom-workflow %}

## Publishing with a custom {% data variables.product.prodname_actions %} workflow

{% data reusables.pages.pages-custom-workflow-beta %}

To configure your site to publish with {% data variables.product.prodname_actions %}:

{% data reusables.pages.navigate-site-repo %}
{% data reusables.repositories.sidebar-settings %}
{% data reusables.pages.sidebar-pages %}
1. Under "Build and deployment", under "Source", select **GitHub Actions**.
1. {% data variables.product.product_name %} will suggest several starter workflows. If you already have a workflow to publish your site, you can skip this step. Otherwise, choose one of the options to create a {% data variables.product.prodname_actions %} workflow. For more information about creating your custom workflow, see "[Creating a custom {% data variables.product.prodname_actions %} workflow to publish your site](#creating-a-custom-github-actions-workflow-to-publish-your-site)."

   {% data variables.product.prodname_pages %} does not associate a specific workflow to the {% data variables.product.prodname_pages %} settings. However, the {% data variables.product.prodname_pages %} settings will link to the workflow run that most recently deployed your site.

### Creating a custom {% data variables.product.prodname_actions %} workflow to publish your site

For more information about {% data variables.product.prodname_actions %}, see "[Actions](/actions)."

When you configure your site to publish with {% data variables.product.prodname_actions %}, {% data variables.product.product_name %} will suggest starter workflows for common publishing scenarios. The general flow of a workflow is to:

1. Trigger whenever there is a push to the default branch of the repository or whenever a pull request that targets the default branch is opened, reopened, or updated.
1. Use the [`actions/checkout`](https://github.com/actions/checkout) action to check out the repository contents.
1. If required by your site, build any static site files.
1. Use the [`actions/upload-pages-artifact`](https://github.com/actions/upload-pages-artifact) action to upload the static files as an artifact.
1. If the workflow was triggered by a push to the default branch, use the [`actions/deploy-pages`](https://github.com/actions/deploy-pages) action to deploy the artifact. This step is skipped if the workflow was triggered by a pull request.

The starter workflows use a deployment environment called `github-pages`. If your repository does not already include an environment called `github-pages`, the environment will be created automatically. We recommend that you add an environment protection rule so that only the default branch can deploy to this environment. Para obter mais informações, consulte "[Usando ambientes para implantação](/actions/deployment/targeting-different-environments/using-environments-for-deployment)".

{% note %}

**Note**: A `CNAME` file in your repository file does not automatically add or remove a custom domain. Instead, you must configure the custom domain through your repository settings or through the API. For more information, see "[Managing a custom domain for your GitHub Pages site](/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-a-subdomain)" and the [Pages API reference documentation](/rest/pages#update-information-about-a-github-pages-site).

{% endnote %}

### Troubleshooting publishing with a custom {% data variables.product.prodname_actions %} workflow

For information about how to troubleshoot your {% data variables.product.prodname_actions %} workflow, see "[About monitoring and troubleshooting](/actions/monitoring-and-troubleshooting-workflows/about-monitoring-and-troubleshooting)."

{% endif %}