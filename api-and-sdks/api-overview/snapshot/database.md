---
icon: database
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

# Banco de Dados

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/presets" method="get" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/presets/random-names" method="get" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database" method="get" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database" method="post" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/{dbID}" method="get" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/{dbID}" method="delete" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/{dbID}" method="patch" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/{dbID}/start" method="put" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/{dbID}/stop" method="put" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/{dbID}/restart" method="put" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/{dbID}/backup" method="post" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/{dbID}/backups" method="get" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/{dbID}/backups/{backupId}/download" method="get" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/{dbID}/restore" method="post" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/{dbID}/logs" method="get" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="api-endpoints-pt-v2" path="/database/{dbID}/logs" method="delete" %}
[OpenAPI api-endpoints-pt-v2](https://raw.githubusercontent.com/discloud/apidoc/refs/heads/main/api-endpoints-pt-v2.openapi.yaml)
{% endopenapi-operation %}
