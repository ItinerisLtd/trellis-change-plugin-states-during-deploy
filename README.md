# trellis-change-plugin-states-during-deploy

[![GitHub tag](https://img.shields.io/github/tag/ItinerisLtd/trellis-change-plugin-states-during-deploy.svg)](https://github.com/ItinerisLtd/trellis-change-plugin-states-during-deploy/tags)
[![license](https://img.shields.io/github/license/ItinerisLtd/trellis-change-plugin-states-during-deploy.svg)](https://github.com/ItinerisLtd/trellis-change-plugin-states-during-deploy/blob/master/LICENSE)

Change WP plugin activation states when [Trellis](https://github.com/roots/trellis) deploys [Bedrock](https://github.com/roots/bedrock).

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Requirements](#requirements)
- [Installation](#installation)
- [Role Variables](#role-variables)
- [Usage](#usage)
- [FAQs](#faqs)
  - [Why ignore errors?](#why-ignore-errors)
- [Testing](#testing)
  - [Syntax Check](#syntax-check)
- [Author Information](#author-information)
- [Feedback](#feedback)
- [Change log](#change-log)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Requirements

- Trellis [6b40320](https://github.com/roots/trellis/commit/6b403203f9fac49f8c2264c7bf17e0011e70ead4) or later
- Ansible v2.6 or later

## Installation

Add this role to `galaxy.yml`:
```yaml
# galaxy.yml
- src: https://github.com/ItinerisLtd/trellis-change-plugin-states-during-deploy
  version: x.x.x # Check for latest version!
```

Run the command:
```bash
trellis galaxy install

# Alternatively
ansible-galaxy install -r galaxy.yml --force
```

## Role Variables

1. Define the list of `plugins` in an environment:
    ```yaml
    # group_vars/production/wordpress_sites.yml
    wordpress_sites:
      example.com:
        # ...
        plugins:
          activate:
            - bb-plugin
            - searchwp
          deactivate:
            - wordpress-seo
    ```

2. Add this role to the [`deploy_after` hook](https://roots.io/trellis/docs/deploys/#hooks), before any cache related roles:
    ```yaml
    # group_vars/all/deploy-hooks.yml
    # Learn more on https://roots.io/trellis/docs/deploys/#hooks
    deploy_after:
      - "{{ playbook_dir }}/vendor/roles/trellis-change-plugin-states-during-deploy/tasks/main.yml"
      # Cache purging roles must be inserted afterwards, like:
      - "{{ playbook_dir }}/vendor/roles/itinerisltd.trellis_purge_wp_rocket_cache_during_deploy/tasks/main.yml"
    ```

## Usage

[Deploy](https://roots.io/trellis/docs/deploys/#example) as usual. No special action needed.

## FAQs

### Why ignore errors?

Currently, if a listed plugin is not found it will fail the deployment.

## Testing

### Syntax Check

```bash
➜ ansible-playbook -i 'localhost,' --syntax-check tests/test.yml
```

## Author Information

[trellis-change-plugin-states-during-deploy](https://github.com/ItinerisLtd/trellis-change-plugin-states-during-deploy) is a [Itineris Limited](https://www.itineris.co.uk/) project created by [Lee Hanbury-Pickett](https://github.com/codepuncher).

Special thanks to [the Roots team](https://roots.io/about/) whose [Trellis](https://github.com/roots/trellis) make this project possible.

Full list of contributors can be found [here](https://github.com/ItinerisLtd/trellis-change-plugin-states-during-deploy/graphs/contributors).

## Feedback

**Please provide feedback!** We want to make this library useful in as many projects as possible.
Please submit an [issue](https://github.com/ItinerisLtd/trellis-change-plugin-states-during-deploy/issues/new) and point out what you do and don't like, or fork the project and make suggestions.
**No issue is too small.**

## Change log

Please see [CHANGELOG](./CHANGELOG.md) for more information on what has changed recently.

## License

[trellis-change-plugin-states-during-deploy](https://github.com/ItinerisLtd/trellis-change-plugin-states-during-deploy) is released under the [MIT License](https://opensource.org/licenses/MIT).
