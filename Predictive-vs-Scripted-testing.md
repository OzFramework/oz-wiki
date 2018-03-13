
## Testing with Context Aware Testing vs Scripted testing

#### Oz
In order to determine the outcome of tests, Oz uses Context Awareness rather than static scripting. In this document we will compare the approaches and discuss the reasons why Oz uses this technique to handle tests.


#### Scripted Testing

Commonly, the process for creating behavioral automated testing involves describing _in extremely fine detail_ a list of instructions we want to take which make up the test. These instructions are collected and described either in a gherkin-like DSL layer, aggregated into step definitions, abstracted into functions, or some combination of all three. A highly scripted test might look something like this:

##### Example 1.a
```gherkin
Scenario: Login and add a book to my cart
  Given I am on the login Page
    And I type "test_email@test.com" in the "username" field
    And I type "test_password" in the "password" field
    And I click the "login" button
    And I type "John Doe" into the "Author" field
    And I click "search"
  When I click "First search result"
    And I click the "Add to cart" button
    And I click the "View cart" button
  Then I should see "Book 1 by John Doe" as the "Item 1" text
```

**Example 1.a** shows a very explicit version of what a highly scripted test may look like. In practice a script like this would be considered 'bad form' and would probably look something closer to **Example 1.b**:

##### Example 1.b
```gherkin
#login.feature
Scenario: Login and add a book to my cart
  Given I am logged in
  When I Search for "John Doe"
    And I add the first search result to my cart
  Then I should see the "Book 1 by John Doe" as the "Item 1" text
```
```ruby
#step_definitions.rb
Given /^I am logged in$/ do
  @page.set("username", "test_email@test.com")
  @page.set("password", "test_password")
  @page.click("login")
end

When /^I search for "(.*?)"$/ do
  @page.set("Author", "John Doe")
  @page.click("search")
end

When /^I add the first search result to my cart$/ do
  @page.click("First search result")
  @page.click("Add to cart")
  @page.click("View cart")
end
```

In **Example 1.b** we can see that the instructions have been collected into more descriptive step definitions for re-use. If we look closely however the reality is that these instructions are still _scripted_ and very _static_ regardless of where they are described/implemented. This is great for smaller systems as it useful for clarity. However, **as soon as the system achieves any moderate level of complexity these static tests become exponentially harder to maintain**. This problem gets worse as time goes on because a single change to the AUT often makes it necessary to change many many sets of previously un-related instructions and tests that use those instructions become increasingly brittle as their effects become ever more intertwined. This brittleness turns directly into maintenance effort as features are added and tests start to fail.




#### Context Aware Testing
In short what we mean by _Context Aware Testing_ is the concept that

Describe what states the application can be in

we will create a _state model_ of what state the application is in using custom classes.

 instead  and then when we want to test we just tell Oz what we want it to get to, and let Oz validate all the parts of the app that we care about once we're in that state.






#### Comparing approaches

**Scripted Testing**

- Pros:
    - Simple to implement
    - Easy to explain (especially to business partners)
- Cons:
    - Difficulty to maintain grows exponentially
    - Scripts grow stale and become out dated
    - Doesn't scale
    - Tests are brittle (one change in the app can become many many changes in tests)




#### Why Oz uses Context Aware Testing
So what does that gain for us? The primary reason we use this paradigm is to help with one of our [two main goals](Home-Page), _Keep test maintenance to a minimum_. Remember that maintenance is the your worst enemy when it comes to automated testing.

