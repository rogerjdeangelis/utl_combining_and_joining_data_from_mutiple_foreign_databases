# utl_combining_and_joining_data_from_mutiple_foreign_databases
Join a MS Access table of students going on the class trip to a excel table containing age and sex of students.

    ```  Join a MS Access table of students going on the class trip to a excel table containing age and sex of students.                                              ```
    ```  Combining and joining data from mutiple foreign databases                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  related to                                                                                                                                                   ```
    ```  SAS Pass-through SQL - Multiple DBs                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://stackoverflow.com/questions/19255905/sas-pass-through-sql-multiple-dbs                                                                               ```
    ```                                                                                                                                                               ```
    ```  Joe profile                                                                                                                                                  ```
    ```  https://stackoverflow.com/users/1623007/joe                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```  "You can't perform a pass-through query to another pass-through query, unless your two                                                                       ```
    ```  databases are naturally connected in some way that you could take advantage of in the native system."                                                        ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://goo.gl/8mWJGb                                                                                                                                        ```
    ```  https://communities.sas.com/t5/Base-SAS-Programming/Pulling-data-from-different-data-sources/m-p/415493                                                      ```
    ```                                                                                                                                                               ```
    ```  INPUT                                                                                                                                                        ```
    ```  =====                                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```   MS Access Table CLASS_TRIP in access database d:/mdb/class_trip.mdb                                                                                         ```
    ```                                                                                                                                                               ```
    ```     NAME                                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```    Alfred                                                                                                                                                     ```
    ```    Alice                                                                                                                                                      ```
    ```    William                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```   Excel Table of entire class                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```   WORKBOOK d:/xls/class.xlsx with sheet class (you can use [sheet1])                                                                                          ```
    ```                                                                                                                                                               ```
    ```     d:/xls/class.xlsx                                                                                                                                         ```
    ```        +----------------------------------------------------------------+                                                                                     ```
    ```        |     A      |    B       |     C      |    D       |    E       |                                                                                     ```
    ```        +----------------------------------------------------------------+                                                                                     ```
    ```     1  | NAME       |   SEX      |    AGE     |  HEIGHT    |  WEIGHT    |                                                                                     ```
    ```        +------------+------------+------------+------------+------------+                                                                                     ```
    ```     2  | ALFRED     |    M       |    14      |    69      |  112.5     |                                                                                     ```
    ```        +------------+------------+------------+------------+------------+                                                                                     ```
    ```     3  | BARBARA    |    F       |    13      |    58      |  101.5     |                                                                                     ```
    ```        +------------+------------+------------+------------+------------+                                                                                     ```
    ```         ...                                                                                                                                                   ```
    ```        +------------+------------+------------+------------+------------+                                                                                     ```
    ```     20 | WILLIAM    |    M       |    15      |   66.5     |  112       |                                                                                     ```
    ```        +------------+------------+------------+------------+------------+                                                                                     ```
    ```     [CLASS]                                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```  SAS comes with a sample mdb                                                                                                                                  ```
    ```  C:\Program Files\sashome\SASFoundation\9.4\access\sasmisc\demo.mdb                                                                                           ```
    ```  Copy this mdb to d:/mdb/class_trip.mdb                                                                                                                       ```
    ```  Then create the table below in Access                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  PROCESS                                                                                                                                                      ```
    ```  =======                                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```      libname xel "d:/xls/class.xlsx";                                                                                                                         ```
    ```      libname mdb "d:/mdb/class_trip.mdb";                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```      proc sql;                                                                                                                                                ```
    ```        create                                                                                                                                                 ```
    ```          table want as                                                                                                                                        ```
    ```        select                                                                                                                                                 ```
    ```          *                                                                                                                                                    ```
    ```        from                                                                                                                                                   ```
    ```          xel.class                                                                                                                                            ```
    ```        where                                                                                                                                                  ```
    ```          name in ( select name from mdb.class_trip);                                                                                                          ```
    ```                                                                                                                                                               ```
    ```      run;quit;                                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```      libname xel clear;                                                                                                                                       ```
    ```      libname mdb clear;                                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  OUTPUT                                                                                                                                                       ```
    ```  ======                                                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```  WORK.WANT total obs=4                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```       NAME      SEX    AGE    HEIGHT    WEIGHT                                                                                                                ```
    ```                                                                                                                                                               ```
    ```      Alice       F      13     56.5       84.0                                                                                                                ```
    ```      Barbara     F      13     65.3       98.0                                                                                                                ```
    ```      Carol       F      14     62.8      102.5                                                                                                                ```
    ```      William     M      15     66.5      112.0                                                                                                                ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://goo.gl/8mWJGb                                                                                                                                        ```
    ```  https://communities.sas.com/t5/Base-SAS-Programming/Pulling-data-from-different-data-sources/m-p/415493                                                      ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  libname mdb "d:/mdb/class_trip.mdb";                                                                                                                         ```
    ```  data mdb.class_trip;                                                                                                                                         ```
    ```   input name$;                                                                                                                                                ```
    ```  cards4;                                                                                                                                                      ```
    ```  Alfred                                                                                                                                                       ```
    ```  Alice                                                                                                                                                        ```
    ```  William                                                                                                                                                      ```
    ```  ;;;;                                                                                                                                                         ```
    ```  run;quit;                                                                                                                                                    ```
    ```  libname mdb clear;                                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  %utlfkil(d:/mdb/class.xlsx);                                                                                                                                 ```
    ```  libname xel "d:/mdb/class.xlsx";                                                                                                                             ```
    ```  data xel.class;                                                                                                                                              ```
    ```    set sashelp.class;                                                                                                                                         ```
    ```  run;quit;                                                                                                                                                    ```
    ```  libname xel clear;                                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```   Access table MDB.CLASS_TRIP total obs=3                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```     NAME                                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```    Alfred                                                                                                                                                     ```
    ```    Alice                                                                                                                                                      ```
    ```    William                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  libname xel "d:/xls/class.xlsx";                                                                                                                             ```
    ```  libname mdb "d:/mdb/class_trip.mdb";                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  proc sql;                                                                                                                                                    ```
    ```    create                                                                                                                                                     ```
    ```      table want as                                                                                                                                            ```
    ```    select                                                                                                                                                     ```
    ```      *                                                                                                                                                        ```
    ```    from                                                                                                                                                       ```
    ```      xel.class                                                                                                                                                ```
    ```    where                                                                                                                                                      ```
    ```      name in ( select name from mdb.class_trip);                                                                                                              ```
    ```                                                                                                                                                               ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  libname xel clear;                                                                                                                                           ```
    ```  libname mdb clear;                                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  NOTE: Libref XEL was successfully assigned as follows:                                                                                                       ```
    ```        Engine:        EXCEL                                                                                                                                   ```
    ```        Physical Name: d:/xls/class.xlsx                                                                                                                       ```
    ```  510   libname mdb "d:/mdb/class_trip.mdb";                                                                                                                   ```
    ```  NOTE: Libref MDB was successfully assigned as follows:                                                                                                       ```
    ```        Engine:        ACCESS                                                                                                                                  ```
    ```        Physical Name: d:/mdb/class_trip.mdb                                                                                                                   ```
    ```  511   proc sql;                                                                                                                                              ```
    ```  512     create                                                                                                                                               ```
    ```  513       table want as                                                                                                                                      ```
    ```  514     select                                                                                                                                               ```
    ```  515       *                                                                                                                                                  ```
    ```  516     from                                                                                                                                                 ```
    ```  517       xel.class                                                                                                                                          ```
    ```  518     where                                                                                                                                                ```
    ```  519       name in ( select name from mdb.class_trip);                                                                                                        ```
    ```  NOTE: Table WORK.WANT created, with 3 rows and 5 columns.                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  520   run;quit;                                                                                                                                              ```
    ```  NOTE: PROC SQL statements are executed immediately; The RUN statement has no effect.                                                                         ```
    ```  NOTE: PROCEDURE SQL used (Total process time):                                                                                                               ```
    ```        real time           0.01 seconds                                                                                                                       ```
    ```        user cpu time       0.00 seconds                                                                                                                       ```
    ```        system cpu time     0.00 seconds                                                                                                                       ```
    ```        memory              3217.71k                                                                                                                           ```
    ```        OS Memory           17132.00k                                                                                                                          ```
    ```        Timestamp           11/22/2017 11:00:10 AM                                                                                                             ```
    ```        Step Count                        95  Switch Count  0                                                                                                  ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  521   libname xel clear;                                                                                                                                     ```
    ```  NOTE: Libref XEL has been deassigned.                                                                                                                        ```
    ```  522   libname mdb clear;                                                                                                                                     ```
    ```  NOTE: Libref MDB has been deassigned.                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```
