# Kong APIs to Services and Routes Migration

Simple script to convert all Kong v0.14.1 APIs (and their plugins) to Services and Routes.

# Motivation

APIs have been removed in Kong v1.0.x in order to upgrade from v0.14.1 you need to re-create all your APIs as Services and Routes. This script migrates each API into one Service and one Route. It might not be the best way but it works. Kong suggests if two Services have the same upstream-url they should be merged into one Service with multiple Routes (common plugins enabled on the Service, specific plugins only enabled on Routes). You can still merge similar Services into one after you have run my migration script.

# Prerequisites
* Kong upgraded to v0.14.1 (the only version I have tested against)
* Python 3, os and requests modules
* Access to Kong's Admin API
* Fresh backups of your Kong

# Warning
* The script doesn't stop on failures, it can mess up you configuration, so test first.
* All plugins which were assigned to an API will be assigned to the new Service, if you have custom plugins which can only be used with Routes you will need to manually migrate these first.

# Dry Run
```
export KONG_URL=http://127.0.0.1:8001 # Your Kong's admin api url and port
./kong-migrate-apis.py
```

# Real Run
```
export KONG_URL=http://127.0.0.1:8001 # Your Kong's admin api url and port
export KONG_MIGRATE=True
./kong-migrate-apis.py
```
The script actually migrates only first 1000 APIs, if you have more run the script again.
