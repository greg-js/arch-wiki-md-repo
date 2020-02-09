<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Migrating to a Single Sign On infrastructure](#Migrating_to_a_Single_Sign_On_infrastructure)
    *   [1.1 Proposal](#Proposal)
    *   [1.2 Services](#Services)
    *   [1.3 Questions](#Questions)
    *   [1.4 Migration for large user databases](#Migration_for_large_user_databases)

## Migrating to a Single Sign On infrastructure

Currently users have to register at every webservice we have, this sucks. The idea is to move to a single source of truth for our user management.

### Proposal

Move to Keycloak as identity and user management

### Services

| Service | SAML | OpenID-connect | Alternative | Allowed | Alternative |
| Grafana | [supported](https://grafana.com/docs/grafana/latest/auth/saml/) | Devops |
| BBS | not supported | not supported | All |
| Zabbix | [bug report](https://support.zabbix.com/browse/ZBXNEXT-3320) | Devops |
| Mediawiki | [extension](https://www.mediawiki.org/wiki/Extension:SimpleSAMLphp) | All |
| AUR | not supported | not supported | All, with special status |
| Patchwork | [django plugin?](https://github.com/fangli/django-saml2-auth) | [django openid plugin](https://github.com/mozilla/mozilla-django-oidc) | gitlab | Staff |
| Archweb | [django plugin?](https://github.com/fangli/django-saml2-auth) | [django openid plugin](https://github.com/mozilla/mozilla-django-oidc) | Staff |
| Mailman | [bug report](https://gitlab.com/mailman/hyperkitty/issues/90) | All |
| Kanboard | [reverse proxy](https://docs.kanboard.org/en/latest/admin_guide/reverse_proxy_authentication.html?highlight=sso) | Staff | Gitlab |
| Gitlab | [supported](https://docs.gitlab.com/ee/user/group/saml_sso/scim_setup.html#gitlab-configuration) | All |
| Matrix | [blog article](https://edenmal.moe/post/2019/Matrix-Synapse-SAML2-Login/) | Staff |
| Quassel | not supported? | not supported | Staff | A lot |
| Email (dovecot) => unix user | pam script?? | Staff |
| SSH/unix users | pam script? | Staff |

### Questions

*   How to handle existing users from services?
*   How do we provision our own users?

### Migration for large user databases

*   AUR has required emails, but no concept of verified email. We need users to verify their email on the AUR to have a reliable datapoint to merge with.
    *   => Implement email verification.
*   BBS has required, verified emails.
*   Mailman obviously requires verified emails.
*   Wiki:
    *   email verification is required for editing via `$wgEmailConfirmToEdit` [[1]](https://git.archlinux.org/vhosts/wiki.archlinux.org.git/tree/LocalSettings.archlinux.org.php#n230)
    *   coordinate potential changes to the wiki settings and user notifications with the [wiki administrators](/index.php/ArchWiki_talk:Maintenance_Team "ArchWiki talk:Maintenance Team")