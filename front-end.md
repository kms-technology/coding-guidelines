# KMS Front-end Coding Guidelines

- [1. Introduction](#1-introduction)
- [2. Coding Styles](#2-coding-styles)
    - [2.1. HTML](#21-html)
    - [2.2. CSS](#22-css)
    - [2.3. JavaScript](#23-javascript)
    - [2.4. AngularJS](#24-angularjs)
    - [2.5. Angular](#25-angular)
    - [2.6. React](#26-react)
- [3. Boilerplate Code](#3-boilerplate-code)
    - [3.1. Angular](#31-angular)
    - [3.2. React](#32-react)
- [4. Testing](#4-testing)
    - [4.1. Unit-Testing](#41-unit-testing)
    - [4.2. End-to-End Testing](#42-end-to-end-testing)
- [5. Best Practices](#5-best-practices)
    - [5.1. HTML, CSS and JavaScript](#51-html-css-and-javascript)
    - [5.2. CSS Framework](#52-css-framework)
    - [5.3. CSS Methodologies](#53-css-methodologies)
    - [5.4. styled-components](#54-styled-components)
    - [5.5. Accessibility](#55-accessibility)
    - [5.6. Code Analysis Tools](#56-code-analysis-tools)
    - [5.7. Project Management Tools](#57-project-management-tools)
- [6. Checklist](#6-checklist)
- [7. Resources & References](#7-resources--references)
    - [7.1. Resources](#71-resources)
    - [7.2. References](#72-references)

## 1. Introduction

This document describes a collection of standards, conventions, and guidelines for writing solid Front-end code, especially, JavaScript code. They are based on sound, proven software engineering principles that lead to code that is easy to understand, to maintain, and to enhance. Furthermore, code conventions are important to programmers for a number of reasons: 

* 80% of the lifetime cost of a piece of software goes to maintenance.
* Hardly any software is maintained for its whole life by the original author.
* Code conventions improve the readability of the software, allowing engineers to understand new code more quickly and thoroughly, making teams of developers significantly more productive
* If you ship your source code as a product, you need to make sure it is as well packaged and clean as any other product you create.

The naming conventions, guidelines and best practices described in this document are compiled from KMS developers own experiences and by referring to popular community guidelines.

## 2. Coding Styles

### 2.1. HTML

KMS refers to write HTML code following coding guidelines and best practices defined by well-known community [hail2u](https://github.com/hail2u/html-best-practices.

The guidelines are crafted for developers who want to take their markup further, making it leaner and more semantically rich. It also provides and demonstrates all general HTML tags, explains where and how to use them.

**Full Documentation:** https://github.com/hail2u/html-best-practices/blob/master/README.md

### 2.2. CSS

KMS refers to write CSS or Sass code following style guide defined by well-known community [Airbnb](https://github.com/airbnb/css).

The guideline provides best practices to format, comment on a CSS content. As an important section, the guidelines introduce and encourage developers to apply CSS methodologies as OOCSS and BEM to the front-end project.

Regarding Sass, the guideline offers the correct ways to use Sass syntax, the ordering of property declarations, naming conventions for variables, usage of mixins, @extend directive, nested selectors…

**Full Documentation:** https://github.com/airbnb/css/blob/master/README.md

### 2.3. JavaScript

KMS refers to write CSS or Sass code following style guide defined by well-known community [Airbnb](https://github.com/airbnb/javascript).

The guideline provides all best practices of use JavaScript types, variables, references, objects, functions, hoisting… also coding conventions for blocks, comments, naming.

KMS encourages to use ECMAScript 6 and Beyond syntax and features. The guideline provides detail best practices to use arrow functions, classes, modules, generators, properties…

As an important thing about JavaScript performance, the guideline points out cases of uses that may impact the performance and suggestions to avoid the issues. 

**Full Documentation:** https://github.com/airbnb/javascript/blob/master/README.md

### 2.4. AngularJS

KMS refers to develop an AngularJS (1.x) application using ES5 or ES6+ by folloiwing the popular style guide provided/maintained by [John Papa](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md)

**Full Documentation:** https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md

### 2.5. Angular

KMS refers to develop an Angular (2+) application using TypeScript by following the style guide provided by the official [Angular](https://angular.io/docs/ts/latest/guide/style-guide.html) website.

Angular Style Guide presents fully conventions and, as importantly, it explains why to do that.

**Full Documentation:** https://angular.io/docs/ts/latest/guide/style-guide.html

### 2.6. React

KMS refers to follow React and JSX Style Guide defined by well-known community [Airbnb](https://github.com/airbnb/javascript).

As an enhancement of JavaScript coding guideline, the document explains all bad/good usages of React declaration, props, refs, tags, class, mixins. Also, it presents coding conventions and best practices to use naming, alignment, quotes, parentheses, ordering…

**Full Documentation:** https://github.com/airbnb/javascript/blob/master/react/README.md

## 3. Boilerplate Code

By using a Front-end framework, it requires preparing a lot of things: package management tool, configuration files, initial source code, unit-test, integration-test, code coverage tool, code styling checking... It is highly recommended to create new front-end project based on pre-defined skeleton code, or boilerplate code.

### 3.1. Angular

KMS refers to use Angular with Webpack. We refer to use the seed repo developed by [Preboot](https://github.com/preboot/angular2-webpack). This seed repo serves:

* Best practices in file and application organization for [Angular 2](https://angular.io/).
* Ready to go build system using [Webpack](https://webpack.github.io/docs/) for working with [TypeScript](http://www.typescriptlang.org/).
* Testing Angular 2 code with [Jasmine](http://jasmine.github.io/) and [Karma](http://karma-runner.github.io/).
* Coverage with [Istanbul](https://github.com/gotwarlost/istanbul).
* End-to-end Angular 2 code using [Protractor](https://angular.github.io/protractor/).
* Stylesheets with [Sass](http://sass-lang.com/) (not required, it supports regular css too).
* Error reported with [TSLint](http://palantir.github.io/tslint/) and [Codelyzer](https://github.com/mgechev/codelyzer).
* Documentation with [TypeDoc](http://typedoc.org/).

**Code Repository:** https://github.com/preboot/angular2-webpack

### 3.2. React

KMS refers to use React with Redux for highly scalability, application state management. We refer to use the boilerplace code provided by [React Boilerplate](https://github.com/react-boilerplate/react-boilerplate). This boilerplace repo help us to start new React project quickly as a highly scalable, offline-first foundation with the best developer experience and a focus on performance and best practices. It's features:

* Quick scaffolding
  - Create components, containers, routes, selectors and sagas - and their tests - right from the CLI.
* Instant feedback
  - Enjoy the best DX (Developer eXperience) and code your app at the speed of thought.
* Predictable state management
* Next generation JavaScript
  - Use template strings, object destructuring, arrow functions, JSX syntax and more, today.
* Next generation CSS
* Industry-standard routing
* Industry-standard i18n internationalization support
* Offline-first
  - The next frontier in performant web apps: availability without a network connection from the instant your users load the app.
* SEO
* And more...

**Code Repository:** https://github.com/react-boilerplate/react-boilerplate

## 4. Testing

### 4.1. Unit-Testing

JavaScript is a dynamically typed language which comes with the great power of expression, but it also comes with almost no help from the compiler. For this reason, it is strongly required the code written in JavaScript needs to come with a strong set of tests.

[Jasmine](https://jasmine.github.io/) and [Mocha](https://mochajs.org/) are the most popular JavaScript unit testing frameworks. Jasmine is mainly paired with Angular, while Mocha with React.

It is recommended to goal over 70% of code coverage and [Istanbul](https://github.com/gotwarlost/istanbul) is a good tool to metric the coverage.

### 4.2. End-to-End Testing

Unit tests are the first line of defense for catching bugs, but sometimes issues come up with integration between components which can't be captured in a unit test. End-to-end tests are made to find these problems. 

[Protractor](http://www.protractortest.org/) is recommended to use in Angular projects while [WebdriverIO](http://webdriver.io/) should be a good choice for React applications.

## 5. Best Practices

### 5.1. HTML, CSS and JavaScript
- Use a CSS reset
- Don't mix CSS with HTML
- Don't mix JavaScript with HTML
- Place CSS files in the <head>
- Place JavaScript file at the bottom
- Use HTML symantically
- Minified CSS/JS

### 5.2. CSS Framework

If you don’t intend to use anything but standard elements,[Bootstrap](http://getbootstrap.com/) or [Foundation](http://foundation.zurb.com/) is of choice. Its range of application covers CMS, CRM, simple websites of open-source projects, fast prototypes and the likes.

However, it is not the best idea to use full CSS framework if the website has a complex design, non-standard components or complex combinations of such components (for instance, if there are A/B tests using a number of alternative component designs and page layouts).

### 5.3. CSS Methodologies

KMS encourages some combination of [OOCSS](http://oocss.org/), [BEM](http://getbem.com/) and [SMACSS](https://smacss.com/) for these reasons:

* It helps create clear, strict relationships between CSS and HTML
* It helps us create reusable, composable components
* It allows for less nesting and lower specificity
* It helps in building scalable stylesheets

**OOCSS** is a programming paradigm. OOCSS stands for Object Oriented CSS, so it's best understood in the context of Object Oriented programming: classic (spaghetti) CSS vs. OOCSS is a bit like procedural (spaghetti) backend code vs. Object-Oriented backend code.

OOCSS focuses on flexible, modular, swappable components that do One Thing Well. OOCSS focuses on the single responsibility principle, separation of concerns, and much more of the foundational concepts of Object Oriented Programming.

* Nicole Sullivan's [OOCSS wiki](https://github.com/stubbornella/oocss/wiki)
* Smashing Magazine's [Introduction to OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)

**BEM** is a specific concrete application of OOCSS. BEM stands for Block Element Modifier, and it describes the pattern of each CSS object's class name.

* CSS Trick's [BEM 101](https://css-tricks.com/bem-101/)
* Harry Roberts' [introduction to BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

**SMACSS** stands for Scalable and Modular Architecture for CSS. It's a book and a methodology for writing CSS (created by Jonathan Snook), but its most significant and influential aspect is its organizational system, which is designed to provide a set of buckets into which CSS should be organized

* [SMACSS web site](https://smacss.com/)

### 5.4. styled-components

For Reac applications, [styled-components](https://github.com/styled-components/styled-components) allows you to write actual CSS code to style your components. It also removes the mapping between components and styles – using components as a low-level styling construct could not be easier!

### 5.5. Accessibility

Accessibility shouldn't be an afterthought. You don't have to be a WCAG expert to improve your website, you can start immediately by fixing the little things that make a huge difference, such as:

- Learning to use the alt attribute properly
- Making sure your links and buttons are marked as such (no <div class=button> atrocities)
- Not relying exclusively on colors to communicate information
- Explicitly labelling form controls

Using [Web Accessibility Checklist](http://a11yproject.com/checklist.html) for your web applications.

### 5.6. Code Analysis Tools

* [ESLint](http://eslint.org/) for ECMAScript 6+ coding style checking. 
* [TSLint](https://palantir.github.io/tslint/) for TypeScript coding style checking

### 5.7. Project Management Tools

* [NPM](https://www.npmjs.com/) as the package manager for JavaScript
* Consider using _pre-defined_ npm scripts as a build tool instead of Gulp or Grunt

## 6. Checklist

There is a Front-end checklist, an exhaustive list of all elements you need to have / to test before launching your site / HTML page to production. It is based on Front-End developers’ years of experience, with the additions coming from some other open-source checklists. Detail list is at [Front-end Checklist](http://frontendchecklist.com/) 

## 6. Resources & References

### 6.1. Resources
- [HTML Best Practices](https://github.com/hail2u/html-best-practices/blob/master/README.md)
- [Airbnb CSS / Sass Style Guide](https://github.com/airbnb/css/blob/master/README.md)
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript/blob/master/README.md)
- [Angular Style Guide](https://angular.io/docs/ts/latest/guide/style-guide.html)
- [Airbnb React/JSX Style Guide](https://github.com/airbnb/javascript/blob/master/react/README.md)
- [Web Accessibility Checklist](http://a11yproject.com/checklist.html)

### 6.2. References
- [Front-end Guidelines Questionnaire](https://github.com/bradfrost/frontend-guidelines-questionnaire)
- [5 Questions Every Unit Test Must Answer](https://medium.com/javascript-scene/what-every-unit-test-needs-f6cd34d9836d#.8yjo9e8a7)
- [Bootstrap - An Intervention](https://evilmartians.com/chronicles/bootstrap-an-intervention)
- [CSS Evolution: From CSS, SASS, BEM, CSS Modules to Styled Components](https://m.alphasights.com/css-evolution-from-css-sass-bem-css-modules-to-styled-components-d4c1da3a659b#.zdulmmlze)
