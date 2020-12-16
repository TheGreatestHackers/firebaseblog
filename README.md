# Fireangularblog 
## By James Dumitru

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 11.0.4.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

If you need the node modules, make sure to Run `npm install` and if need be, change error of deprecated @angularfire2 to @angular/fire. 
I had to deal with a deprecated import for firebase. 

- If you are running into node modules errors, as I've seen dealing with `firebase.app.module.d.ts` or `interfaces.d.ts` or `database.d.ts` you must Run `ng add @angular/fire` correctly instead of what npm does by default and uninstall firebase and run that command. The imports are wacky but it should fix the issue.

IF you see firebase/app as an issue, I assure you it's not and is something vs code won't pickup. 

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.
