# [**kiara**](https://dharpa.org/kiara) plugin: {{ plugin_name }}

This package contains a set of commonly used/useful modules, pipelines, types and metadata schemas for [*kiara*](https://github.com/DHARPA-project/kiara).

## Description

{{ project_short_description }}

## Package content

{% for item_type, item_group in get_context_info().get_all_info().items() %}

### {{ item_type }}
{% for item, details in item_group.item_infos.items() %}
- [`{{ item }}`][kiara_info.{{ item_type }}.{{ item }}]: {{ details.documentation.description }}
{% endfor %}
{% endfor %}

## Links

 - Documentation: [https://{{ github_user }}.github.io/{{ full_project_slug }}](https://{{ github_user }}.github.io/{{ full_project_slug }})
 - Code: [https://github.com/{{ github_user }}/{{ full_project_slug }}](https://github.com/{{ github_user }}/{{ full_project_slug }})
