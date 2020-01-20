# AzureAPIM
Labs for the Azure API Management Meetup

## Lab 1

### Create your APIM instance

In this lab we are going to expose our first API using an OpenAPI 3.0 specification.
The APIs we are going to expose are from the Pet Store, for this lab we are hosting this API on an Azure App Service (it's already done, you don't need to create it)

The OpenAPI can be found at: 
https://petstoreapim.azurewebsites.net/api/v3/openapi.json

you will need this URL for the import process.

1. Go to the Azure Portal and create a new resource
<br/>![Step 1](/images/1.png)
2. Search for API Management 
<br/>![Step 1](/images/2.png)
3. Create a new APIM and give it an **unique** name
<br/>![Step 1](/images/3.png)
4. In the Azure Notification Pane you can see the progress (it will take 5 minutes)
<br/>![Step 1](/images/4.png)
5. Go to the crate APIM resource
<br/>![Step 1](/images/5.png)
6. Click on APIs and then OpenAPI
<br/>![Step 1](/images/6.png)
7. As OpenAPI specification url use: https://petstoreapim.azurewebsites.net/api/v3/openapi.json  
   - set **petstore** as API URL suffix
<br/>![Step 1](/images/7.png)
8. The APIs has been imported:
<br/>![Step 1](/images/8.png)
9. Click on settings and:
- As Webservice ULR use: https://petstoreapim.azurewebsites.net/api/v3
- Uncheck Subscription Required
- Click on Save 
<br/>![Step 1](/images/9.png)
10. Go to the following url:
``` 
https://<<youruniqueapimname>>.azure-api.net/petstore/pet/1
```
where ``<<youruniqueapimname>>`` must be replace with your unique APIM name you gave in step 3.
<br/>

Now you should see the response of the PetStore API exposed through Azure API Management
 <br/>![Step 1](/images/10.png)

## Lab 2
