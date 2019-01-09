# A10 GUI Framework

## Why do need to use A10's GUI framework

To provide consistency, reusability and cost savings for the construction of web UI across A10’s product portfolio, we need a common set of technologies, design guidelines, and software libraries. 

## Setup Issues

### How to install?

 npm i -S [https://github.com/a10networks/a10-gui-framework.git](https://github.com/a10networks/a10-gui-framework.git)​

## Coding issues

### 1.Coding Style

This project code follows the `Prettier` coding style. Developers do not need to care of coding style consistency as long as they are using `VSCode` editor and have installed `Prettier` plugin. `VScode` will format your code automatically through Prettier when saving file due to `.vscode/settings.json`.

```typescript
{
  "editor.formatOnSave": true
}
```

## How do I use Redux with the framework?

### 1. Create action function

```jsx
import invariant from 'invariant'

import { A10ACTION_TYPES } from '../actionTypes'

export interface IDataSetOptions {
  namespace: string | string[]
  data: any
  containerID: string
}
export interface IDataSetAction extends IDataSetOptions {
  type: string
}

export const setData = (options: IDataSetOptions) => {
  invariant(options.namespace, 'options.namespace is required')
  invariant(options.hasOwnProperty('data'), 'options.data is required')
  invariant(options.containerID, 'options.containerID is required')
  return {
    type: A10ACTION_TYPES.DATA.SET,
    ...options,
  }
}

export interface IDataRemoveOptions {
  namespace: string | string[]
  containerID?: string
}
export interface IDataRemoveAction extends IDataRemoveOptions {
  type: string
}

export const removeData = (options: IDataRemoveOptions) => {
  invariant(options.namespace, 'options.namespace is required')
  return {
    type: A10ACTION_TYPES.DATA.REMOVE,
    ...options,
  }
}
```

### 2. Create the reducer function

```jsx
import { Map, Set } from 'immutable'

import { A10ACTION_TYPES } from '../actionTypes'
import { IDataSetAction, IDataRemoveAction} from '../actions/data'

export const A10Data = (state = Map(), action: any) => {
  switch (action.type) {
    case A10ACTION_TYPES.DATA.SET: {
      const { data, namespace } = action as IDataSetAction
      const namespaceArray = Array.isArray(namespace)
        ? namespace
        : namespace.split('.')
      return state.setIn(namespaceArray, data)
    }
    case A10ACTION_TYPES.DATA.REMOVE: {
      let { namespace } = action as IDataRemoveAction
      namespace = Array.isArray(namespace) ? namespace : [namespace]
      namespace.forEach((ns: string) => {
        const nsArray = ns.split('.')
        state = state.deleteIn(nsArray)
        nsArray.pop()
        while (nsArray.length) {
          const node = state.getIn(nsArray)
          if (Map.isMap(node) && node.isEmpty()) {
            state = state.deleteIn(nsArray)
          }
          nsArray.pop()
        }
      })
      return state
    }
    default:
      return state
  }
}


```

### 3. Store / call the reducer

```jsx

  import {
  Store,
  createStore as reduxCreateStore,
  compose,
  bindActionCreators as reduxBindActionCreators,
  Dispatch,
  ActionCreator,
  Action,
} from 'redux'
import { createEpicMiddleware, combineEpics, Epic } from 'redux-observable'
import _ from 'lodash'

import { A10Epics } from './epics'
import * as A10Reducers from './reducers'

export interface IA10ReduxProps {
  reducers?: IObject
  initState?: IObject
}
export interface IA10ReduxPlugin {
  plug?(): IA10ReduxProps
  play?(store?: Store<any>): void
}

export type Plugins = Array<IA10ReduxPlugin | IA10ReduxPlugin[]>

export const createStore = (
  appReducers: IObject = {},
  data: IObject = {},
  pluginsList: Plugins = [],
) => {
  const plugins = pluginsList.reduce((list: IA10ReduxPlugin[], item) => {
    const plugin = Array.isArray(item) ? item : item ? [item] : []
    return [...list, ...plugin]
  }, [])
  const reduxProps = invokePlugins(plugins as IA10ReduxPlugin[], 'plug')
  const rootReducer = combineReducers({
    ...appReducers,
    ...A10Reducers,
    ...reduxProps.reducers,
  })
  const store = reduxCreateStore(
    rootReducer,
    {
      ...data,
      ...reduxProps.initState,
    },
  )
  return store

}
```

### 4. Using the component

```jsx
import React from 'react'
import { Store } from 'redux'
import { Provider as ReduxProvider } from 'react-redux'
import _ from 'lodash'

import { A10Root } from './A10Root'
import { CONFIG, IGlobalConfig } from '../settings/config'
import { createStore, checkNamespaces, IA10ReduxProps, Plugins } from '../redux'
import { getHTTPManager } from '../libs'

export interface IA10ProviderProps extends IA10ReduxProps {
  CONFIG: IGlobalConfig
  store?: Store<any>
  plugins?: Plugins
}

export interface IEpicDependencies {
  httpClient: IGlobalConfig['httpClient']
  HTTPManager: ReturnType<typeof getHTTPManager>
  [dependency: string]: any
}

export class A10Provider extends React.Component<IA10ProviderProps> {
  static defaultProps = {
    CONFIG,
  }
  render() {
    const {
      reducers,
      middlewares,
      initState,
      epics,
      epicDependencies,
      plugins,
      children,
      CONFIG: APP_CONFIG,
      store: providedStore,
    } = this.props
    // make GLOBAL_CONFIG and CONFIG are same reference for global imported getNS()
    const GLOBAL_CONFIG = Object.assign(CONFIG, APP_CONFIG)
    GLOBAL_CONFIG.EPIC_DEPENDENCIES = GLOBAL_CONFIG.EPIC_DEPENDENCIES || {}
    const { EPIC_DEPENDENCIES } = GLOBAL_CONFIG
    // backward compatibility support
    if (!GLOBAL_CONFIG.httpClient && EPIC_DEPENDENCIES.httpClient) {
      GLOBAL_CONFIG.httpClient = EPIC_DEPENDENCIES.httpClient
    } else {
      EPIC_DEPENDENCIES.httpClient = GLOBAL_CONFIG.httpClient
    }
    if (GLOBAL_CONFIG.DEBUG && _.isPlainObject(GLOBAL_CONFIG.REDUX_DATA_NS)) {
      checkNamespaces(GLOBAL_CONFIG.REDUX_DATA_NS)
    }
    Object.assign(EPIC_DEPENDENCIES, epicDependencies)
    const { httpClient } = GLOBAL_CONFIG
    const HTTPManager = getHTTPManager(httpClient)
    EPIC_DEPENDENCIES.HTTPManager = EPIC_DEPENDENCIES.HTTPManager || HTTPManager
    const store =
      providedStore ||
      createStore(
        reducers,
        middlewares,
        epics,
        initState,
        EPIC_DEPENDENCIES,
        plugins,
      )
    return (
      <ReduxProvider store={store} {...this.props}>
        <A10Root CONFIG={GLOBAL_CONFIG} store={store} HTTPManager={HTTPManager}>
          {children}
        </A10Root>
      </ReduxProvider>
    )
  }
}

export default A10Provider
```

## How to use redux-observable in the framework?

### 1.install `rxjs` and `redux-observable`.

```javascript
npm i -S rxjs redux-observable 
```

### 2.Create epic functions

```jsx
// approot/redux/epics/myEpic.ts
import { Observable } from 'rxjs'
import { ActionsObservable } from 'redux-observable'
import { Action, Store } from 'redux'

import { setMyActionData, IMyAction } from 'approot/redux/actions' // actionCreators
import { ACTION_TYPES } from 'approot/redux/actionTypes'

export const myActionEpic = (
  action$: ActionsObservable<Action>,
  store: Store<any>,
  epicDependencies: IObject,
): Observable<Action> => {
  // action in
  return action$
    .ofType(ACTION_TYPES.MY_ACTION)
    .mergeMap((action: IMyAction) => {
      const { params } = action
      const { httpClient, HTTPManager } = epicDependencies
      return (
        Observable.from(httpClient.get('/axapi/v3/test', params))
          // action out
          .map((response: IObject) =>
            setMyActionData({
              response,
            }),
          )
          // action out for exception
          .catch((error: IObject) =>
            Observable.of(
              setMyActionData({
                error: true,
              }),
            ),
          )
      )
    })
}
```

### 3. Collect all epic functions and then export it in epics/index.ts.

```jsx
// approot/redux/epics/index.ts
import { myActionEpic } from './myEpic'

export const epics = [myActionEpic]
export default epics
```

### 4.Provide the epics to A10Provider.

```jsx
// approot/index.ts
import React from 'react'
import ReactDOM from 'react-dom'
import { A10Provider, A10Router } from 'a10-gui-framework'

import CONFIG from 'approot/configs/global'
import middlewares from 'approot/redux/middlewares'
import reducers from 'approot/redux/reducers'
import epics from 'approot/redux/epics'
import APP from 'approot/containers/App'

const initState = {}
ReactDOM.render(
  <A10Provider
    CONFIG={CONFIG}
    middlewares={middlewares}
    reducers={reducers}
    epics={epics}
    initState={initState}
  >
    <A10Router.Browser>
      <APP />
    </A10Router.Browser>
  </A10Provider>,
  document.getElementById('root'),
)
```

## Can I use redux-thunk?

Yes, redux-thunk is an asynchronous action middleware.

## What are the benefits of using httpRequest?

All React-Redux applications need to communicate with an HTTP server. A set of common problems frequently arise while making HTTP requests: error handling, request cancellation, and state data management.  Here are some proposals for dealing with this problems.

### **Generic Error Handling**

GUI Framework will catch every HTTP error and program error at runtime. It analyzes the error, and dispatches out a Redux action with complete error information and appropriate error message \(JSON syntax or pure text\) that could be customized by app developer if needed.

### **Request Cancellation**

Every HTTP request is able to be aborted as long as developer dispatches out a cancel action. However, if the request may affect server state change, then the server state is undefined. This cancellation facility is often used when switching pages or to stop UI operations \(mainly HTTP GET requests\).

### **State Data Management**

Most developers may face issues arising from state data management in Redux store. Redux will not purge unused state data in the store by default, which may introduce unnecessary memory consumption.



