# Drupal Drush Deployment

This Quicksilver project contains scripts that can be used
to deploy a Drupal site using Drush. A proper Drupal update
via Drush consists of the following steps:

1. Database updates
2. Sync configuration
3. Sync configuration (yes this is intentionally repeated)
4. Rebuild caches
5. Run deploy hooks

We think it's best to include these steps for the `sync_code`
and `deploy` Quicksilver hooks.

## Usage

```yaml
api_version: 1

workflows:
  sync_code:
    after:
      -
        type: webphp
        description: 'Rebuild cache'
        script: private/scripts/drush_deploy_hooks/cache_rebuild.php
      -
        type: webphp
        description: 'Execute database updates'
        script: private/scripts/drush_deploy_hooks/database_updates.php
      -
        type: webphp
        description: 'Import configuration'
        script: private/scripts/drush_deploy_hooks/drush_config_import.php
      -
        type: webphp
        description: 'Import configuration'
        script: private/scripts/drush_deploy_hooks/drush_config_import.php
      -
        type: webphp
        description: 'Run Drush deploy hooks'
        script: private/scripts/drush_deploy_hooks/drush_deploy_hook.php
  deploy:
    after:
      -
        type: webphp
        description: 'Rebuild cache'
        script: private/scripts/drush_deploy_hooks/cache_rebuild.php
      -
        type: webphp
        description: 'Execute database updates'
        script: private/scripts/drush_deploy_hooks/database_updates.php
      -
        type: webphp
        description: 'Import configuration'
        script: private/scripts/drush_deploy_hooks/drush_config_import.php
      -
        type: webphp
        description: 'Import configuration'
        script: private/scripts/drush_deploy_hooks/drush_config_import.php
      -
        type: webphp
        description: 'Run Drush deploy hooks'
        script: private/scripts/drush_deploy_hooks/drush_deploy_hook.php
```

!!! note

    Instead of `drush deploy` we instead break out each step
    into its own script. This is because Quicksilver webhooks
    timeout after 2 minutes. Instead of giving the entire
    `drush deploy` command 2 minutes total to complete, each
    step is given 2 minutes to complete (for a maximum run
    time of 10 minutes).
