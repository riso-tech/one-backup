PostgreSQL Backups with Docker
==============================

.. note:: For brevity it is assumed that you will be running the below commands against local environment, however, this is by no means mandatory so feel free to switch to ``production.yml`` when needed.


Prerequisites
-------------

#. the project was generated with ``use_docker`` set to ``y``;
#. the stack is up and running: ``docker-compose -f local.yml up -d postgres``.


Restoring from the Existing Backup
----------------------------------

To restore from one of the backups you have already got (take the ``backup_2018_03_13T09_05_07.sql.gz`` for example), ::

    $ docker cp ./backups/one.sql.gz $(docker-compose -f local.yml ps -q postgres):/backups

    $ docker-compose -f local.yml exec postgres restore one.sql.gz

You will see something like ::

    Restoring the 'my_project' database from the '/backups/backup_2018_03_13T09_05_07.sql.gz' backup...
    INFO: Dropping the database...
    INFO: Creating a new database...
    INFO: Applying the backup to the new database...
    SET
    SET
    SET
    SET
    SET
     set_config
    ------------

    (1 row)

    SET
    # ...
    ALTER TABLE
    SUCCESS: The 'my_project' database has been restored from the '/backups/backup_2018_03_13T09_05_07.sql.gz' backup.

