---
title: Schema previews
intro: "You can preview upcoming features and changes to the {% data variables.product.prodname_dotcom %} GraphQL schema before they are added to the {% data variables.product.prodname_dotcom %} GraphQL API."
redirect_from:
  - /v4/previews
versions:
  fpt: "*"
  ghec: "*"
  ghes: "*"
  ghae: "*"
topics:
  - API
---

## About schema previews

During the preview period, we may change some features based on developer feedback. If we do make changes, we'll announce them on the [developer blog](https://developer.github.com/changes/) without advance notice.

To access a schema preview, you'll need to provide a custom [media type](/rest/overview/media-types) in the `Accept` header for your requests. Feature documentation for each preview specifies which custom media type to provide.

{% note %}

**Note:** The GraphQL schema members under preview cannot be accessed via the Explorer at this time.

{% endnote %}