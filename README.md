<p align="center">
  <img src="https://raw.githubusercontent.com/GoogleCloudPlatform/microservices-demo/master/src/frontend/static/icons/Hipster_HeroLogoCyan.svg" width="300" alt="Online Boutique" />
</p>

**Online Boutique** is a cloud-native microservices demo application.
Online Boutique consists of a 10-tier microservices application. The application is a
web-based e-commerce app where users can browse items,
add them to the cart, and purchase them.

---

## Screenshots
| Home Page | Checkout Screen |
| :--------:| :--------------:|
| ![Home Page](https://github.com/GoogleCloudPlatform/microservices-demo/blob/master/docs/img/online-boutique-frontend-1.png) | ![Checkout](https://github.com/GoogleCloudPlatform/microservices-demo/blob/master/docs/img/online-boutique-frontend-2.png) |

<br>

## Quick Start
1. **Clone this repository.**
2. **Deploy the microservices to the cluster.**

   ```
   kubectl apply -f ./manifests/deployment.yaml
   ```
   
3. **Wait for the pods to be ready.**
   
   ```
   kubectl get pods
   ```
   
   After a few minutes, you should see the pods running:
   
   ```
   NAME                                     READY   STATUS    RESTARTS   AGE
   adservice-76bdd69666-ckc5j               1/1     Running   0          2m58s
   cartservice-66d497c6b7-dp5jr             1/1     Running   0          2m59s
   checkoutservice-666c784bd6-4jd22         1/1     Running   0          3m1s
   currencyservice-5d5d496984-4jmd7         1/1     Running   0          2m59s
   emailservice-667457d9d6-75jcq            1/1     Running   0          3m2s
   loadgenerator-665b5cd444-gwqdq           1/1     Running   0          3m
   paymentservice-68596d6dd6-bf6bv          1/1     Running   0          3m
   productcatalogservice-557d474574-888kr   1/1     Running   0          3m
   recommendationservice-69c56b74d4-7z8r5   1/1     Running   0          3m1s
   redis-cart-5f59546cdd-5jnqf              1/1     Running   0          2m58s
   shippingservice-6ccc89f8fd-v686r         1/1     Running   0          2m58s
   ```
   
4. **Deploy the frontend application and service.**
   
   [online-boutique-frontend](https://github.com/mkryshak/online-boutique-frontend)
   
<br>

## Architecture
**Online Boutique** is composed of 11 microservices written in different
languages that communicate with each other using gRPC. See the [Development Principles](https://github.com/GoogleCloudPlatform/microservices-demo/blob/master/docs/development-principles.md) doc for more information.

![Architecture](https://github.com/GoogleCloudPlatform/microservices-demo/blob/master/docs/img/architecture-diagram.png)

<br>

| Service | Language | Description |
| :------ | :------- | :---------- |
| [adservice](./source/adservice) | Java | Provides text ads based on given context words. |
| [cartservice](./source/cartservice) | C# | Stores the items in the user's shopping cart in Redis and retrieves it. |
| [checkoutservice](./source/checkoutservice) | Go | Retrieves user cart, prepares order and orchestrates the payment, shipping and the email notification. |
| [currencyservice](./source/currencyservice) | Node.js | Converts one money amount to another currency. Uses real values fetched from European Central Bank. It's the highest QPS service. |
| [emailservice](./source/emailservice) | Python | Sends users an order confirmation email (mock). |
| [frontend](https://github.com/deepfence-demo/online-boutique-frontend/tree/master/source) | Go | Exposes an HTTP server to serve the website. Does not require signup/login and generates session IDs for all users automatically. |
| [paymentservice](./source/paymentservice) | Node.js | Charges the given credit card info (mock) with the given amount and returns a transaction ID. |
| [productcatalogservice](./source/productcatalogservice) | Go | Provides the list of products from a JSON file and ability to search products and get individual products. |
| [recommendationservice](./source/recommendationservice) | Python | Recommends other products based on what's given in the cart. |
| [shippingservice](./source/shippingservice) | Go | Gives shipping cost estimates based on the shopping cart. Ships items to the given address (mock) |

## See Also
[microservices-demo](https://github.com/GoogleCloudPlatform/microservices-demo)
