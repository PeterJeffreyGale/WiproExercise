Test Automation exercise for Wipro Digital

### Building and Executing the Solution

This solution requires Maven & a JDK to be installed and can be built and run with the command:

...>mvn verify

A batch file is provided which can be edited to set the Maven and JDK paths where these are not set in the local PC environment:

...>RunMavenWithTests.bat

The test results can be found at: ...\target\surefire-reports

Alternatively the tests can be run within the IntelliJ IDE, for example.

### Approach

While I am not a very experienced user with Cucumber, I wanted to use this tool as the bases for this exercise, to demonstrate at least a basic level of competence.

* A POM (Page Object Model) approach has been taken, even though the application is a single page application (SPA) - the page objects represent logical sets of functionality.

* I prefer not to use the full PageFactory class available from the Selenium project,
  as I find it is not always suitable for working with dynamic element locators,
  which results in needing multiple locate strategies ("@FindBy" and indivdual getElement() methods)

* I prefer to use specific element getters in all cases, which makes for more consistency.

* While many choose to use ID's for locating elements where they are available,
  as these are deemed to be fasted and least likely to change and cause test failures,
  I feel that they are an implementation choice, not part of the actual application design, and not something real users are aware of.
  So I prefer [dynamic] xpaths which are more flexible and can implicitly test something design aspect of the Design/UI which the user actively relies on interact with the page.
  This approach may cause more test failures, but those test will mostly be due to [planned or unplanned] UI changes which the ID approach will not have flagged.
  In practice, I am happy to adopt the ID approach where the other UI aspects are seen to be adequately covered in other tests.

* I have restricted my page object to using Domain Specific Language (DSL), and making no direct references to the underlying automation tool (Selenium).
  In this way, the automation tool could potentially be quickly replace if a better choice came along or if it needed upgrading, without having to refactor the actual tests implemented.
  Also, this supports the Cucumber/Gherkin style approach of letting non-technical people get involved in writing automated tests in greater detail

* All Selenium based automation code is wrapped in a single "WebBrowser" object so that  simple improvements can be made and applied unuiversally
  (e.g. always putting a wait for elements before executing 'clicks' or other actions on them.)

* I have adopted the approach of executing all tests through a "UsesSession" object.
  This leaves potential for simulating tests where [test] users have multiple user interfaces open at the same time, e.g. front-end web browsers and back-end databases,
  or where there are multiple users/actors involved in a test (e.g. a Customer and a Customer Services agent) where they each have an independent separate web browser session open) at the same time.
  Though feature has not been absolutely necessary here, but makes the setup more readily extensible if it became necessary.

### Desireable Improvements Outstanding

If I had more time, I would like to have:

* Investigatged why the browser opens mutliple times,adnm reduced the need for this (browser closed after each scanario rather than all?)

* Facilitate switching browser type for cross-browser testing

* Implementation of Cucumber's own html base test reports?

* Better reporting and execution logging in the "WebBrowser" object for additional test debugging as necessary.

