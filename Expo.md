# Infintiy Works Practices Expo

## Steps:
Before starting these steps make sure the pact broker is running.
Checkout the starting branch
```
git checkout expo-1
```
and then run the following command
```
docker-compose up -d
```
The pact broker allows the consumer to share it's contracts with the provider. We can take a look at this broker [here](http://localhost:8000) (username/password: pact_workshop/pact_workshop).
### Step 1
First of all, let's take a look at how unit tests alone aren't enough.

1. Run the Consumer's unit tests. They should pass, suggesting we have a working consumer.
```
npm test --prefix consumer
```
2. Let's take a look at our app. Spin up the Provider.
```
  npm start --prefix provider
```
3. In a different terminal window, spin up the consumer.
```
  npm start --prefix consumer
```
4. Visit the Consumer UI at [http://localhost:3000](http://localhost:3000). If you select `See more!` you should get an error. This is because we had an incorrect assumption about the providers API.
### Step 2
Now let's add some contract tests and see the value they bring.

5. Checkout the second branch.
```
git checkout expo-2
```
6. Run the Consumer pact tests and publish the contracts to the broker.
```
npm run test:pact --prefix consumer
npm run pact:publish --prefix consumer
```
7. Run the Provider pact tests and we should see some failures. Therefore, Pact would have highlighted this issue for us!
```
npm run test:pact --prefix provider
```
If we take a closer look at the [consumer](consumer/src/api.js) we can see that we get a single product from `/products/:id`. However, looking at the [provider](provider/product/product.routes.js), this should in fact be `/product/:id`.
### Step 3
We can now take a look at the complete solution.

8. Checkout the third branch
```
git checkout expo-3
```
9. Re-run the consumer pact tests and publish the contracts to the pact broker.
```
npm run test:pact --prefix consumer
npm run pact:publish --prefix consumer
```
10. We can then verify these contracts.
```
npm run test:pact --prefix provider
```
11. If you visit the [pact broker](http://localhost:8000) you should be able to see the verified status of the published contract.
