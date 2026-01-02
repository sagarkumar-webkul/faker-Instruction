# faker-Instruction
# Fake Data Handling in Playwright Tests

## Purpose

To ensure **stable, realistic, and reusable test data**, we use a fake
data generation library instead of hard-coded values in Playwright
tests.

This approach helps to: - Avoid data conflicts - Prevent failures due to
reused emails or phone numbers - Reduce manual data cleanup - Make tests
independent and repeatable

------------------------------------------------------------------------

## Recommended Library

### `@faker-js/faker`

This is the **official and actively maintained faker library** for
JavaScript and works seamlessly with Playwright.

------------------------------------------------------------------------

## Installation

``` bash
npm install @faker-js/faker --save-dev
```

------------------------------------------------------------------------

## Basic Usage

``` js
import { faker } from '@faker-js/faker';

const userData = {
  fullName: faker.person.fullName(),
  email: faker.internet.email(),
  phone: faker.phone.number(),
  password: faker.internet.password(10),
};
```

------------------------------------------------------------------------

## Example: Playwright Test Using Fake Data

``` js
import { test, expect } from '@playwright/test';
import { faker } from '@faker-js/faker';

test('Create user with fake data', async ({ page }) => {
  const user = {
    name: faker.person.fullName(),
    email: faker.internet.email(),
    phone: faker.phone.number(),
  };

  await page.goto('/register');
  await page.fill('#name', user.name);
  await page.fill('#email', user.email);
  await page.fill('#phone', user.phone);
  await page.click('button[type="submit"]');

  await expect(page.locator('.success-message')).toBeVisible();
});
```

------------------------------------------------------------------------

## Best Practices

### Do

-   Use faker for emails, phone numbers, names, and addresses
-   Generate fake data inside the test scope
-   Keep faker usage consistent across the test suite

### Do Not

-   Hardcode static values like `test@test.com`
-   Reuse fixed phone numbers across tests
-   Store faker-generated values in environment variables

------------------------------------------------------------------------

## Common Faker Methods (Quick Reference)

``` js
faker.person.fullName();
faker.internet.email();
faker.phone.number();
faker.location.streetAddress();
faker.company.name();
faker.number.int({ min: 1, max: 100 });
faker.internet.password();
```

------------------------------------------------------------------------

## When Not to Use Faker

-   Validating existing demo or production data
-   Testing exact boundary or edge-case values
-   Data migration or backward compatibility scenarios

------------------------------------------------------------------------

## Summary

-   Faker is **mandatory** for generating dynamic test data
-   Reduces flaky tests and data dependency issues
-   Keeps Playwright tests clean, scalable, and maintainable

**All new Playwright automation tests must use `@faker-js/faker` for
fake data generation.**
