# Examples

## App entry

{% embed url="https://index.tsx" caption="react di" %}

## How to create the first hello world page

     A component and container having the component

## Write the hello world page with Redux

## Introduce a form page. How to setup, import widgets, and hook APIs 

### How to setup, import widgets 

### Condition 1: without Redux

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

## How to delete data

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

