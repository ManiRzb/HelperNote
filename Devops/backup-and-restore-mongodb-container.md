# MongoDB Backup and Restore Guide

This document provides a comprehensive guide on how to backup and restore a MongoDB database running inside a Docker container. It covers the use of `mongodump` and `mongorestore` tools with authentication enabled.

## Prerequisites

- Docker
- MongoDB Docker container running
- Basic command-line knowledge

## 1. Backup Process Using `mongodump`

`mongodump` is a utility for creating a binary export of the contents of a database. 

### Steps for Backup:

1. **Identify the MongoDB Container:**
   First, identify the name or ID of your MongoDB container. You can list all running containers using:
   ```sh
   docker ps
   ```

2. **Perform the Backup:**
   Use the `docker exec` command to run `mongodump` inside your MongoDB container. Replace `<container_name>` with your container's name or ID, and `<db_name>` with the name of your database. Authentication details (username and password) are also required.
   ```sh
   docker exec <container_name> mongodump --db <db_name> --authenticationDatabase admin -u <username> -p <password> --archive=/tmp/backup/db_backup.gz --gzip
   ```

3. **Copy the Backup File to Host:**
   Once the backup is complete, copy the backup file from the container to your host machine.
   ```sh
   docker cp <container_name>:/data/backup/db_backup.gz ./db_backup.gz
   ```

4. **Verify Backup:**
   Ensure the `db_backup.gz` file is present on your host system and is not corrupted.

## 2. Restore Process Using `mongorestore`

`mongorestore` is a utility for restoring a binary backup created by `mongodump`.

### Steps for Restore:

1. **Copy the Backup File to the Container:**
   If the backup file is not already inside the container, copy it from the host to the container.
   ```sh
   docker cp ./db_backup.gz <container_name>:/data/backup/db_backup.gz
   ```

2. **Restore the Backup:**
   Use `docker exec` to run `mongorestore` inside your container. Replace `<container_name>` with your container's name or ID.
   ```sh
   docker exec <container_name> mongorestore --authenticationDatabase admin -u <username> -p <password> --archive=/data/backup/db_backup.gz --gzip
   ```

3. **Verify Restoration:**
   Connect to your MongoDB instance and verify that the data has been restored correctly.

## Important Notes

- **Authentication:**
  The username and password must have sufficient privileges to perform backup and restore operations.
  
- **Data Consistency:**
  Ensure no write operations are happening during the backup process to maintain data consistency.

- **Backup Schedule:**
  Consider automating backups using cron jobs or similar scheduling tools.

- **Security:**
  Secure your backup files appropriately. They contain sensitive data.

- **Resource Utilization:**
  Be aware that both backup and restore operations can be resource-intensive and might impact the performance of your MongoDB instance.

## Troubleshooting

- If you encounter permission issues, ensure that the Docker container has the correct permissions to access the `/data/backup` directory.
- For any errors related to `mongodump` or `mongorestore`, check the MongoDB documentation for the specific version you are using, as command options might vary.

