# A10 GUI Common Library

## Introduction <a id="introduction"></a>

A10Container is the abstract class for all A10 containers to implement. It is based on the A10 GUI Framework to maximize modularity and maintainability. 

### Repo path: 

[https://github.com/a10networks/a10-gui-common.git](https://github.com/a10networks/a10-gui-common.git)

### Install

 1. Add `a10-gui-common` into your package.json.

  "a10-gui-common": "[git+](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-common/null)[https://github.com/a10networks/a10-gui-common.git](https://github.com/a10networks/a10-gui-common.git)"

2. Execute `npm i a10-gui-common` 

 `$ npm i a10-gui-common`

 _**NOTE:** `a10-gui-common` requires `a10-gui-framework` and `a10-gui-widgets`_

### How to use

Usage of Auto-Config Form

```jsx
import { AutoForm } from 'a10-gui-common'

const yourComponent = () => {
  return (
    <AutoForm
      schemaPath="config/form/virtual-server"
      apiPrefix="/hccapi/v3"
      defaultParams={{ provider: 'root', tenant: 't1' }}
      interceptor={{
        onSubmitSuccess: (sformUtils, response) => {
          // TODO
        },
        onCancel: (sformUtils, error) => {
          // TODO
        },
      }}
    />
  )
}
```

​

## Containers

### A10Container

 A10Container is abstract class for all containers. It extends A10Component and implements IA10Container interface.

#### use case

```jsx
export default interface IA10Container {

}

// A10 abstract container
export default Class A10Container extends React.Component<IA10Container> {

}
export default setupA10Container(A10Container)

```

### THObjectExplorerContainer

THObjectExplorerContainer extends A10Container and implemented the interface ITHObjectExplorerProps.

#### use case

```jsx
export default interface ITHObjectExplorerContainerProps {

}

export default Class THObjectExplorerContainer extends A10Container<ITHObjectExplorerContainerProps> {

}
```

### AutoForm

AutoForm has the consistent look and feel cross multiple product line such as Harmony controller and Thunder and development teams. And Auto generate React GUI form pages using UI JSON schema files provided by CM team.

#### use case

```jsx
import { AutoForm } from 'a10-gui-common'
onClickNewRuleset = (event: React.SyntheticEvent) => {
  const { actions } = this.props
  event.preventDefault()
  event.stopPropagation()
  this.context.openSlidingPage(
    <AutoForm
      showSectionIcon={true}
      schemaPath="config/form/rule-set"
      params={{
        afterActivate: actions.getActiveRuleset,
      }}
      interceptor={this.handleInterceptorRuleset()}
    />,
  )
}
```

### SForm

Auto-config form \(SForm\) is using UI JSON schema to generate React form. The form includes layout, sections, fields, buttons and create/update functionalities. However, comparing to form mockups, certain fields might not exist in UI JSON schema. These fields are called customized fields.

#### use case

```jsx
import { SForm } from 'a10-gui-common'

export default SForm.customize({
  onInitSchema: (schemaFields: IObject) => {
    schemaFields['class-list.type']['cm-meta'].allowed = [
      {
        label: 'IPv4',
        value: 'ipv4',
        help: 'Make class-list type IPv4',
      },
      {
        label: 'IPv6',
        value: 'ipv6',
        help: 'Make class-list type IPv6',
      },
    ]
  },
  onRenderSection: (interceptors: any, title: string): any => {
    const { getFieldValue } = interceptors
    if (title !== 'IPv4' && title !== 'IPv6' && title !== 'Basic') {
      return null
    } else {
      if (getFieldValue('class-list.type') !== 'ipv4' && title === 'IPv4') {
        return null
      }
      if (getFieldValue('class-list.type') !== 'ipv6' && title === 'IPv6') {
        return null
      }
    }
  },
})
```

## To do list

#### WAFForm



## ​[FAQ](https://a10-gui.gitbook.io/ugf/faq/a10-gui-framework)​ <a id="faq"></a>

