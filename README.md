# Azure PostgreSQL Database

## Creating the Database and Private Link:

1. Create an [Azure PostgreSQL Database](https://docs.microsoft.com/en-us/azure/postgresql/quickstart-create-server-database-portal):

1. Create a VNET or use an Existing VNET with a client subnet and a client VM.

1. Create a private endpoint and a private link to access to your Azure PostgreSQL Database from your v-nets client subnet as shown [here](https://docs.microsoft.com/en-us/azure/postgresql/concepts-data-access-and-security-private-link)
If you want you can also deny public network access with [this configuration](https://docs.microsoft.com/en-us/azure/postgresql/howto-deny-public-network-access), from Connection Security under Settings.

1. Login to Client VM.

1. Download SSL Certificates From [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem)
https://docs.microsoft.com/en-us/azure/postgresql/concepts-ssl-connection-security

1. Download and install [pgAdmin](https://www.postgresql.org/ftp/pgadmin/pgadmin4/v5.0/windows/)

1. Click on Add New Server form Quick Links on the home page of pgAdmin app. Here how you should fiill the details has importance
    * In General Tab:
        * Give A name for your server login definition
    * In Connection Tab:
        * Host Name/address: Copy the **Server name** from Essentials Section of your  Azure PostgreSQL Database's overview screen.
        * Username: Copy the **Admin username** from Essentials Section of your  Azure PostgreSQL Database's overview screen.
        * Port:5432 (default port)
        * Meintenance database: postgres
    * In SSL Tab:
        * SSL mode: Select **Verify-Full** from drop-down list.
        * Root certificate: Copy the full path  of the certificate you downloaded on previous steps.

## Testing with data:
Create a dummy table:
```SQL
CREATE TABLE public.somedata(
    thing TEXT NOT NULL,
    tdata  INTEGER,
    tdata2 NUMERIC
); 
```

insert some data:
```SQL
INSERT INTO public.somedata (thing,tdata,tdata2) VALUES('Lovely Day', 1, 1.2);

INSERT INTO public.somedata (thing,tdata,tdata2) VALUES('It is Raining', 12, 25.16);
```
select data:
```SQL
SELECT * FROM public.somedata;
```



Useful Notes:


https://docs.microsoft.com/en-us/azure/postgresql/concepts-connectivity-architecture

https://docs.microsoft.com/en-us/azure/postgresql/concepts-ssl-connection-security

https://docs.microsoft.com/en-us/azure/postgresql/concepts-data-access-and-security-private-link

https://docs.microsoft.com/en-us/azure/postgresql/howto-configure-sign-in-aad-authentication
