
## Testing with State Forecasting and Aggregation vs Scripted testing #

#### Oz
In order to determine the outcome of tests, Oz is designed to use State Forecasting and State Aggregation rather than simple scripting. I know what you're thinking; **That's a nice bunch of fancy words, but what does it actually mean?** Well let's start by describing what's out there already.

#### Scripted Testing
Commonly, behavioral automated testing means describing _in extremely fine detail_ what actions we want to take and what parts of the app we want to validate inside of a very static, pre-scripted test. Where the behavior is scripted is irrelevant regardless of whether it's described in a gherkin-like DSL layer, aggregated into monolithic step definitions, or abstracted into functions inside the codebase. The reason for this is because it is still _scripted_ and that script is _static_. This is great for smaller systems we want to test as it useful for clarity. However, **as soon as the system achieves any moderate level of complexity these static tests become exponentially harder to maintain**. This problem gets worse as time goes on because one change to the system often makes it necessary to change many tests and those tests become increasingly brittle. So how do we get around the brittleness of statically scripted tests?


####State Forcasting and State Aggregation
In short what we mean by _State Forecasting_ is the concept that

Describe what states the application can be in

we will create a _state model_ of what state the application is in using custom classes.

 instead  and then when we want to test we just tell Oz what we want it to get to, and let Oz validate all the parts of the app that we care about once we're in that state.







#### Why Oz uses State Forcasting and Aggregation
So what does that gain for us? The primary reason we use this paradigm is to help with one of our [two main goals](Home-Page), _Keep test maintenance to a minimum_. Remember that maintenance is the your worst enemy when it comes to automated testing.

Story Time:
> This is my story