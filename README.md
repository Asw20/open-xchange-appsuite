# open-xchange-appsuite
OX App Suite docker image
Online office suite with mail client, calendar, cloud file storage, text and spreadsheet editors.

Note: this image is not intended to be a production-ready solution. For proper configuration instructions refer the official knowledge base.
Building image

Before use you need to build the image.

Docker should be installed and running.

Clone repository:

git clone https://github.com/asw20/open-xchange-appsuite.git
cd docker-ox-app-suite

Build image (with tag ox):

docker build -t open-xchange-appsuite .

Usage

This command launches OX App Suite on port 8085 and mounts /var/www/ox as file storage:

docker run -itd -p 8085:80 -v /var/www/ox:/ox/store ox

You also can mount directory /var/lib/mysql - a directory with MySQL data.

Available environment variables:

    OX_ADMIN_MASTER_LOGIN - system admin login (default oxadminmaster)
    OX_CONFIG_DB_HOST - Database server url or IP address
    OX_CONFIG_DB_NAME - Configuration Database name (default ox7_configdb)
    OX_DB_NAME - Open Xchange Database (default ox7_database) 
    OX_CONFIG_DB_USER - Database user (default openxchange) 
    OX_CONTEXT_ADMIN_LOGIN - context admin login (default oxadmin)
    OX_CONTEXT_ADMIN_EMAIL - context admin email (default admin@example.com)
    OX_CONTEXT_ID - context id (number, default 1)
    OX_SERVER_NAME - server name (default oxserver)
    OX_SERVER_MEMORY - server memory limit (MB, default 1024)
    OX_DB_PORT - Database access port (default 3306)
    OX_DB_PASSWORD - openxchange config Database user password (default db_password)
    OX_ADMIN_PASSWORD - oxadmin password (default admin_password)
    OX_MASTER_PASSWORD - oxadminmaster system admin password (default master_password)
    OX_ROOT_PASSWORD - root Database Root password (default root_password)

Context admin can register new users.

Create new user:

docker exec <container_name> /opt/open-xchange/sbin/createuser \
    -c <context_id> \
    -A <context_admin_login> \
    -P <context_admin_password> \
    -u <new_user_login> \
    -p <new_user_password> \
    -e <new_user_email> \
    -d <display_name> \
    -g <given_name> \
    -s <surname> \
    -l <default language, e.g. ru_RU, optional>

