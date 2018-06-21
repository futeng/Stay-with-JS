# Test HTTP API

We relay on API to get or modify data in current age since we separate server code from web project programming. What would you do if your backend partner is not ready to deploy the API for you.

![image-20180621233316869](assets/image-20180621233316869.png)

We can go really far with decoupling like coding base on documentation.

With the definition of data format (such as how to request and what kind of JSON will response). We can easyly create an a proxy to replace the server API. 

![image-20180621234743344](assets/image-20180621234743344.png)

> https://www.mocky.io/ 
>
> Give you : Mock your HTTP responses to test your REST API

It's really cool to give the HTTP mock server by `mocky.io`. 

We could generate our custom response easily. And here is my test response JSON data:

```json
// call http://www.mocky.io/v2/5b2b5a553000006200234590

{"name":"futeng"}
```

