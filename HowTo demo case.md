##HowTo demo case

First of all i created a dummy app, using the [Spring Initializr](https://start.spring.io).

Generated a __Maven Project__ with __Java__ and Spring Boot __1.5.15__ . The important part was to add the __Keycloak__ dependencie.

---

Since you already have the dummy app, we'll head straight to HowTo secure the dummy app with Keycloak.

First of all you have to go to the application.properties and add:
```java
	keycloak.auth-server-url=http://localhost:8180/auth
	keycloak.realm=demo (or what ever name suits you)
	keycloak.resource=keycloakdemo (choose something fitting)
	keycloak.public-client=true
	
	keycloak.security-constraints[0].authRoles[0]=user
	keycloak.security-constraints[0].securityCollections[0].patterns[0]=/login/*
```

---

Now we'll launch Keycloak. If you havent downloaded it klick [here](https://www.keycloak.org/downloads.html), download the latest version and extract it.

Go to the bin/ directory of Keycloak, open a terminal and execute:

		Linux/Unix:
			$ ./standalone.sh
		
		Windows:
			> .\standalone.bat
			
---

After the server boots, open your browser and go the
[http://localhost:8080/auth](http://localhost:8080/auth) URL.


Keycloak has no admin account by default. Therefore you have
to create an admin account on the welcome page.


Once you've created an admin account. You can log in to the Admin Console by clicking on the Administration Console link or by using the [http://localhost:8080/auth/admin/](http://localhost:8080/auth/admin/) URL.
Afterwards the Admin Page opens.

---

Now you're in the Master realm. You can now create a new realm. Simply hover over Master and a button "Add Realm" should appear.
Name your new __realm__ "demo" (or whatever fits your usecase). In this showcase you already added the realm demo to your application properties.

Afterwards you have to create a __client__ for your application. The sidebar has the button "Clients", simply click on "Clients" and then "Create". Choose whatever name suits your application. For this showcase i chose "keycloakdemo".

---

Furthermore we have to create a new user. Click on "Users" and you'll get to the administration for users.

Create a new user by clicking on the Add user button. Give your new user an appropriate name, i chose testuser. You can altough give him a first and last name. Afterwards save and head to the tab "Credentials".

You have to give you new user an password. Although you can decide wether it is temporary or not. If it is temporary the user has to set a new password once he's logged in.

---

Now that we've completed these steps, we close Keycloak and launch it again:

		Linux / Unix:

			$ ./standalone.sh -Djboss.socket.binding.port-offset=100

		Windows:

			> .\standalone.bat -Djboss.socket.binding.port-offset=100

Now Keycloak has the [http://localhost:8180/](http://localhost:8180/) address.

---

Now the login page of the dummy page should be secured by Keycloak.

Launch your dummy app and see for yourself.