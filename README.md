# AngularJest

Angular project configured with Jest, to compare the configuration and performance between Jest and Karma.

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 1.4.7.

## Configuring Jest

Setting up [Jest](http://facebook.github.io/jest/) is pretty easy to do in an Angular CLI project! Following these steps should get you up and running:

### 1. Installing npm dev packages
First install the required dependencies:
```bash
npm install -D jest jest-preset-angular @types/jest
```
Or with [Yarn](https://yarnpkg.com/lang/en/):
```bash
yarn add --dev jest jest-preset-angular @types/jest
```
### 2. Jest directory
Create a jest directory in your root folder. This directory will contain 2 files, a `jest.main.ts` file to load in the dependencies for Jest and a `jest.global-mocks.ts` for, you've guessed it, global mocks.

`jest.main.ts`
```javascript
import 'jest-preset-angular';
import './jest.global-mocks';
```
`jest.global-mocks.ts`
```javascript
const mock = () => {
    let storage = {};
    return {
        getItem: key => key in storage ? storage[key] : null,
        setItem: (key, value) => storage[key] = value || '',
        removeItem: key => delete storage[key],
        clear: () => storage = {},
    };
};

Object.defineProperty(window, 'localStorage', { value: mock() });
Object.defineProperty(window, 'sessionStorage', { value: mock() });
Object.defineProperty(window, 'getComputedStyle', {
    value: () => ['-webkit-appearance']
});
```


### 3. Configuring Jest
Now that we've got all the required files, it's time to configure Jest! Go to your `package.json` file and add the following Jest configuration to it:

`package.json`
```json
{

    // name, version, dependencies,...

    "jest": {
        "preset": "jest-preset-angular",
        "setupTestFrameworkScriptFile": "<rootDir>/jest/jest.main.ts",
        "coverageReporters": ["lcov"],
        "coveragePathIgnorePatterns": ["<rootDir>/node_modules/", "<rootDir>/jest/.*\\.(ts)$", "<rootDir>/src/app/.*\\.(html)$"]
    }
}
```
We'll load in a preset configuration for Jest combined with Angular, indicate where our setupTestFrameworkScriptFile is located and configure the coverageReporters with some paths it should ignore. While we're at the package.json file, it's safe to remove the `@types/jasmine` dependency, as `@types/jest` is taking care of those types now.

Want to configure Jest even further? Take a look at the [Configuring Jest](http://facebook.github.io/jest/docs/en/configuration.html#content) documentation for more options.

### 4. npm scripts
Phew, that should be it for now. Let's define some npm scripts which will trigger our tests to run with Jest.
`package.json`
```json
{
    "scripts": {
        // Other scripts...

        "jest": "jest --notify",
        "jest:watch": "jest --watch",
        "jest:coverage": "jest --coverage",
    }
}
```
We've got a script to run the test just once, another one to enable watch mode and the last one to generate a coverage report after the tests have been run. Once you're convinced with Jest, you can replace the name of the scripts with `test` instead of `jest`. :wink:

### 4. Run your Jest powered tests
Run one of the npm scripts and witness how fast your tests are being run with Jest!

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `-prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running unit tests with Jest

Run `ng jest` to execute the unit tests via [Jest](http://facebook.github.io/jest/).

Run `ng jest:watch` to enable watch mode.

Run `ng jest:coverage` to generate coverage reports.

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).
