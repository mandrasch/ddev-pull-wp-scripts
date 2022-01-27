
- Detect if WP-CLI is available on remote server, couldn't get it to work (is more robust than reading values with bash?), snippet for db_pull_command from .ddev/providers/ssh.yaml

```
  # (Alternative approach, deactived by now (not working correctly):
    # Check for WP-CLI first, then fallback to mysqldump
    # 
    # echo "Connect to SSH and check if WP-CLI is available ..."
    # TODO: is there a more robust way? Any unexpected output will cause an error?
    # WP_CLI_AVAILABLE="$(ssh ${sshUser}@${sshHost} "cd ${sshWpPath} && if [[ -x 'command -v wp' ]]; then echo "1"; else echo "0"; fi")"
    # if [ "$WP_CLI_AVAILABLE" = "1" ]; then echo "WP-CLI is available remotely"; else echo "WP-CLI not available remotely, we'll try mysqldump instead"; fi
    #
    # Database dump via WP-CLI 'wp db export':
    # if [ "$WP_CLI_AVAILABLE" = "1" ]; then ssh ${sshUser}@${sshHost} "cd ${sshWpPath} && wp db export | gzip -9 -c" > .ddev/.downloads/db.sql.gz; fi
    #
    # Database dump via mysqldump, db connection is
    # parsed from wp-config.php via bash):
    # if [ "$WP_CLI_AVAILABLE" = "0" ]; then ssh ${sshUser}@${sshHost} "cd ${sshWpPath} && mysqldump --user=\$(cat wp-config.php | grep DB_USER | cut -d \' -f 4) --password=\$(cat wp-config.php | grep DB_PASSWORD | cut -d \' -f 4) --host=\$(cat wp-config.php | grep DB_HOST | cut -d \' -f 4) \$(cat wp-config.php | grep DB_NAME | cut -d \' -f 4) | gzip -9 -c" > .ddev/.downloads/db.sql.gz; fi
    #
    # eo Alternative approach, deactived by now)
```