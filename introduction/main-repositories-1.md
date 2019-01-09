# Main Repositories

## A10 GUI Framework

### What is it?

It's the base of our framework.

It's also a HOC library for React.js and Redux, where our framework has encapsulated some core concepts like containers, components, widgets, and also some frequently used features like i18n, a feature debugger. 

If you want to write your own component or container, please refer to this repository while including relevant interfaces and examples to contribute to a widget. You can write the code as below.

```jsx
import { createA10Widget, A10Component } from 'a10-gui-framework'
class A10Button extends A10Component<IA10ButtonProps> {
}
export default createA10Widget(A10Button)
```

To read more, please see[ A10 GUI Framework.](../main-repositories/a10-gui-framework.md)

### How to make it work?

Since this is not a public repository, you have to add the repository git path to your package.json 

```text
 "dependencies": {
    "a10-gui-framework": "https://github.com/a10networks/a10-gui-framework.git",
    ...
}
```

Then use npm install to install it. If you come across any installation issues, please see the FAQ of [A10 GUI Framework](../faq/a10-gui-framework.md).

To setup the bootstrap code, please refer to [ a10-gui-ugf-template bootstrap code](https://github.com/a10networks/a10-gui-ugf-template/blob/master/src/index.tsx).

### Main features

1. A10 Root, stores some React context variables
2. A10 Router, a React Router Wrapper
3. A10 Container interface
4. A10 Widget interface
5. Redux Wrapper for HTTP Request
6. CSS infrastructure, we created a unified Less framework, defined colors, font size, etc.

## A10 GUI widget

### What is it?

It's a GUI consisting of small buildable widgets; somewhat like a React Component,  but all stateless.

80% of the components are based on [Ant Design](https://ant.design/) widgets. It has integrated Ant style and A10 customized UI style. We added A10 Widget Interface to extend Ant's widgets. 

### How to make it work?

You need to first install it similarly to how you installed a10-gui-framework. 
Generally these two lines are like fraternal twins. Refer below: 

```javascript
  "dependencies": {
    "a10-gui-framework": "https://github.com/a10networks/a10-gui-framework.git",
    "a10-gui-widgets": "https://github.com/a10networks/a10-gui-widgets.git",
    ...
  }
```

Then call npm install to install. If you come across any issues during installation, please see [A10 GUI Widgets. ](../faq/a10-gui-widgets.md)'s FAQ

Import the widget to your React Container as follows: 

```jsx
import { A10Form, A10Button, A10Input } from 'a10-gui-widgets'
const FormItem = A10Form.Item

export class Form extends A10Container<IFormProps, IFormState> {
  //...
  render() {
    const { onSubmit = _.noop } = this.props
    const { dataA, dataB } = this.state
    return (
        <A10Form layout="horizontal">
          <FormItem label="Field A">
            <A10Input
              placeholder="input placeholder"
              value={dataA}
              onChange={this.onChange.bind(this, 'dataA')}
            />
          </FormItem>
          <FormItem label="Field B">
            <A10Input
              placeholder="input placeholder"
              value={dataB}
              onChange={this.onChange.bind(this, 'dataB')}
            />
          </FormItem>
          <FormItem>
            <A10Button type="primary" onClick={onSubmit}>
              Submit
            </A10Button>
          </FormItem>
        </A10Form>
    )
  }
}
```

### Widgets List

Please refer to [ A10 GUI Widgets](../main-repositories/a10-gui-widgets.md) to see what widgets we have. 

## A10 GUI Common Library <a id="a10-gui-common-library"></a>

### What is it? <a id="what-is-it-2"></a>

A10 Gui Common Library is a common container library. It's different from our widgets library because it has encapsulated business logic inside of it, and it is also decoupled from the app. 

For example, we have decoupling in AutoForm. In AutoForm we need to provide a JSON schema as it's meta data, but since it only depends on A10 CM Schema's definition, we can use the same code for any type of production. 


### How to make it work? <a id="how-to-make-it-work-2"></a>

Let's take AutoForm as the example:

You need to install the a10-gui-common repository first, add the following lines to your package.json, and run npm install command.

```javascript
 "dependencies": {
    "a10-gui-framework": "https://github.com/a10networks/a10-gui-framework.git",
    "a10-gui-widgets": "https://github.com/a10networks/a10-gui-framework.git",
    "a10-gui-common": "https://github.com/a10networks/a10-gui-common.git",
    ...
  }
```

... and then add the following code into your containers

```jsx
import { AutoForm } from 'a10-gui-common'
​
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

For detailed usage about AutoForm, see the [AutoForm usage document.](https://github.com/a10networks/a10-gui-common)​

### Main Containers <a id="main-containers"></a>

#### Used in production containers <a id="used-in-production-containers"></a>

1. AutoForm: generate form by schema
2. AutoLog: generate log analysis dashboard

#### To be added <a id="to-be-added"></a>

1. Wizard : generate wizard
2. Dashboard : generate app dashboard

