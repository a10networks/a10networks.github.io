# Examples

## App entry

```html

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
import { A10Provider, A10Router } from 'a10-gui-framework'

import './styles/index.less'

import Root from './Root'

ReactDOM.render(
  <A10Provider>
    <A10Router.Browser>
      <Root />
    </A10Router.Browser>
  </A10Provider>,
  document.getElementById('root') as HTMLElement,
)


```

```jsx
// Root.tsx

import React from 'react'
import {
  A10Container,
  setupA10Container,
  IA10ContainerDefaultProps,
  A10Route,
} from 'a10-gui-framework'

import HelloWorld from './HelloWorld'

export interface IRootProps extends IA10ContainerDefaultProps { }
export interface IRootState { }

class Root extends A10Container<IRootProps, IRootState> {
  render() {
    return (
      <>
        {/* This is the Root Container. */}
        <A10Route path="/" component={HelloWorld} />
      </>
    )
  }
}

export default setupA10Container(Root)

```

## How to create the first hello world page

```jsx
// HelloWorld.tsx

import React from 'react'
import { A10Container, setupA10Container, IA10ContainerDefaultProps } from 'a10-gui-framework'

import InputName from './InputName'

export interface IHelloWorldProps extends IA10ContainerDefaultProps { }
export interface IHelloWorldState {
  target: string
}

class HelloWorld extends A10Container<IHelloWorldProps, IHelloWorldState> {
  constructor(props: IHelloWorldProps) {
    super(props)

    this.state = {
      target: 'World',
    }
  }

  changeTarget = (name: string) => {
    this.setState({
      target: name,
    })
  }

  render() {
    return (
      <>
        <h1>Hello {this.state.target}!</h1>
        <InputName onOK={this.changeTarget} />
      </>
    )
  }
}

export default setupA10Container(HelloWorld)

```

```jsx
// InputName.tsx

import React from 'react'
import { A10Component } from 'a10-gui-framework'

export interface IInputNameProps {
  onOK: (name: string) => void
}

export interface IInputNameState {
  name: string
}

export class InputName extends A10Component<IInputNameProps, IInputNameState> {
  constructor(props: IInputNameProps) {
    super(props)

    this.state = {
      name: '',
    }
  }

  onNameChanges = (event: any) => {
    this.setState({
      name: event.target.value,
    })
  }

  onClickOK = () => {
    const { onOK } = this.props
    const { name } = this.state

    if (onOK && onOK instanceof Function) {
      onOK(name)
    }
  }

  render() {
    return (
      <>
        <label htmlFor="name"><strong>Input target Name: </strong></label>
        <input id="name" type="text" onChange={this.onNameChanges} />
        <button onClick={this.onClickOK} >OK</button>
      </>
    )
  }
}

export default InputName

```

## Write the hello world page with Redux

## Introduce a form page. How to setup, import widgets, and hook APIs

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

