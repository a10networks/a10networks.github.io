# Examples

## App entry

{% embed url="https://index.tsx" caption="react di" %}

## How to create the first hello world page

     A component and container having the component

component

```jsx
class HelloWorld extends A10Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>
  }
}

export default HelloWorld
```

container

```jsx
class HelloWorldContainer extends A10Containder {
  render() {
    return (
      <HelloWorld name="World" />
    )
  }
}
export default setupA10Container(HelloWorldContainer)
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

