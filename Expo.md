# Infintiy Works Practices Expo

## Steps:
1. Run the consumers unit tests (Should pass!)
2. Spin up the Consumer and provider and see the failure when looking at a single product
    - This is because we had an incorrect assumption about the providers API.
3. Run Consumer pact tests (Should pass!)
4. Run the Provider tests (Should fail!)
    -  This shows that Pact would have helped us find this issue.
5. Fix the consumer and rerun the pact tests (Should pass!)
6. Move to second branch with new pact test that needs a state.
7. run consumer tests which pass but fail on provider
8. Fix provider tests (add state)
9. Look at the broker.

## What do I need to do?
- Create a starting branch with...
  - passing consumer unit and pact tests.
  - Failing provider tests.
  - Missing one tests which uses a state (do not include this state in the provider).
- Create a second branch with...
  - the same, but fixed, consumer and provider tests as the starting branch.
  - an additional consumer test which requires a state missing from the provider.
- Create a third branch with the full solution.

