---
description: Blob Storage CDN
icon: diagram-project
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# CDN

{% openapi-operation spec="api-endpoints-en-v2" path="/cdn/usage" method="get" %}
[OpenAPI api-endpoints-en-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-en-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-en-v2" path="/cdn/list" method="get" %}
[OpenAPI api-endpoints-en-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-en-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-en-v2" path="/cdn/file" method="get" %}
[OpenAPI api-endpoints-en-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-en-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-en-v2" path="/cdn/file" method="delete" %}
[OpenAPI api-endpoints-en-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-en-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-en-v2" path="/cdn/upload" method="put" %}
[OpenAPI api-endpoints-en-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-en-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-en-v2" path="/cdn/folder" method="post" %}
[OpenAPI api-endpoints-en-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-en-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-en-v2" path="/cdn/folder" method="delete" %}
[OpenAPI api-endpoints-en-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-en-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-en-v2" path="/cdn/multipart" method="post" %}
[OpenAPI api-endpoints-en-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-en-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-en-v2" path="/cdn/multipart/{uploadId}/parts/{partNumber}" method="put" %}
[OpenAPI api-endpoints-en-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-en-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-en-v2" path="/cdn/multipart/{uploadId}/complete" method="post" %}
[OpenAPI api-endpoints-en-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-en-v2.openapi.yaml)
{% endopenapi-operation %}
