
## Testing with Context Aware Testing vs Scripted testing

#### Oz
In order to determine the outcome of tests, Oz uses ***Context Awareness*** rather than ***Static Scripting***. In this document we will compare the approaches and discuss the reasons why Oz uses this technique to handle tests.


#### Scripted Testing

Commonly, the process for creating behavioral automated tests involves describing _in extremely fine detail_ a list of instructions which make up the test. These instructions are collected and described either in a gherkin-like DSL layer, aggregated into step definitions, abstracted into functions, or some combination of all three. A highly scripted test might look something like this:

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
  Then I should see "Book 1 by John Doe" as the "Item 1" text
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

In **Example 1.b** we can see that the instructions have been collected into more descriptive step definitions for re-use. If we look closely however the reality is that these instructions are still _scripted_ and very _static_ regardless of where they are described/implemented. This is also usually true of implementation code also, even when an existing framework/pattern is used. Most frameworks or approaches which abstract away details don't deal with the fundamental fact that the test scripts that result are still highly static.

This is great for smaller systems as it useful for clarity. However, **as soon as the system achieves any moderate level of complexity these static tests become exponentially harder to maintain**. This problem gets worse as time goes on because a single change to the AUT often makes it necessary to change many many sets of previously un-related instructions and tests that use those instructions become increasingly brittle as their effects become ever more intertwined. This brittleness turns directly into maintenance effort as features are added and tests start to fail.




#### Context Aware Testing

:construction:



#### Comparing approaches

**Scripted Testing**

:construction:



**Context Aware Testing**

:construction:



#### Why Oz uses Context Aware Testing

:construction:

