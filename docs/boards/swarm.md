# Kudos Boards for Docker Swarm

Basic instructions for deploying Kudos Boards into Docker Swarm for on-premise IBM Connections environments

---

### Pre-Requisites

1. Docker Swarm with Portainer installed. [Guide here](/swarm/)
1. Storage - an accessible MongoDB and S3 object store. [Guide here](/swarm/storage/)
1. SMTP gateway setup for email notifications
1. [Config File](/assets/config/swarm/boards.yml) downloaded
1. Dockerhub account with access to Kudos Boards repository.

   Send your account details to [support@kudosboards.com](mailto:support@kudosboards.com) if you don't already have this.

1. SSL certificate - You will need to use a certificate that covers at least the 2 domains you plan to use, for example Kudos Boards cloud uses the domains `https://kudosboards.com` and `https://api.kudosboards.com`. The certificate should be pem encoded with a separate key file.

---

### Setup OAuth

Kudos Boards currently supports the following oAuth providers for authentication and integration: IBM Connections (on premise), IBM Connections Cloud and Microsoft Office 365.

You will need to setup an OAuth application with one (or more) of these providers for Kudos Boards to function. please refer to the following documentation:

| Provider                     | Registration / Documentation                                                                                  | Callback URL                             |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| IBM Connections (on premise) | [Kudos instructions](/boards/connections/auth-on-prem/)                                                       | `[BOARDS_URL]/auth/connections/callback` |
| Microsoft Office 365         | [Azure app registrations](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) | `[BOARDS_URL]/auth/msgraph/callback`     |
| Google                       | [Google Console](https://console.developers.google.com/apis/credentials)                                      | `[BOARDS_URL]/auth/google/callback`      |
| LinkedIn                     | [LinkedIn](https://www.linkedin.com/developers/apps)                                                          | `[BOARDS_URL]/auth/linkedin/callback`    |
| Facebook                     | [Facebook developer centre](https://developers.facebook.com/apps/2087069981334024/fb-login/settings/)         | `[BOARDS_URL]/auth/facebook/callback`    |

---

### Update config file

**Swarm Variables**:

| Key                               | Description                                                    |
| --------------------------------- | -------------------------------------------------------------- |
| `x-minio-access`                  | Your minio `ACCESS_KEY` as defined in your docker swarm config |
| `x-minio-secret`                  | Your minio `SECRET_KEY` as defined in your docker swarm config |
| `x-app-env.APP_URI`               | Your `[BOARDS_URL]`                                            |
| `services.webfront.deploy.labels` | Update the `traefik.frontend.rule` your `[BOARDS_URL]`         |
| `services.core.deploy.labels`     | Update the `traefik.frontend.rule` with your `[API_URL]`       |

**Boards Variables**:

Follow instructions on [this page](/boards/env/common/)

---

### Deploy

1. Open Portainer and login
1. Select your primary endpoint
1. Choose Stacks from the side menu
1. Click Add Stack
1. Name your stack kudos-boards
1. Browse to your customised config file
1. Click "Deploy the stack"

---

### Update DNS

Update DNS records with a CNAME entry pointing to your swarm URL.

For example:

    kudosboards.com -> swarm.isw.net.au
    api.kudosboards.com -> swarm.isw.net.au

---

### IBM Connections integrations

Please follow these instructions

- [Header](/boards/connections/header-on-prem/)
- [Apps Menu](/boards/connections/apps-menu-on-prem/)
- [Widgets](/boards/connections/widgets-on-prem/)

---

### Advanced

You can also run Kudos Boards with externally hosted mongo database and/or S3 storage.
For assistance with this contact [support@kudosboards.com](mailto:support@kudosboards.com)

---
