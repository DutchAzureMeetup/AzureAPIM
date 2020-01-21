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
<br/>![](/images/1.png)
2. Search for API Management 
<br/>![](/images/2.png)
3. Create a new APIM and give it an **unique** name.
- **It's important to choose **Consumption** plan, with the other ones can take 45 min to be created!**
<br/>![](/images/3.png)
1. In the Azure Notification Pane you can see the progress (it will take 5 minutes)
<br/>![](/images/4.png)
5. Go to the created APIM resource
<br/>![Step 1](/images/5.png)
6. Click on APIs and then OpenAPI
<br/>![](/images/6.png)
7. As OpenAPI specification url use: https://petstoreapim.azurewebsites.net/api/v3/openapi.json  
   - set **petstore** as API URL suffix
<br/>![](/images/7.png)
8. The APIs has been imported:
<br/>![](/images/8.png)
9. Click on settings and:
- As Webservice ULR use: https://petstoreapim.azurewebsites.net/api/v3
- Uncheck Subscription Required
- Click on Save 
<br/>![](/images/9.png)
10. Go to the following url:
``` 
https://<<youruniqueapimname>>.azure-api.net/petstore/pet/1
```
where ``<<youruniqueapimname>>`` must be replace with your unique APIM name you gave in step 3.
<br/>

Now you should see the response of the PetStore API exposed through Azure API Management
 <br/>![](/images/10.png)

## Lab 2

One of the best practices when dealing with APIs is to use throttling to eventually limit the number of calls.
In this lab we go to apply a rate limit policy. 

1. Open the API created in Lab1 and click on "All Operations"
 <br/>![](/images/21.png)

2. Click on the ``</>``  icon in the Inbound Processing Pane
 <br/>![](/images/22.png)

3. Replace the whole content with the following and then Save:

    ``` xml
    <policies>
        <inbound>
            <base />
            <rate-limit calls="5" renewal-period="15" />
        </inbound>
        <backend>
            <base />
        </backend>
        <outbound>
            <base />
        </outbound>
        <on-error>
            <base />
        </on-error>
    </policies>
    ``` 
    <br/>![](/images/23.png)

4. Open a browser and request the API from the previous lab:

``` 
https://<<youruniqueapimname>>.azure-api.net/petstore/pet/1
```

Refresh the page multiple times, you will see a message like this: 

<br/>![](/images/24.png)


 ## Lab 3

 Another best practice when dealing with APIs is to identify your consumers (this is different from authentication!).
 In APIM this can be accomplished using subscriptions keys linked to a Product.

1. Go to your PetStore API and in the settings pane enable the checkbox "Subscription Required" and Save.
 <br/>![](/images/31.png)

2. Open a browser and request the API from the previous lab:

    ``` 
    https://<<youruniqueapimname>>.azure-api.net/petstore/pet/1
    ```
    You will see the following: 
    <br/>![](/images/32.png)

3. Let's create a new Product with the PetStore API in it
<br/>![](/images/33.png)
<br/>![](/images/34.png)

4. Let's create a subscription for this product
<br/>![](/images/35.png)
<br/>![](/images/36.png)

5. Get the subscription key
<br/>![](/images/37.png)
<br/>![](/images/38.png)

6. Open a browser and request the API from the previous lab:

    ``` 
    https://<<youruniqueapimname>>.azure-api.net/petstore/pet/1?subscription-key=<<yoursubscriptionkey>>
    ```

Replace ``<<yoursubscriptionkey>>`` with the subscription key you copied.


You will now be able to see again a valid response and Azure API Management is able to identify you!