---
title: Angular CLI
layout: redirect
weight: 25
---

When developing a pure Angular you can create an Angular CLI project and add Cumulocity CLI to it.
This functionality is only available after 1004.2.0.

### Install Angular CLI

Follow the [instructions](https://angular.io/cli) to install @c8y/cli globally.

```sh
npm install -g @angular/cli
```

### Create a new project

```sh
ng new my-first-iot-project
cd my-first-iot-project
```

### Add Cumulocity CLI

```sh
cd my-first-iot-project
ng add @c8y/cli
```

### Run application

```sh
ng serve
```

In your browser, open http://localhost:4200/ to see the new application run.

You can configure the [application options](#static-options) inside the package.json file and [customize branding](#branding) with LESS or CSS custom variables


