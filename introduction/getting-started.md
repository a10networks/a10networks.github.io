# Getting Started

## Installation

### Using a generator 

To quick a start a project, we recommend using a UGF generator--a [Yeoman ]((https://yeoman.io/)generator). 

Follow these steps:

1. First install Yeoman tool
2. Then follow the steps from [Generate Your App](generate-your-app.md) to generate the whole framework and its required items.
3. Your app should be running! 

If you'd like to learn more, you can add your generated code into your IDE, and start from \[project name\]/index.tsx.

### I would like to build blocks

If you would like try to build the whole thing by yourself,  here are the required technologies:

1. Nodejs 8.11+ 
2. git
3. create-react-app

After you have acquired the required technologies, follow these steps: 

* Initialize a project using create-react-app

```text
$ create-react-app my-project
```

*  Adding required GUI framework components into [package.json](https://github.com/a10networks/a10-gui-ugf-template/blob/master/package.json)

```javascript
"dependencies": {
    "a10-gui-framework": "https://github.com/a10networks/a10-gui-framework.git",
    "a10-gui-widgets": "https://github.com/a10networks/a10-gui-framework.git",
    "a10-gui-common": "https://github.com/a10networks/a10-gui-common.git",
    ...
  },

  ...
```

* Using npm tool to install all your required softwares

```bash
$ npm install
```

* Create the basic folder and file structure under the source folder, see [reference](https://github.com/a10networks/a10-gui-ugf-template/tree/master/src)
* Setup bootstrap file using a10-gui-framework

```jsx
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

```jsx
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

* Try to import a widget from a10-gui-widgets

```jsx
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

* Read our [ Framework book](../main-repositories/a10-gui-framework.md) and use [widgets storybook](../main-repositories/a10-gui-widgets.md) and our [common library](../main-repositories/a10-stateful-common-library.md) storybook to add more functionalities.

## Development Tools

#### IDE setup

Use any text editor like VSCode, Sublime Text, Hbuilder, Notepad++. 

A10 Onbox GUI team uses VSCode since it's lightweight , stable, and has higher code performance. In our GUI git repository, we have already setup all the VSCode running environment configurations, so all you need to do is to pull it down, add it into your VSCode editor, and VSCode will help you startup GUI team's dev environment. The VS Code configuration files are under \[your\_project\_root\]/.vscode/

If you have your favorite IDE,  we suggest you install basic plugins such as eslint and tslint. To highlight your code, please install Typescript and ES6 relevant plugin.

For coding style, we are using  tslint:recommended and tslint-react. For more information about this topic, please see [tslint.json](https://github.com/a10networks/a10-gui-ugf-template/blob/master/tslint.json).

#### Browser extensions recommend

For debugging React and Redux, we suggest installing the following two extensions on Chrome or Firefox, as it can help you debug React's Virtual DOM hierarchy and Redux store data.

* [React developer Tools](https://github.com/facebook/react-devtools)
* [Redux DevTools Extension](https://github.com/zalmoxisus/redux-devtools-extension)

## Examples

For more examples,  please read [Examples](examples.md) page.

## Learn 

#### Just the Basics

We have 3 main design documents that include the basic concepts of our framework, widget, and container, please click the following links to read.

1. [A10 GUI Framework design doc](https://github.com/a10networks/a10networks.github.io/raw/0.7.0/design-docs/A10-GUI-Framework-Design-v1.1a.docx)
2. [A10 GUI Container design doc](https://github.com/a10networks/a10networks.github.io/raw/0.7.0/design-docs/A10-Container-Design-v1.0a.docx)
3. [A10 GUI Widgets design doc](https://github.com/a10networks/a10networks.github.io/raw/0.7.0/design-docs/A10-GUI-Widgets-v1.1a.docx)
4. [A10 GUI Redux for HTTP Request design doc](https://github.com/a10networks/a10networks.github.io/raw/0.7.0/design-docs/A10ReduxHTTP_design_v1.0b.docx) 

#### Real-World Usage

If you'd like to learn how it works in the real-world , please contact [ax-web-dl@a10networks.com](mailto:ax-web-dl@a10networks.com) to gain permission to access the production code.

## Help and Discussion

You can send an e-mail to [ax-web-dl@a10networks.com](mailto:ax-web-dl@a10networks.com) or join our [slack discussion group](https://a10webguiteam.slack.com/messages/CBJH1KJKD), 

For a10-gui-framework issues, you can directly connect our framework maintainer [Roll ](mailto:stsai@a10networks.com) and [Chris](mailto:christzhusiul@a10networks.com). 

For a10-gui-widgets issues, please connect [Rui](mailto:%20ruiz@a10networks.com).

Permissions needs to be granted in order to access the frameworks' source codes. Email / connect with [Yushan](mailto:yhou@a10networks.com) and the aformentioned maintainers to be granted permission.

An alternative is to post your issue(s) to the relevant git repository issue boards; we will answer your questions ASAP.

## Should You Use?

This is currently not an open source project, as it is only used in A10networks Corp. You are welcome to use this framework and code as a A10networks GUI developer, but please don't distribute the source code to anywhere outside of A10networks.

## Repositories Access Permission

As an A10 GUI internal project, you have no permission to access the framework repositories outside A10networks Corp.

To access those frameworks' source code,  you need to be grant permissions, so you need connect [Yushan](mailto:yhou@a10networks.com) and the relevant maintainers mentioned above.



