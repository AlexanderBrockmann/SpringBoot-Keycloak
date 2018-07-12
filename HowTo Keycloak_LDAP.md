##HowTo add LDAP to Keycloak

First of all you have to add this code snippet to your application properties:
	
		keycloak.credentials.secret="Secret Key"
		keycloak.use-resource-role-mappings=false
		
---

Then we head to the client you are using for your application. Set the "Access Type" to __confidential__ and press save.

Now there should be a new tab "Credentials". Open the tab and set the "Client Authenticator" to __Client Id and Secret__.

Copy the Key that is displayed next to the button "Regenerate Secret". Now go to your application properties, paste the Key to the keycloak.credentials.secret and replace "Secret Key".

---

Afterwards back to Keycloak. Click on the button "User Federation" in the sidebar. Once you're in the menu for "User Federation", click on the dropdown button "Add provider" and select "ldap".

Choose a fitting name for this ldap, in my case it's "adesso.ldap". Set the priority to 1, "Edit Mode" to "UNSYNCED" and "Vendor" to "Active Directory".

Further add these attributes to the given fields:

		Username LDAP attribute : sAMAccountName
		RDN LDAP attribute : sAMAccountName
		UUID LDAP attribute : objectGUID
		User Object Classes : top,person,organizationalPerson,user
		Connection URL : ldap://ldap01.adesso.de
		Users DN : ou=_users,ou=adesso_deutschland,dc=adesso,dc=local
		Authentication Type : simple
		
Now to "Bind DN" and "Bind Credential". To access the LDAP you'll need a technical user. I'll hand out these informations personally.

Once all this is done, save and restart Keycloak / the dummy app.

---

Now you can try for yourself if you can log in with your adesso credentials.
