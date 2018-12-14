---
description: 'UGF: A10 Unified  GUI Framework'
---

# Getting Started

UGF is a GUI framework used to build A10networks GUI pages. It's composed by React.js related opensource  softwares. It's a business-adapted , higher performance, and easier debug framework.

Here are the key features on current release:

1. Using some design pattern seamlessly integrated GUI team required technologies like React.js, Redux+Observable, Immutable.js, add GUI team general used logic.
2. A separate widget library we named a10-gui-widgets, all the components inside this are stateless, means it can only accept data to display.
3. A stateful components library we called a10-gui-common, it stored many stateful components, it's a kind of small app component, example, a Log Auto Gen component, plugin to framework, fill some parameters, then it's an awesome feature.
4. Generator can help you easily integrate all things together, it can generate framework in one key, also can generate your module containers and components initial model.
5. Integrated UT framework Jest and E2E test framework Nightwatch,  developer's can follow the examples easily write your own cases under your modules.

## Installation

### Using generator 

The easiest way to start a project I recommend you to use UGF generator, it's a [Yeoman ](https://yeoman.io/)generator, you need first install Yeoman tool, and then follow the [Generate Your App](generate-your-app.md)  steps to generate the whole framework and it's required stuffs,  after go through those simple steps, you app is running up. 

If you'd like learning deeper, then you can add your generated code into your IDE,  start from \[project name\]/index.tsx.

### I would like to build blocks

If you would like try to build the whole thing by yourself,  here are some prerequisites software:

1. Nodejs 8.11+ 
2. git
3. create-react-app

then here is the basic steps:

* Initial a project using create-react-app

```text
$ create-react-app my-project
```

*  Adding required GUI framework components into [package.json](https://github.com/a10networks/a10-gui-ugf-template/blob/master/package.json)

```text
"dependencies": {
    "a10-gui-framework": "git+https://git.a10networks.com:8443/scm/guinext/a10-gui-framework.git",
    "a10-gui-widgets": "git+https://git.a10networks.com:8443/scm/guinext/a10-gui-widgets.git",
    ...
  },

  ...
```

* Using npm tool to install all your required softwares

```text
$ npm install
```

* Create basic folder and file structure under the source folder, see [reference](https://github.com/a10networks/a10-gui-ugf-template/tree/master/src)
* Read[ Framework book](../main-repositories/a10-gui-framework.md) and using [widgets storybook](../main-repositories/a10-gui-widgets.md) and [common library](../main-repositories/a10-stateful-common-library.md) storybook to build your app

### Development Tools

IDE setup

Browser extensions recommend

### Basic Example



### Examples

Waiting for Jason provide examples

## Learn 

#### Just the Basics

#### Intermediate Concepts

#### Real-World Usage

## Help and Discussion

## Should You Use

## Repositories Access Permission

Since it's an A10 GUI internal project, if you have no permission to access the framework repositories, please contact us.



