# A10 GUI Framework

## Introduction

A10 GUI Framework is based on modern web design. At the heart of it, we leverage a component based front-end JavaScript framework called React.js. Together with Redux and the embodiment of a set of design patterns, we aimed to provide a set of tools that allow for appealing, modern, and consistent web UI to be built with relative ease and simplicity.

### Repository path:

#### [https://github.com/a10networks/a10-gui-framework.git](https://github.com/a10networks/a10-gui-framework.git)

### Installation

$ npm i -S [https://github.com/a10networks/a10-gui-framework.git](https://github.com/a10networks/a10-gui-framework.git)

### How to use

Framework’s main components like A10Provider, A10Root, A10Router and A10Container are used to build basic scaffolding.

Easy to use! For example, simply write `import A10Provider from a10-gui-framework`

Using it as html tags in render\(\)

```jsx
import { A10Provider} from 'a10-gui-framework'
ReactDOM.render(
  <A10Provider
    CONFIG={CONFIG}
    middlewares={middlewares}
    reducers={reducers}
    initState={initState}
  >
      ...
  </A10Provider>,
  document.getElementById('root'),
)
```

## Core components

### A10Provider

A10Provider is a wrapper for React-Redux Provider. We use this wrapper to wire up some global middleware to help the system monitor global data \(theme, debug\) or to log critical information.

#### Use Case

```jsx
import middlewares from ‘approot/redux/middlewares’
import reducers from ‘approot/redux/reducers’
import { A10Provider } from ‘a10-gui-framework’
Const initState = {}
ReactDom.render(
<A10Provider
middlewares={middlewares}
reducers={reducers}
initState={initState}>
<A10Root config={} />
</A10Provider>
, documentRoot)
```

### A10Root

A10Root is the place to accept initial configurations defined in a JS file and to send into Redux. A10Root is also the place to have a component context so that every descendent can access the global variables.

#### Use Case

```jsx
import configurations from ‘approot/settings/configs’
import { A10Root } from ‘a10-gui-framework’
ReactDom.render(<A10Provider middlewares={} reducers={} initState={}>
<A10Root config={ configurations } />
</A10Provider>, documentRoot)
```

### A10Router

A10Router is a React Router wrapper, simplified from React Router for ease of use.

#### Use Case

```jsx
import routes from ‘approot/settings/routes’
import { A10Router } from ‘a10-gui-framework’
ReactDom.render(<A10Provider middlewares={} reducers={} initState={}>
<A10Root config={}>
<A10Router routes={routes}>
<Redirect from="messages/:id" to="/messages/:id" />
</A10Router>
</A10Root>
</A10Provider>, documentRoot)
```

In this case, we imported the routes from app/settings/routes.tsx. The file looks like:

```jsx
export default {
‘slb’: {
‘virtual-server’: {
component: THVirtualServerContainer,
params: [‘name’],
index: true,
title: ‘Virtual Server’,
template: {
component: THVirtualServerContainer,
title: ‘Virtual Server’,
params: [‘name’],
…
}
},
‘virtual-service’: {
component: THVirtualServiceContainer,
title: ‘Virtual Server’,
params: [‘ip’, ‘port’]
…
},
},
‘cgn’: {}
}
```

On above definition, the ‘slb’, ‘virtual-server’ will combine to a route path /slb/virtual-server, and the path will route to an A10Container called THVirtualServerContainer. params is also a Frameworks preserved option. With the params option, an example virtual-service URL looks may be of the form /slb/virtual-service/:ip/:port.

### A10Container

A10Container is the heavy-hitter. It is a stateful component which is connected to the Redux store. A10Container contains page elements, and could include A10Container, or A10Widgets, or external \(external to this Framework\) React Components.

#### Create Interface

```jsx
setupA10Container(component, mapStateToProps={}, mapDispatchToProps={}, options={}) : function
```

#### Create Container

```jsx
import { setupA10Container } from ‘a10-gui-framework’
import { A10Button, A10Input, A10Form } from ‘a10-gui-widgets’
import { THFormContainer } from ‘a10-gui-thunder-com’
Class LoginContainer extends A10Container {
Render() {
return (
<THFormContainer>
<A10Form.Item><A10Input title=”username” /></A10Form.Item>
<A10Form.Item><A10Input title=”password” type=”password” /><A10Form.Item>
<A10Form.Item><A10Button>Submit</A10Button></A10Form.Item>
</THFormContainer>
)
}
}
function mapStateToProps(state) {
return { todos: state.todos }
}
function mapDispatchToProps(dispatch) {
return bindActionCreators(Object.assign({}, todoActionCreators, counterActionCreators), dispatch)
}
Const options = {
redux: { … },
isWithRouter: true,
autoPurge: true,
}
Export default setupA10Container(LoginContainer, mapStateToProps, mapDispatchToProps, options)
```

#### Use Case

```jsx
import { A10Router, A10Provider, A10Root } from ‘a10-gui-framework’
import LoginContainer from ‘./containers/LoginContainer’
const routes = {
‘login’: LoginContainer
}
ReactDom.render(<A10Provider middlewares={} reducers={} initState={}>
<A10Root config={}>
<A10Router routes={routes}/>
</A10Root>
</A10Provider>, documentRoot)
```

### [A10 Widgets](https://a10-gui.gitbook.io/ugf/~/drafts/-LTvZa0LwJLFk24sVZd1/primary/main-repositories/a10-gui-widgets)

## [FAQ](https://a10-gui.gitbook.io/ugf/faq/a10-gui-framework)

