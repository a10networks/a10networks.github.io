# Main Repositories

## A10 GUI Framework

### What is it?

It's the framework base.

Basically it's a HOC library for React.js and Redux, we encapsulated some core conceptions like container, component and widget,  also some general used features like i18n, feature debugger.

If you want to write your own components and containers, please refer this repository, and include relevant interfaces, example, to contribute an widgets, you can write the code as below

```jsx
import { createA10Widget, A10Component } from 'a10-gui-framework'
class A10Button extends A10Component<IA10ButtonProps> {
}
export default createA10Widget(A10Button)
```

To read more, please see[ A10 GUI Framework.](../main-repositories/a10-gui-framework.md)

### How to make it work?

Since it's not a public repo, you have to add the repository git path to your package.json 

```text
 "dependencies": {
    "a10-gui-framework": "https://github.com/a10networks/a10-gui-framework.git",
    ...
}
```

Then use npm install to install it, if meet troubles on installation, please see FAQ of [A10 GUI Framework](../faq/a10-gui-framework.md).

To setup the bootstrap code, please refer[ a10-gui-ugf-template bootstrap code](https://github.com/a10networks/a10-gui-ugf-template/blob/master/src/index.tsx).

### Main features

1. A10 Root , store some React context variables
2. A10 Router , a React Router Wrapper
3. A10 Container interface
4. A10 Widget interface
5. Redux Wrapper for HTTP Request
6. CSS infrastructure, we created a unified Less framework, defined colors, font size etc.

## A10 GUI widget

### What is it?

It's a GUI smallest blocks, it's a kind of React Component,  but we defined it's stateless.

80% of it's component based on [Ant Design](https://ant.design/) widgets,  it integrated Ant style and A10 customized UI style. We added A10 Widget Interface to extend it. 

### How to make it work?

You need install it first like what a10-gui-framework do, generally these two lines are twins.

```javascript
  "dependencies": {
    "a10-gui-framework": "https://github.com/a10networks/a10-gui-framework.git",
    "a10-gui-widgets": "https://github.com/a10networks/a10-gui-framework.git",
    ...
  }
```

Then use npm install to install it, if meet troubles on installation, please see FAQ of [A10 GUI Widgets. ](../faq/a10-gui-widgets.md)

and then import it from your React Container

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

Please refer[ A10 GUI Widgets](../main-repositories/a10-gui-widgets.md) to know what widgets we have. 

## A10 GUI Stateful Common Library

### What is it?

### How to make it work?

### Main features

