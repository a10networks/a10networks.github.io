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

#### Users roles with permission

## How to update the data

## How to delete data

## How to use A10 GUI common: AutoLog Gen

```jsx
import { AutoForm } from 'a10-gui-common'
...
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
  ...
```

## How to use A10 App Generator

## Extra: Using the examples above with the A10 Generator 

