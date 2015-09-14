Writing fully integrated tests can be a point of contention testing, especially when it comes to writing [Capybara](https://github.com/jnicklas/capybara) test that need to wait JavaScript to load items. 

Having a Rails API that is powered by some select Angular code can be challenging when items don't load when you need them to. 

This happens occasionally in our test suite, causing some tests to inconsistently fail. My first thought with these failures is to add a line for `sleep 5` in the problem expectations in order to manipulate the test to wait for clickable items to appear on the page.

Rather than continue with this process, I looked to implementing a more elegant solution, but stumbled upon [Rspec::Wait](https://github.com/laserlemon/rspec-wait), which implements a nice `:wait_for` method to replace random expectations.  Adding `:wait_for` methods to sleep is still a bandaid, but at least it makes the intention of the test more clear.
_ _ _

**The Real issue:**

Having multiple expectations within one test Bloc always looks weird to me, they are extremely hard to debug. I find them mostly inexcusable in a unit test, but when for feature test they are necessity to simulate a user flow, for example:

<script src="https://gist.github.com/bdougie/0212e6c39371d9aec969.js"></script>

*Note: There are multiple expectations that are being created only to check for the existence of certain buttons prior to the Capybara `:click`. 

These expectation placements did not seem right and this seemed like an ideal place to implement the [RSpec::Wait](https://github.com/laserlemon/rspec-wait). I went ahead and replaced these expectations with `:wait_for`'s instead but noticed something instead. 

While running the RSpec test repeatedly I was tipped to figuring out there was a bit of expectation debt happening, which was the root issue for the buttons not loading. The backlog of things to do in the test added the button loading slow downs.

While TDDing a feature we tend to add extra expectations to guide us into writing code to match, but after the feature is implemented, the existence of some of these expectations are no longer needed. 

I just deleted a few expectations and notice a instant speed boost (3 second runtime improvement, even with RSpec::Wait adding test time to `:wait_for` items) in the test as well as a clear improvement in the test no longer randomly failing due to buttons not loading in time, thanks to combination of test deletion and `:wait_for`.

<script src="https://gist.github.com/bdougie/7d601484df4e8badfedd.js"></script>

---
So this all got me to ask the question, 

*Do we even need these Capybara test in Rails if we already have unit test coverage and could we replace the Capybara test more with JavaScript Integration test?*

I am in the process of trying out recreating these test in our JavaScript test suite, since JS is the tool causing the hold up and doing all the work in these test.



