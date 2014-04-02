lda-examples
============

This project contains several examples &amp; tutorials for Linked Data for Applications (LDA).

`
Note: if you don't have python 2.7, you need to install it before proceeding.
`

Before attempting to run any of the examples, if you haven't already done so, 
bring up a virtual machine with Nginx and MongoDB in it:

```sh
cd lda-examples
vagrant up
```

The first time you do this it might take minute or two. Subsequent times should be around 15 seconds.

Todo Sample
-----------

This is an example of an LDA-based 'todo list' application. To run the application proceed as follows:

1. cd into the todo directory:
```sh
cd lda-examples/todo
```

2. Get the python libraries you need (only needs to be run once):
```sh
python setup.py install
```

3. Run the todo server:
```sh
./run.sh (or equivalent for your OS)
```
You should see the message "todo initiated on host: localhost port: 3007".

At this point, you can point your browser at http://localhost:3007/items where you should see a very
simple UI that allows you to add and view items on a todo list.

Setupshop Sample
----------------

This example demonstrates a multi-tenant hoster managing a hosted site called 'CloudSupplements' - an online store of vitamins and health products.
Setupshop can be run in different configurations, but here we document what you need to do to run it in a local development configuration.

This application uses services provided by the [lda-siteserver](https://github.com/ld4apps/lda-siteserver) component of LDA. Before attempting to run this example, make sure the siteserver application is running by following the instructions [shown here](https://github.com/ld4apps/lda-siteserver/blob/master/README.md). Make sure you've added the following line in your
/etc/hosts (C:\Windows\System32\Drivers\etc\hosts on Windows) file:

```sh
127.0.0.1 cloudsupplements.localhost
```

Once the siteserver application is running and your /etc/hosts file is properly configured, proceed as follows:

1. cd into the setupshop directory:
```sh
cd lda-examples/setupshop
```

2. Get the python libraries you need (only needs to be run once):
```sh
python setup.py install
```

3. Run the setupshop server:
```sh
./run.sh (or equivalent for your OS)
```
You should see the message "test setupshop initiated on host: localhost port: 3006".

4. Create the test data:
```sh
cd test
./setupshop_test_data_create.sh
```
If successful, you should see a number of POST messages on the console that look something like this:
```sh
######## POSTed resource: http://localhost:3001/ac/13.1, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/ac/13.2, status: 201
######## POSTed resource: http://localhost:3001/ac/13.3, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/ac/13.4, status: 201
######## POSTed resource: http://localhost:3001/mt/13.5, status: 201
######## POSTed resource: http://localhost:3001/mt/13.6, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.2, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.3, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.4, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.5, status: 201
######## POSTed resource: http://localhost:3001/mt/cloudsupplements, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.6, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.7, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.8, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.9, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.10, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.11, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.12, status: 201
...
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.60, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.61, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.62, status: 201
######## POSTed resource: http://cloudsupplements.localhost:3001/cat/12.63, status: 201
Done.
```

At this point, you can point your browser at http://localhost:3001/ where you will initially see no existing sites. 

If you log in as **admin/admin**, the cloudsupplements site will appear. 
You can explore the cloudsupplements site and you can link from there to the store at http://cloudsupplements.localhost:3001/. You can also create new sites and you can add new improvements (instances of capabilities) to them. Your choice of capabilities is currently limited to shop and blog so your improvements need to be of those types. You can create a new shop, but there is not enough implemented yet to let you completely define your catalog, prices, taxes etc., through the UI. Blogging is even more embryonic.

You can also create a new account (register) and log in. You use the same account to create new sites that you use to shop at an existing site - accounts are not specific to a particular capability.
