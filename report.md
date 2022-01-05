# Primary Goal Report

First of all we need to start the Eureka discovery server in order to allow the services to be registered in the server:
```bash
./gradlew :registration:bootRun
```

Once it has been started we run the accounts service (by default it uses the port 2222) with the command:
```bash
./gradlew :accounts:bootRun
```

Then we run this command to start the web service:
```bash
./gradlew :web:bootRun
```

After this we check that both services have been registered by the Eureka server by accessing to its dashboard.


Now we are going to run a second instance of the accounts service using the port 4444. In order to do that we need
to change the port that the accounts service uses by modifying its configuration file in 
``/accounts/src/resources/application,yml``. Then we we start the new instance with the same command as the first one.


Then we check the new instance has also been registered by the Eureka server.

The last thing we are going to do is killing the instance of accounts service running in the port 2222 and then do
requests to the web service to see what happens. We can see that after killing the instance it is no longer in the dashboard.


After that we will try to fetch the information of an account using the web service


We see that we can succesfully fetch the information. This happens because the web service asks the Eureka server for the
URI ``http://ACCOUNTS-SERVICE`` instead of accessing directly the accounts service. Then, the Eureka server answers with the
real location of an instance of the accounts service, which is the accounts service running in the port 4444.



