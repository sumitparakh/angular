# Angular Architecture

This document provides a high-level overview of the Angular framework's architecture. It is intended for developers who want to understand how Angular is built and how the different parts of the framework fit together.

## High-Level Overview

Angular is a platform and framework for building single-page client applications using HTML and TypeScript. It is built around the concept of components, which are the fundamental building blocks of Angular applications.

At its core, Angular is a dependency injection framework. It provides a way to declare dependencies between different parts of your application and have the framework instantiate and wire them together for you.

### Components and Templates

Angular applications are made up of a tree of components. Each component is responsible for a part of the UI and is defined by a class and a template. The template is written in HTML and can contain Angular-specific syntax to bind data to the DOM and define the component's structure.

### Decorators

Angular uses decorators to add metadata to classes, methods, and properties. This metadata tells Angular how to process the class and its members. For example, the `@Component` decorator identifies a class as a component and provides metadata about it, such as its template, styles, and selector.

### Compilation

Angular applications can be compiled in two ways:

*   **Just-in-Time (JIT) compilation:** The application is compiled in the browser at runtime. This is the default for development.
*   **Ahead-of-Time (AOT) compilation:** The application is compiled at build time. This results in a smaller, faster application.

The Angular compiler, called Ivy, is responsible for compiling the application's templates and decorators into JavaScript code that can be executed in the browser.

### Modules

Angular applications are organized into modules. A module is a container for a group of related components, directives, pipes, and services. The root module, `AppModule`, is responsible for bootstrapping the application.

### Dependency Injection

Dependency injection (DI) is a core concept in Angular. It is a design pattern in which a class requests dependencies from external sources rather than creating them itself. In Angular, the injector is responsible for creating and managing dependencies.

## Core Packages

The Angular framework is a monorepo that is composed of several packages. Each package is a separate NPM package and has a specific purpose. The following is a list of the core packages and their descriptions:

*   **`@angular/core`**: Provides the core functionality of the Angular framework, including the dependency injection system, component lifecycle hooks, and decorators.
*   **`@angular/common`**: Provides commonly needed services, pipes, and directives, such as `ngIf` and `ngFor`.
*   **`@angular/compiler`**: The Angular compiler. It takes the application's templates and decorators and compiles them into JavaScript code.
*   **`@angular/compiler-cli`**: The command-line interface for the Angular compiler. It is used to compile Angular applications ahead-of-time (AOT).
*   **`@angular/platform-browser`**: Contains the code that is specific to running Angular applications in a browser, such as DOM manipulation and event handling.
*   **`@angular/platform-browser-dynamic`**: Provides the just-in-time (JIT) compiler for Angular applications.
*   **`@angular/router`**: The Angular router. It is used to navigate between different views in an application.
*   **`@angular/forms`**: Provides support for building forms in Angular applications.
*   **`@angular/animations`**: Provides support for animations in Angular applications.
*   **`@angular/elements`**: Provides support for creating custom elements that can be used in any web application.
*   **`@angular/service-worker`**: Provides support for service workers in Angular applications.
*   **`@angular/upgrade`**: Provides tools for upgrading AngularJS applications to Angular.
*   **`zone.js`**: A library for managing execution contexts, which is a key part of Angular's change detection mechanism.

## Build Process

To build the Angular framework from source, you will need to have the following software installed on your machine:

*   [Git](https://git-scm.com/)
*   [Node.js](https://nodejs.org)
*   [Yarn](https://yarnpkg.com/)

### Getting the Sources

First, you need to fork and clone the Angular repository:

```shell
# Clone your GitHub repository:
git clone git@github.com:<github username>/angular.git

# Go to the Angular directory:
cd angular

# Add the main Angular repository as an upstream remote to your repository:
git remote add upstream https://github.com/angular/angular.git
```

### Installing Dependencies

Next, you need to install the project's dependencies using Yarn:

```shell
yarn install
```

### Building the Project

To build the project, run the following command:

```shell
yarn build
```

The build artifacts will be placed in the `dist/packages-dist` directory.

### Running Tests

To run the tests, you can use the following command:

```shell
yarn test //packages/...
```

This will run all the tests for all the packages.

## Compiler

The Angular compiler, known as Ivy, is responsible for transforming Angular templates and decorators into plain JavaScript that can be understood by the browser. This compilation process can happen either Just-in-Time (JIT) in the browser, or Ahead-of-Time (AOT) as a build step.

### ngtsc: The Angular Compiler

`ngtsc` is a TypeScript-to-JavaScript transpiler that transforms Angular decorators into static properties on classes. It's a minimal wrapper around the TypeScript compiler (`tsc`) and includes a set of Angular-specific transforms. `ngtsc` operates on your application's source code.

### ngcc: The Angular Compatibility Compiler

`ngcc` (Angular Compatibility Compiler) is a tool that processes code from `node_modules` and produces an Ivy-compatible version. This is necessary because libraries on NPM are not always compiled with Ivy. `ngcc` allows you to use these older libraries in your Ivy application.

### Decorator Compilation

The compiler's main job is to take the metadata from decorators like `@Component`, `@Directive`, and `@Injectable` and convert it into static properties on the class. For example, a `@Component` decorator will be compiled into a `ɵcmp` static property on the component's class. This static property contains all the information that Angular needs to create and manage the component at runtime.

### Tree-Shaking and Reference Inversion

One of the key features of the Ivy compiler is its ability to produce tree-shakable code. Tree-shaking is the process of removing unused code from your application, which results in a smaller bundle size.

To make tree-shaking possible, the compiler performs a process called "reference inversion". This process analyzes your templates and determines which components, directives, and pipes are actually used. It then adds direct references to these used types in the component's definition. This allows the bundler to safely remove any unused types.
