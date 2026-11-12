# Azure WordPress

## Description

Wordpress 6.5.5. Designed for Azure App service or Azure Container apps with Redis and MariaDB

Custom Image forked from [Azure wordpress multicontainer docker image](https://github.com/Azure-Samples/multicontainerwordpress) 

Features:
- Updated to PHP 8.2 / Wordpress 6.5.5
- Retains Redis cache
- Removed cert settings for MYSQL

Tested with Azure app service and Azure container apps (if you want persistent db/wpress files) with MariaDB 11.2.5

 