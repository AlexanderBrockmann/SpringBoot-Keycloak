##HowTo

The repository [SpringBoot-Keycloak](https://github.com/AlexanderBrockmann/SpringBoot-Keycloak), already contains a dummy app.

The app is generated, with the [Spring Initializr](https://start.spring.io) as a __Maven Project__ with __Java__ and Spring Boot __1.5.15__ . The important part was to add the __Keycloak__ dependencie.

---

Since you already have the dummy app, we'll head straight to how to secure the dummy app with Keycloak.

Disclaimer: The demo app won't work in this state, since it has no login.

Let's open the app in an IDE, go to the application.properties and add:
```java
	keycloak.auth-server-url=http://localhost:8180/auth
	keycloak.realm=demo
	keycloak.resource=keycloakdemo
	keycloak.public-client=true
	
	keycloak.security-constraints[0].authRoles[0]=user
	keycloak.security-constraints[0].securityCollections[0].patterns[0]=/login/*
```

---

Now we'll launch Keycloak. If you havent downloaded it klick [here](https://www.keycloak.org/downloads.html), download the latest version and extract it.

Go to the bin/ directory of Keycloak, open a terminal and execute:

		Linux / Unix:

			$ ./standalone.sh -Djboss.socket.binding.port-offset=100

		Windows:

			> .\standalone.bat -Djboss.socket.binding.port-offset=100
			
---

After the server boots, open your browser and go the
[http://localhost:8180/auth](http://localhost:8180/auth) URL.


Keycloak has no admin account by default. Therefore you have
to create an admin account on the welcome page.


Once you've created an admin account. You can log in to the Admin Console by clicking on the Administration Console link or by using the [http://localhost:8080/auth/admin/](http://localhost:8080/auth/admin/) URL.
Afterwards the Admin Page opens.

---

Now you're in the Master realm. You can now create a new realm. Simply hover over Master and a button "Add Realm" should appear.
The realm should be the same as the realm you defined in application properties.

Afterwards you have to create a __client__ for your application. The sidebar has the button "Clients", simply click on "Clients" and then "Create". For this showcase we fill the field ID with keycloakdemo.

---

Before we create a new user, we have to set a default role for new users. To do this we head to roles, the button can be found in the sidebar. Now we add a role called user. We don't add a description. Afterwards we head back to the main window of roles and click the tab default roles, where we simply add user to realm default roles. Now every new user has the role "user".

---

Furthermore we have to create a new user. Click on "Users" and you'll get to the administration for users.

Create a new user by clicking on the Add user button. Give your new user an appropriate username, first name and last name. Afterwards save and head to the tab "Credentials".

You have to give your new user a password. Although you can decide wether it is temporary or not. If it is temporary the user has to set a new password once he's logged in.

---

Now the login page of the demo app should be secured by Keycloak.

Launch your dummy app and see for yourself.