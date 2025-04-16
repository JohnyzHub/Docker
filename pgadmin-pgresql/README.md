This compose file has two services. One for postgresql server and the other one is the pgadmin browser tool to query the db tables.

1. Either git clone this repo or download this specific docker-compose file.

2. From the local directory where the downloaded docker-compose file is located, execute		
	
       > docker-compose up --quiet-pull --build -d
	
    This command pulls the images, creates the network, volumes and containers.
    After successful completion, two services should be up and running.
	
3. Connect pgadmin on browser at localhost:8085

4. Login with email id and password specified for this service, in the yaml file.

5. Get the postgres container id using <b>docker ps</b> command<br>and get the IP address of the postgres container<br> 
      by opening powershell and supply the below command
       
       > docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <postgres-containerid>

6. Connect to postgresql db server:
	
       from lhs right click servers-> register -> server -> postgres-> connect
	   general tab: name - postgres
	   connection tab: host name/address - [postgres container ip from the previous step]
			port-5432
			maintenance database - postgres
			user name - postgres
			pwd  - postgres

7. Open query tool and execute the below commands to query sample db table.

	   CREATE TABLE EMPLOYEE
	    (
		ID serial,
		NAME varchar(100) NOT NULL,
		SALARY numeric(15, 2) NOT NULL,
		PRIMARY KEY (ID)
	     );

	   INSERT INTO EMPLOYEE (NAME, SALARY) VALUES ('JOHNY', 25000);
	   INSERT INTO EMPLOYEE (NAME, SALARY) VALUES ('BASHA', 35000)	;				

	   SELECT * FROM EMPLOYEE;

    If everything works fine, you should be able to see the two entries you inserted.

7. To stop the services, execute command: 

       > docker-compose down

      This stops the services, removes the network and containers created for this compose file.

8. To remove everything that was created as part of this compose file, execute: 
	
       > docker-compose down -v --rmi all

      This removes almost everything that is created for this compose file, including the images.

9. To set the schema name for the query tool run the command '<b>SET search_path TO schema-name</b>'; eg: set search_path TO gtp;
