# Breaking the Monolith by using hapi 
## Background
Let me get the disclaimer out of the way: I am not an expert on Hapi
I started looking into Hapi's ability to break components out.
This is my attempt to follow other tutorials from a hello world to a true component system.
I have broken this down into the following steps

| Project  | Description | Link |
|---|---|---|
|hapi-tut-monolith-01|A simple hello world hapi project| [01](https://github.com/quapaw/hapi-tut-monolith-01)|
|hapi-tut-monolith-02a|Add services - customers and products| [02A](https://github.com/quapaw/hapi-tut-monolith-02a)|
|hapi-tut-monolith-02b|Adding Glue and externalizing config| [02B](https://github.com/quapaw/hapi-tut-monolith-02b)|
|hapi-tut-monolith-02c|Moving services into their own folders| [02C](https://github.com/quapaw/hapi-tut-monolith-02c)|
|**hapi-tut-monolith-03-main**|**Moved service into own project. Instructions here**|**[03-main](https://github.com/quapaw/hapi-tut-monolith-03-main)**|
|hapi-tut-monolith-03-customer|Just the customer service| [03-customers](https://github.com/quapaw/hapi-tut-monolith-03-customers)|
|hapi-tut-monolith-03-products|Just the produce service| [03-products](https://github.com/quapaw/hapi-tut-monolith-03-products)|
|hapi-tut-monolith-04a-customer|Movement of some files| [04a-customers](https://github.com/quapaw/hapi-tut-monolith-04a-customers)|
|hapi-tut-monolith-04b-customer|New methods| [04b-customers](https://github.com/quapaw/hapi-tut-monolith-04b-customers)|
|hapi-tut-monolith-04c-customer|Validation and Error Handling|[04c-customers](https://github.com/quapaw/hapi-tut-monolith-04c-customers)|
|hapi-tut-monolith-04d-customer|Unit Testing|[04d-customers](https://github.com/quapaw/hapi-tut-monolith-04d-customers)|
|hapi-tut-monolith-04e-customer|Add Mongo and API Doc|[04e-customers](https://github.com/quapaw/hapi-tut-monolith-04e-customers)|
|hapi-tut-monolith-05-customer|Combine work with products for full deployment|[05-customers](https://github.com/quapaw/hapi-tut-monolith-05-customers)|
|hapi-tut-monolith-05-product|Combine work with products for full deployment|[05-products](https://github.com/quapaw/hapi-tut-monolith-05-product)|
|**hapi-tut-monolith-05-main**|**Combine work with products for full deployment**|**[05-main](https://github.com/quapaw/hapi-tut-monolith-05-main)**|
|hapi-tut-monolith-06-customer|Move from npm to yarn|[06-customers](https://github.com/quapaw/hapi-tut-monolith-06-customers)|
|hapi-tut-monolith-07-customer|Customer project to go with 07-main|[07-customers](https://github.com/quapaw/hapi-tut-monolith-07-customers)|
|hapi-tut-monolith-07-product|Product project to go with 07-main|[07-products](https://github.com/quapaw/hapi-tut-monolith-07-products)|
|hapi-tut-monolith-07a-main|Catch up with 06 changes|[07a-main](https://github.com/quapaw/hapi-tut-monolith-07a-main)|
|hapi-tut-monolith-07b-main|Change in configuration|[07b-main](https://github.com/quapaw/hapi-tut-monolith-07b-main)|




#HAPI Tutorial - Monolith - 5 - main
This step updates products api to the same level as the 04a - 04e customers api
So the 05-products api has been update with same change and customers api
The documentation was moved out of the individual services to the main component

# Updates to manifests
* Move from manifest json file to ManifestBuilder.js file
    This creates the manifest json but using code and component json file
    * manifest-plugins\manifest-doc.json
        This has the documentation components and will be added by the builder.
        We also added these components to the package.json by running 
        ```
        npm install vision --save
        npm install inert --save
        npm install hapi-swagger --save
        npm install blipp --save
        ```
    * manifest-plugins\manifest-logging.json
        For logging I am using the good plug-in (https://github.com/hapijs/good)
        ```
        npm install good --save
        npm install good-console --save
        npm install good-file --save
        npm install good-squeeze --save
        ```
    * Add hapi-mongodb to ManifestBuilder.js
    
## Start the server
run ```node index.js``` to start
You should see the following on startup
```
http://localhost:3000 [http]
  GET    /                              
  GET    /{name}                        
  GET    /customers                     
  POST   /customers                     
  GET    /customers/{id}                
  GET    /documentation                 
  GET    /products                      
  POST   /products                      
  GET    /products/{id}                 
  GET    /swagger.json                  
  GET    /swaggerui/{path*}             
  GET    /swaggerui/extend.js 
```
    
###Test the services
* Go to the following link [http://localhost:3000/customers](http://localhost:3000/customers)
* Go to the following link [http://localhost:3000/products](http://localhost:3000/products)

