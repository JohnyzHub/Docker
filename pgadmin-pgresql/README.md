This compose file has two services. One for postgresql server and the other one is the pgadmin browser tool to query the db tables.

1. Either git clone this repo or download this specific docker-compose file.

2. From the local directory where the downloaded docker-compose file is located, execute		
	
       > docker-compose up --quiet-pull --build -d
	
    This command pulls the images, creates the network, volumes and containers.
    After successful completion, two services should be up and running.
	
3. Connect pgadmin on browser at 8085 at docker-machine ip address (eg. 192.168.99.100:8085)

4. Login with email id and password specified for this service, in the yaml file.

5. Connect to postgresql db server:
		
       from lhs right click servers-> create -> server -> postgres-> connect
	   general tab: name - postgres
	   connection tab: host name/address - [ip of the docker-machine ie. 192.168.99.100]
			port-5432
			maintenance database - postgres
			user name - postgres
			pwd  - postgres

6. Open query tool and execute the below commands to query sample db table.

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

      <br>This stops the services, removes the network and containers created for this compose file.

8. To remove everything that was created as part of this compose file, execute: 
	
       > docker-compose down -v --rmi all 

      <br>This removes almost everything that is created for this compose file, including the images.
