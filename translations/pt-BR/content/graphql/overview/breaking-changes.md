---
title: Alterações significativas
intro: 'Saiba mais sobre as alterações significativas recentes e futuras na API GraphQL {% data variables.product.prodname_dotcom %}.'
redirect_from:
  - /v4/breaking_changes
versions:
  fpt: '*'
  ghec: '*'
  ghes: '*'
  ghae: '*'
topics:
  - API
---

## Sobre alterações significativas

Alterações significativas são quaisquer mudanças que possam exigir ação dos nossos integrantes. Dividimos essas alterações em duas categorias:

- **Significativas:** As alterações que irão modificar as consultas existentes na API do GraphQL. Por exemplo, a eliminação de um campo seria uma mudança decisiva.
- **Perigoso:** Alterações que não modificam as consultas existentes, mas podem afetar o comportamento de tempo de execução dos clientes. Adicionar um valor de enumerador é um exemplo de uma alteração perigosa.

Nós nos esforçamos para fornecer APIs estáveis para os nossos integrantes. Quando um novo recurso ainda está evoluindo, o lançamos atrás de uma [pré-visualização de esquema](/graphql/overview/schema-previews).

Vamos anunciar as próximas mudanças significativas em andamento pelo menos três meses antes de fazer alterações no esquema do GraphQL para dar tempo aos integradores de fazer os ajustes necessários. As alterações entram em vigor no primeiro dia do trimestre (1 de janeiro, 1 de abril, 1 de julho ou 1 de outubro). Por exemplo, se anunciarmos uma mudança no dia 15 de Janeiro, ela entrará em vigor no dia 1 de julho.
