# Primary Goal Report

First of all we need to start the Eureka discovery server in order to allow the services to be registered in the server:
```bash
./gradlew :registration:bootRun
```
![Eureka server](https://user-images.githubusercontent.com/72268861/148143306-3de6e867-4b46-49d4-aeb4-60c4044cc393.png)

Once it has been started we run the accounts service (by default it uses the port 2222) with the command:
```bash
./gradlew :accounts:bootRun
```
![Accounts service port 2222](https://user-images.githubusercontent.com/72268861/148143369-1940e109-b89d-4f2c-9abc-64504eca28f5.png)

Then we run this command to start the web service:
```bash
./gradlew :web:bootRun
```
![Web service 3333](https://user-images.githubusercontent.com/72268861/148143408-6fb94e43-8e2b-454c-b65e-4b46645b96ae.png)


After this we check that both services have been registered by the Eureka server by accessing its dashboard.
![Eureka dashboard 1](https://user-images.githubusercontent.com/72268861/148143447-7093f218-8702-4ae6-bd88-a03b08afeb85.png)


Now we are going to run a second instance of the accounts service using the port 4444. In order to do that we need
to change the port that the accounts service uses by modifying its configuration file in 
``/accounts/src/main/resources/application.yml``. Then we we start the new instance with the same command as the first one.
![Accounts service port 4444](https://user-images.githubusercontent.com/72268861/148143495-76e72fc5-8699-422f-b473-5bcbe70e26d6.png)


Then we check the new instance has also been registered by the Eureka server.
![Eureka dashboard 2](https://user-images.githubusercontent.com/72268861/148143523-94969100-6a91-4545-80f0-e999c98dd5ba.png)


The last thing we are going to do is killing the instance of accounts service running in the port 2222 and then do
requests to the web service to see what happens. We can see that after killing the instance it is no longer in the dashboard.
![Eureka dashboard 3](https://user-images.githubusercontent.com/72268861/148143544-8d8f8ff0-7049-4b91-8dab-7577327907e1.png)


After that we will try to fetch the information of an account using the web service
![Web service request](https://user-images.githubusercontent.com/72268861/148143581-6f44aa74-b87a-4040-aa9f-1d330fe2d850.png)


We see that we can succesfully fetch the information. This happens because the web service asks the Eureka server for the
URI ``http://ACCOUNTS-SERVICE`` instead of accessing directly the accounts service. Then, the Eureka server answers with the
real location of an instance of the accounts service, which is the accounts service running in the port 4444.



