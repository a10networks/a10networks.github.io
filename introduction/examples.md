# Examples

## App entry

```markup
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="theme-color" content="#000000">
    <title>React Examples</title>
  </head>
  <body>
    <noscript>
      You need to enable JavaScript to run this app.
    </noscript>
    <div id="root"></div>
  </body>
</html>
```

```jsx
// index.tsx

import React from 'react'
import ReactDOM from 'react-dom'
import { A10Provider } from 'a10-gui-framework'

import './styles/index.less'

import Root from './Root'

ReactDOM.render(
  <A10Provider>
    <Root />
  </A10Provider>,
  document.getElementById('root') as HTMLElement,
)
```

```jsx
// Root.tsx

import React from 'react'
import { Link } from 'react-router-dom'
import {
  A10Container,
  setupA10Container,
  IA10ContainerDefaultProps,
  A10Router,
  A10Route,
} from 'a10-gui-framework'

import HelloWorld from './HelloWorld'

export interface IRootProps extends IA10ContainerDefaultProps { }
export interface IRootState { }

class Root extends A10Container<IRootProps, IRootState> {
  render() {
    return (
      <A10Router.Browser>
        <div>
          <Link to="/"> Home </Link>
          <Link to="/hello-world"> HelloWorld </Link>

          <A10Route path="/hello-world" component={HelloWorld} />
        </div>
      </A10Router.Browser>
    )
  }
}

export default setupA10Container(Root)
```

## How to create a Hello World page

```jsx
// HelloWorld.tsx

import React from 'react'
import {
  A10Container,
  setupA10Container,
  IA10ContainerDefaultProps,
} from 'a10-gui-framework'

import Description from './Description'

export interface IHelloWorldProps extends IA10ContainerDefaultProps { }
export interface IHelloWorldState { }

class HelloWorld extends A10Container<IHelloWorldProps, IHelloWorldState> {
  render() {
    return (
      <>
        <h1>Hello World!</h1>
        <Description />
      </>
    )
  }
}
export default setupA10Container(HelloWorld)
```

```jsx
// Description.tsx

import React from 'react'
import { A10Component } from 'a10-gui-framework'

export interface IDescriptionProps { }
export interface IDescriptionState { }

class Description extends A10Component<IDescriptionProps, IDescriptionState> {
  render() {
    return (
      <>
        <p>This is A10Networks.</p>
      </>
    )
  }
}
export default Description
```

## Enhance the Hello World page

```jsx
// Root.tsx

import React from 'react'
import { Link } from 'react-router-dom'
import {
  A10Container,
  setupA10Container,
  IA10ContainerDefaultProps,
  A10Router,
  A10Route,
} from 'a10-gui-framework'

import HelloWorld from './HelloWorld'
import HelloTarget from './HelloTarget'

export interface IRootProps extends IA10ContainerDefaultProps { }
export interface IRootState { }

class Root extends A10Container<IRootProps, IRootState> {
  render() {
    return (
      <A10Router.Browser>
        <div>
          <Link to="/"> Home </Link>
          <Link to="/hello-world"> HelloWorld </Link>
          <Link to="/hello-target"> HelloTarget </Link>

          <A10Route path="/hello-world" component={HelloWorld} />
          <A10Route path="/hello-target" component={HelloTarget} />
        </div>
      </A10Router.Browser>
    )
  }
}

export default setupA10Container(Root)
```

```jsx
// HelloTarget.tsx

import React from 'react'
import {
  A10Container,
  setupA10Container,
  IA10ContainerDefaultProps,
} from 'a10-gui-framework'

import SourceDescription from './SourceDescription'
import InputTargetAndSource from './InputTargetAndSource'

export interface IHelloTargetProps extends IA10ContainerDefaultProps { }
export interface IHelloTargetState {
  target: string
  source: string
}

class HelloTarget extends A10Container<IHelloTargetProps, IHelloTargetState> {
  constructor(props: IHelloTargetProps) {
    super(props)

    this.state = {
      target: 'World',
      source: 'A10Networks'
    }
  }

  changeTarget = (target: string, source: string) => {
    this.setState({
      target,
      source,
    })
  }

  render() {
    const { target, source } = this.state

    return (
      <>
        <h1>Hello {target}!</h1>
        <SourceDescription source={source} />
        <InputTargetAndSource
          defaultTarget={target}
          defaultSource={source}
          onClickOK={(newTarget: string, newSource: string) => {
            this.setState({
              target: newTarget,
              source: newSource,
            })
          }}
        />
      </>
    )
  }
}
export default setupA10Container(HelloTarget)
```

```jsx
// SourceDescription.tsx

import React from 'react'
import { A10Component } from 'a10-gui-framework'

export interface IDescriptionProps {
  source: string
}

export interface IDescriptionState { }

class SourceDescription extends A10Component<IDescriptionProps, IDescriptionState> {
  render() {
    const { source } = this.props

    return (
      <>
        <p>This is {source}.</p>
      </>
    )
  }
}
export default SourceDescription
```

```jsx
// InputTargetAndSource.tsx

import React from 'react'
import { A10Component } from 'a10-gui-framework'

export interface IInputTargetAndSourceProps {
  defaultTarget?: string
  defaultSource?: string
  onClickOK: (target: string, source: string) => void
}

export interface IInputTargetAndSourceState {
  target: string
  source: string
}

class InputTargetAndSource extends A10Component<IInputTargetAndSourceProps, IInputTargetAndSourceState> {
  constructor(props: IInputTargetAndSourceProps) {
    super(props)

    const { defaultTarget, defaultSource } = props
    this.state = {
      target: defaultTarget || '',
      source: defaultSource || '',
    }
  }

  onTargetChanges = (event: any) => {
    this.setState({
      target: event.target.value,
    })
  }

  onSourceChanges = (event: any) => {
    this.setState({
      source: event.target.value,
    })
  }

  onClickOK = () => {
    const { onClickOK } = this.props
    const { target, source } = this.state

    if (onClickOK && onClickOK instanceof Function) {
      onClickOK(target, source)
    }
  }

  render() {
    const { target, source } = this.state

    return (
      <>
        <label htmlFor="source"><strong>From: </strong></label>
        <input id="source" type="text" value={source} onChange={this.onSourceChanges} />
        <label htmlFor="target"><strong>To: </strong></label>
        <input id="target" type="text" value={target} onChange={this.onTargetChanges} />
        <button onClick={this.onClickOK} >OK</button>
      </>
    )
  }
}
export default InputTargetAndSource
```

## Enhance the Hello World page with Redux

```jsx
// index.tsx

import React from 'react'
import ReactDOM from 'react-dom'
import { A10Provider } from 'a10-gui-framework'

import './styles/index.less'

import reducers from './reducers'
import Root from './Root'

ReactDOM.render(
  <A10Provider
    initState={{ target: 'World', source: 'A10Networks' }}
    reducers={reducers}
  >
    <Root />
  </A10Provider>,
  document.getElementById('root') as HTMLElement,
)
```

```jsx
// reducers.ts

function changeTarget(preState = '', action: IObject) {
  switch (action.type) {
    case 'Change Target':
      return action.newTarget
    default:
      return preState
  }
}

function changeSource(preState = '', action: IObject) {
  switch (action.type) {
    case 'Change Source':
      return action.newSource
    default:
      return preState
  }
}

export default {
  target: changeTarget,
  source: changeSource,
}
```

```jsx
// Root.tsx

import React from 'react'
import { Link } from 'react-router-dom'
import {
  A10Container,
  setupA10Container,
  IA10ContainerDefaultProps,
  A10Router,
  A10Route,
} from 'a10-gui-framework'

import HelloWorld from './HelloWorld'
import HelloTarget from './HelloTarget'
import HelloTargetWithRedux from './HelloTargetWithRedux'

export interface IRootProps extends IA10ContainerDefaultProps { }
export interface IRootState { }

class Root extends A10Container<IRootProps, IRootState> {
  render() {
    return (
      <A10Router.Browser>
        <div>
          <Link to="/"> Home </Link>
          <Link to="/hello-world"> HelloWorld </Link>
          <Link to="/hello-target"> HelloTarget </Link>
          <Link to="/hello-target-redux"> HelloTargetWithRedux </Link>

          <A10Route path="/hello-world" component={HelloWorld} />
          <A10Route path="/hello-target" component={HelloTarget} />
          <A10Route path="/hello-target-redux" component={HelloTargetWithRedux} />
        </div>
      </A10Router.Browser>
    )
  }
}

export default setupA10Container(Root)
```

```jsx
// HelloTargetWithRedux.tsx

import React from 'react'
import {
  A10Container,
  setupA10Container,
  IA10ContainerDefaultProps,
} from 'a10-gui-framework'

import DescriptionWithRedux from './DescriptionWithRedux'
import ControlTargetAndSource from './ControlTargetAndSource'

export interface IHelloTargetWithReduxProps extends IA10ContainerDefaultProps {
  target: string
}

export interface IHelloTargetWithReduxState { }

class HelloTargetWithRedux extends A10Container<IHelloTargetWithReduxProps, IHelloTargetWithReduxState> {
  render() {
    const { target } = this.props

    return (
      <>
        <h1>Hello {target || ''}!</h1>
        <DescriptionWithRedux />
        <ControlTargetAndSource />
      </>
    )
  }
}

function mapStateToProps(state: any) {
  const { target } = state
  return {
    target,
  }
}

export default setupA10Container(HelloTargetWithRedux, { mapStateToProps })
```

```jsx
// DescriptionWithRedux.tsx

import React from 'react'
import {
  A10Container,
  setupA10Container,
  IA10ContainerDefaultProps,
} from 'a10-gui-framework'

export interface IDescriptionWithReduxProps extends IA10ContainerDefaultProps {
  source: string
}

export interface IDescriptionWithReduxState { }

class DescriptionWithRedux extends A10Container<IDescriptionWithReduxProps, IDescriptionWithReduxState> {
  render() {
    return (
      <>
        <p>This is {this.props.source || ''}.</p>
      </>
    )
  }
}

function mapStateToProps(state: any) {
  const { source } = state
  return {
    source,
  }
}

export default setupA10Container(DescriptionWithRedux, { mapStateToProps })
```

```jsx
// ControlTargetAndSource.tsx

import React from 'react'
import {
  A10Container,
  setupA10Container,
  IA10ContainerDefaultProps,
} from 'a10-gui-framework'

import { changeTarget, changeSource } from './actions'

export interface IControlTargetAndSourceProps extends IA10ContainerDefaultProps {
  target: string
  source: string
  onChangeTarget: (t: string) => {}
  onChangeSource: (s: string) => {}
}

export interface IControlTargetAndSourceState {
  newTarget: string
  newSource: string
}

class ControlTargetAndSource extends A10Container<IControlTargetAndSourceProps, IControlTargetAndSourceState> {
  constructor(props: IControlTargetAndSourceProps) {
    super(props)

    const { target, source } = this.props
    this.state = {
      newTarget: target || '',
      newSource: source || '',
    }
  }

  onClickOK = () => {
    const { onChangeTarget, onChangeSource } = this.props
    const { newTarget, newSource } = this.state
    onChangeTarget(newTarget)
    onChangeSource(newSource)
  }

  onInputTarget = (event: any) => {
    this.setState({
      newTarget: event.target.value,
    })
  }

  onInputSource = (event: any) => {
    this.setState({
      newSource: event.target.value,
    })
  }

  render() {
    const { newTarget, newSource } = this.state

    return (
      <>
        <label htmlFor="source"><strong>From: </strong></label>
        <input id="source" type="text" value={newSource} onChange={this.onInputSource} />
        <label htmlFor="target"><strong>To: </strong></label>
        <input id="target" type="text" value={newTarget} onChange={this.onInputTarget} />
        <button onClick={this.onClickOK} >OK</button>
      </>
    )
  }
}

function mapStateToProps(state: any) {
  const { target, source } = state
  return {
    target,
    source,
  }
}

function mapDispatchToProps(dispatch: any) {
  return {
    onChangeTarget: (target: string) => {
      dispatch(changeTarget(target))
    },
    onChangeSource: (source: string) => {
      dispatch(changeSource(source))
    },
  }
}

export default setupA10Container(ControlTargetAndSource, { mapStateToProps, mapDispatchToProps })
```

```jsx
// actions.ts

export function changeTarget(target: string) {
  return {
    type: 'Change Target',
    newTarget: target,
  }
}

export function changeSource(source: string) {
  return {
    type: 'Change Source',
    newSource: source,
  }
}
```

## Introduce a form page. How to setup, import widgets, and hook up APIs

### Condition 1: without Redux

**Setup:**

Under the path `“containers\FW\RuleSet\ZoneForm”` create `ZoneForm.tsx`

**import widgets:**

```jsx
import { A10Switch, A10Select, A10Icon, A10Notification, A10Form, A10Input,} from 'a10-gui-widgets'
```

**Hook APIS：**

getData:

```jsx
getZone(zoneName: string) {
    const {
      A10Dispatchers: { httpRequest },
    } = this.props

    httpRequest({
      namespace: namespaceZoneForm,
      request: async (dependencies: IEpicDependencies) => {
        return dependencies.httpClient
          .get(`/axapi/v3/zone/${zoneName}`)
          .then((response: IAxiosResponse) => {
            return Map<string, any>(response.data.zone)
          })
          .catch((error: IAxiosError) => {
            A10Notification.error({
              message: 'Error!',
              description: _.get(
                error,
                'response.data.response.err.msg',
                error.message,
              ),
            })
            return Map<string, any>()
          })
      },
    })
  }
```

SaveData:

```jsx
saveZone = () => {
...
const response = (httpClient as IAxiosInstance)
      .post(aXAPI, {
        zone: payload,
      })
      .then(() => {
        A10Notification.success({
          message: 'Success!',
          description: `${zoneName} was ${
            isUpdate ? 'updated' : 'created'
          } successfully.`,
        })
        onSubmitSuccess()
      })
      .catch((error: IAxiosError) => {
        A10Notification.error({
          message: 'Error!',
          description: _.get(
            error,
            'response.data.response.err.msg',
            error.message,
          ),
        })
      })

    return response
}
```

### Condition 2:with Redux

## Show data/table.

#### How to display it

```jsx
...
render() {
    const { columns, dataSource } = this.state
    return (
      <A10Table
        className="member-status"
        dataSource={dataSource}
        columns={columns}
        bordered
      />
    )
  }
...
```

#### Users roles with permission

## How to update the data

```jsx
  type IOnEdit = (name: string) => () => void
  ...
  onEditZone: IOnEdit = (name: string) => {
    return () => {
      this.context.openSlidingPage(
        <ZoneForm
          zoneName={name}
          onCancel={this.closeSlidingPage}
          onSubmitSuccess={this.closeSlidingPage}
        />,
      )
    }
  }
  ...
```

## How to delete data

```jsx
 type IOnDelete = (name: string) => () => void
 ...
 onDeleteZone: IOnDelete = (name: string) => {
    return () => {
      A10Modal.confirm({
        title: 'Confirmation',
        content: 'Are you sure to delete the selected item?',
        okText: 'Yes',
        okType: 'danger',
        cancelText: 'No',
        onOk: this.deleteZone(name),
      })
    }
  }
  ...
```

## How to use A10 GUI common: AutoLog Gen

```jsx
import * as React from 'react'
import * as PropTypes from 'prop-types'
import { A10Container, setupA10Container } from 'a10-gui-framework'
import { AutoLog } from 'a10-gui-common'
import { RouteComponentProps } from 'react-router'

interface ILogPageProps
  extends RouteComponentProps<{
    moduleName: string
  }> {}

class LogPage extends A10Container<ILogPageProps> {
  static contextTypes = {
    getHelpPage: PropTypes.func,
  }
  context: any

  render() {
    const {
      match: {
        url,
        params: { moduleName },
      },
    } = this.props
    const { getHelpPage } = this.context
    const schemaPath = `log/${moduleName}`
    return <AutoLog schemaPath={schemaPath} helpPagePath={getHelpPage(url)} />
  }
}
export default setupA10Container(LogPage, {
  isWithRouter: true,
})
```

## How to use A10 App Generator

## Extra: Using the examples above with the A10 Generator

