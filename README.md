# Playwright Java Demo

A small end-to-end test automation project built with **Playwright**, **Java**, **JUnit 5**, and **Maven**.

The project demonstrates a structured approach to browser-based automated testing, including the **Page Object Model (POM)**, reusable test components, UI assertions, and automated test execution with **GitHub Actions**.

## Tech Stack

* Java
* Playwright for Java
* JUnit 5
* Maven
* GitHub Actions

## Project Structure

```text
playwright-java-demo/
├── pom.xml
├── README.md
├── .gitignore
├── src/
│   ├── main/java/
│   │   └── pages/
│   │       ├── LoginPage.java
│   │       ├── ProductsPage.java
│   │       └── CartPage.java
│   │
│   └── test/java/
│       └── tests/
│           ├── LoginTest.java
│           ├── ProductTest.java
│           └── CheckoutTest.java
│
└── .github/
    └── workflows/
        └── tests.yml
```

## Test Coverage

The automated tests cover several common end-to-end web application scenarios.

### Authentication

* Successful login
* Invalid login
* Validation of expected login behaviour

### Products

* Product listing
* Product information validation
* Product selection
* Adding products to the shopping cart

### Shopping Cart and Checkout

* Verify products added to the cart
* Validate cart contents
* Remove or update items
* Complete the checkout workflow
* Verify expected checkout result

## Design

The project uses the **Page Object Model** to separate browser interaction logic from test scenarios.

Page classes are located under:

```text
src/main/java/pages/
```

For example:

```java
public class LoginPage {

    private final Page page;

    public LoginPage(Page page) {
        this.page = page;
    }

    public void login(String username, String password) {
        page.getByLabel("Username").fill(username);
        page.getByLabel("Password").fill(password);
        page.getByRole(AriaRole.BUTTON,
                new Page.GetByRoleOptions().setName("Login")).click();
    }
}
```

Tests remain focused on behaviour rather than implementation details:

```java
@Test
void successfulLogin() {
    loginPage.login(username, password);

    assertTrue(productsPage.isDisplayed());
}
```

## Running the Tests

### Prerequisites

* Java 17 or later
* Maven

Clone the repository and install the dependencies:

```bash
git clone <repository-url>
cd playwright-java-demo
mvn clean install
```

Install the Playwright browser binaries if required:

```bash
mvn exec:java \
  -Dexec.mainClass=com.microsoft.playwright.CLI \
  -Dexec.args="install"
```

Run the test suite:

```bash
mvn test
```

## Continuous Integration

The project uses **GitHub Actions** to execute the automated tests on each push and pull request.

The workflow is defined in:

```text
.github/workflows/tests.yml
```

This provides automated validation of the test suite in a clean CI environment.

## Future Improvements

Possible extensions to the project include:

* Cross-browser testing with Chromium, Firefox, and WebKit
* Parameterised and data-driven tests
* API testing alongside UI testing
* Playwright tracing and screenshots on test failure
* Test reporting
* Additional negative and edge-case scenarios
* Parallel test execution
* Environment-based configuration

## Purpose

This repository is a small hands-on project for exploring modern browser automation using **Playwright with Java**.

The emphasis is on maintainable test design, readable automation code, realistic end-to-end scenarios, and integration with a modern CI workflow.
