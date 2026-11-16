# Azure WordPress

## Description

Wordpress 7.1.4 with Redis 6.0.8 and MariaDB 12.3. Designed for Azure App service or Azure Container apps.

Custom Image forked from [Azure wordpress multicontainer docker image](https://github.com/Azure-Samples/multicontainerwordpress)

Features:

- Retains Redis cache
- Removed cert settings for MYSQL

Tested with Azure app service and Azure container apps (if you want persistent db/wpress files).
