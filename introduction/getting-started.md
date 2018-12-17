# Getting Started

UGF is a GUI framework used to build A10networks GUI projects. It's composed by React.js related opensource  softwares. It's a business-adapted , higher performance, and easier debug framework.

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
* Setup bootstrap file using a10-gui-framework

```text
import React from 'react'
import ReactDOM from 'react-dom'
import { A10Provider, A10Router } from 'a10-gui-framework'

import { config } from './settings'
import appReducers from './redux/reducers'
import './styles/main.less'

import { Home } from './containers/Home'

const middlewares: any[] = []

ReactDOM.render(
  <A10Provider reducers={appReducers} middlewares={middlewares} CONFIG={config}>
    <A10Router.Browser>
      <Home />
    </A10Router.Browser>
  </A10Provider>,
  document.getElementById('root') as HTMLElement,
)
```

* Create a [Home container](https://github.com/a10networks/a10-gui-ugf-template/blob/master/src/containers/Home/Home.tsx)

```text
import React from 'react'
import {
  A10Container,
  setupA10Container,
} from 'a10-gui-framework'

// ...
class Home extends A10Container<IHomeProps, IHomeState> {
  // ...
  render() {
    return (
      <div>Hellow World!</div>
    )
  }
}

export default setupA10Container(Home)
```

* Try to import an widget from a10-gui-widgets

```text
import React from 'react'
import {
  A10Container,
  setupA10Container,
} from 'a10-gui-framework'
​
import { A10Button } from 'a10-gui-widgets'

class Home extends A10Container<IHomeProps, IHomeState> {
  // ...
  render() {
    return (
      <div>Hellow World!</div>
      <A10Button type="primary">
        Click me!
      </A10Button>
    )
  }
}
​
export default setupA10Container(Home)
```

* Read[ Framework book](../main-repositories/a10-gui-framework.md) and using [widgets storybook](../main-repositories/a10-gui-widgets.md) and [common library](../main-repositories/a10-stateful-common-library.md) storybook add more stuffs.

## Development Tools

#### IDE setup

We can use any text editor like VSCode, Sublime Text, Hbuilder, Notepad++. 

A10 oxbox GUI team we used VSCode since it's lightweight , stable and higher coding performance, so in GUI git repository, we have already setup all the VSCode running environment configurations, pull it down, add it into your VSCode editor, VSCode can help you follow GUI team dev env to start your coding. The VS Code configuration files under \[your\_project\_root\]/.vscode/

If you have your favorite IDE,  we suggest you install basic plugins such as eslint and tslint, for highlight your code, please install Typescript and ES6 relevant plugin.

For coding style, we are using  tslint:recommended, tslint-react, for more information about this topic, please see our [tslint.json](https://github.com/a10networks/a10-gui-ugf-template/blob/master/tslint.json).

#### Browser extensions recommend

For debugging React and Redux, we suggest installing following two extensions on Chrome or Firefox, it can help you debug React Virtual DOM hierarchy and Redux store data.

* [React developer Tools](https://github.com/facebook/react-devtools)
* [Redux DevTools Extension](https://github.com/zalmoxisus/redux-devtools-extension)

## Examples

\[Jason\] For more examples,  please read [Examples](examples.md) page.

## Learn 

#### Just the Basics

We have 3 main design docs for the basic concepts of framework, widget and container, please directly click following link to read.

1. [A10 GUI Framework design doc](https://github.com/a10networks/a10networks.github.io/raw/0.7.0/design-docs/A10-GUI-Framework-Design-v1.1a.docx)
2. [A10 GUI Container design doc](https://github.com/a10networks/a10networks.github.io/raw/0.7.0/design-docs/A10-Container-Design-v1.0a.docx)
3. [A10 GUI Widgets design doc](https://github.com/a10networks/a10networks.github.io/raw/0.7.0/design-docs/A10-GUI-Widgets-v1.1a.docx)
4. [A10 GUI Redux for HTTP Request design doc](https://github.com/a10networks/a10networks.github.io/raw/0.7.0/design-docs/A10ReduxHTTP_design_v1.0b.docx) 

#### Real-World Usage

If you'd like to learn how it works on real-world , please contact [ax-web-dl@a10networks.com](mailto:ax-web-dl@a10networks.com) to grant permissions to access production code.

## Help and Discussion

You can send mail to [ax-web-dl@a10networks.com](mailto:ax-web-dl@a10networks.com) or join our [slack discussion group](https://a10webguiteam.slack.com/messages/CBJH1KJKD), 

For a10-gui-framework issues, you can directly connect our framework maintainer [Roll ](mailto:stsai@a10networks.com)and [Chris](mailto:christzhusiul@a10networks.com). 

For a10-gui-widgets issues, please connect [Rui](mailto:%20ruiz@a10networks.com).

To access those frameworks' source code,  you need to be grant permissions, so you need connect [Yushan](mailto:yhou@a10networks.com) and above maintainers.

Or you can post issues to different git repository issue boards, we will answer your questions at first time to get it.

## Should You Use

This is not an open project by now, only used in A10networks Corp. If you are part of A10networks GUI developer,  welcome to use it, but please don't distribute the source code to outside of A10networks.

## Repositories Access Permission

Since it's an A10 GUI internal project, if you have no permission to access the framework repositories outside A10networks Corp.

To access those frameworks' source code,  you need to be grant permissions, so you need connect [Yushan](mailto:yhou@a10networks.com) and above maintainers.



