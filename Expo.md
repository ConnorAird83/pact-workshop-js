# Infintiy Works Practices Expo

## Pact Broker 
Before we begin, make sure the pact broker is running.
Checkout the starting branch
```
git checkout expo-1
```
and then run the following command
```
docker-compose up -d
```
The pact broker allows the consumer to share it's contracts with the provider. We can take a look at this broker [here](http://localhost:8000) (username/password: pact_workshop/pact_workshop).

## Pact Tests
Let's take a look at how unit tests can fall short and how Pact can bring us value.

1. Run the consumers tests (pact and unit). Notice how all of the tests pass. If we stopped here we may believe we have a working consumer.
```
npm test --prefix consumer
```
2. Now we can take a look at the value Pact gives us. Pact should have created us some [contracts](./consumer/pacts/). We need to publish these contracts to the pact broker so the provider can access them.
```
npm run pact:publish --prefix consumer
```
3. Now we can validate our contracts against the provider.
```
npm run test:pact --prefix provider
```
These tests should have failed. There's something wrong with our Consumer! If we dig into the code we can see that the [Consumer](./consumer/src/api.js) is calling `/products/:id`, whereas the [Provider](./provider/product/product.routes.js) exposes `/product/:id`. Pact has highlighted an issue with our assumptions of the Provider that unit tests alone would never have spotted.

## Working Solution
If you want to see a working version of the Pact tests, checkout branch `expo-2` and run the consumer test, publish the contracts to the broker then validate them on the provider.
```
git checkout expo-2
npm test --prefix consumer
npm run pact:publish --prefix consumer
npm run test:pact --prefix provider
```
