# A10 GUI Framework

## Why need use GUI framework

That's a tough question but thankfully, our team is on it. Please bear with us while we're investigating.

## Setup Issues

### How to install?

 npm i -S [https://github.com/a10networks/a10-gui-framework.git](https://github.com/a10networks/a10-gui-framework.git)​

## Coding issues

### 1.Coding Style

This project code are following `Prettier` coding style. Developers do not need to care of coding style consistency as long as using `VSCode` editor and installed `Prettier` plugin. `VScode` will format your code automatically through Prettier when saving file due to `.vscode/settings.json`.

```typescript
{
  "editor.formatOnSave": true
}
```

## How to use Redux with the framework?

TBD

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

