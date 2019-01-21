# A10 GUI Widgets

## Introduction  <a id="introduction"></a>

Widgets are common components that are reused across all A10 applications. This widget library is an extension of our `a10-gui-framework` that facilitates the A10 GUI development process. With the sharable widgets under the same framework, different apps can utilize the same structure and codebase. This promotes the maximization of consistency, modularity, and maintainability of A10 applications.

### Repository path:

[https://github.com/a10networks/a10-gui-widgets](https://github.com/a10networks/a10-gui-widgets)

### Install

1.Add a10-gui-widgets to the dependency of package.json

```javascript
 "dependencies": {
    "a10-gui-widgets": "git https://github.com/a10networks/a10-gui-widgets
},
```

2.Install a10-gui-widgets using npm install

3.To use the a10-gui-widgets in your app:

Take the simple A10Button as an example.

```jsx
import { A10Component } from 'a10-gui-framework'
import { A10Button } from 'a10-gui-widgets'

class Demo extends A10Component {
  render() {
    return <A10Button>test</A10Button>
  }
}
export default Demo
```

4.Importing widget css style

There are two ways to import the css of a10-gui-widget in your code.

By Less

```jsx
import '~a10-gui-widgets/dist/index.less'
```

_**NOTE** ~ means importing the less file from node\_modules_

By css

```jsx
import '~a10-gui-widgets/dist/widgets.bundle.css'
```

_**NOTE**: ~ means importing the less file from node\_modules_

### How to use

```jsx
import { A10WidgetLocaleProvider } from 'a10-gui-widgets'
...

return (
  <A10WidgetLocaleProvider locale={A10WidgetLocaleProvider.locales.ja}>
    <App />
  </A10WidgetLocaleProvider>
)
```

​

## Widget contribution

#### 1. Create a widget

First, create a widget package in `src`, for example:

```javascript
src/
  +-- NewWidget/
    +-- styles/
      +-- index.less  // the less style file
    +-- NewWidget.tsx // your source code
    +-- index.tsx     // the output definition file
    +-- README.md     // the README of this widget for using in Storybook
```

**IMPORTANT** When partially importing some widgets from our a10-gui-widgets library, please **DO NOT** import the styles/index.less of the widget in index.tsx. We have a script \(npm build\) to collect all less files of all widgets into the root index.less \('~a10-gui-widgets/dist/index.less'\).

_**NOTE**: Please write your code in alphabetical order._

#### 2.  Export widget component and props in `src/index.tsx`

These widgets are maintained by A10 devs. PRs are welcomed.

* Create a component
* Wrap the component up with the HOC `createWidget` from **a10-gui-framework**

For example, a simple widget:

```jsx
import * as React from 'react'
import { A10Component, createWidget } from 'a10-gui-framework'

class IconButton extends A10Component {
  render() {
    return <div>test</div>
  }
}
export default createWidget(IconButton)
```

#### 3.  Compile Typescript into JavaScript \(ES5\)

```typescript
export * from './NewWidget'
```

_**NOTE**: Please write the code in alphabetical order._

#### 4.  Write storybook for the widget

Add `NewWidget` folder in stories, and create `index.story.js` file in `NewWidget` folder

_**NOTE:** The code of storybook is created by JavaScript \(ES6\) instead of TypeScript._

```javascript
stories/
  +-- NewWidget/
    +-- index.story.js
```

```jsx
import * as React from 'react'
import { withReadme } from 'storybook-readme'
import { Code, CodeComponent, CodeCard } from '../utils'
import { A10NewWidget } from '../../src'
const A10NewWidgetReadme = require('../../src/NewWidget/README.md')

const Example = () => {
  return (
    <CodeComponent>
      <CodeCard
        title="A10NewWidget example title"
        desc="A10NewWidget example description"
        code={<Code string={'code string'} />}
      >
        <A10NewWidget />
      </CodeCard>
    </CodeComponent>
  )
}
export default story => {
  story.add('A10NewWidget', withReadme(A10NewWidgetReadme, Example))
}
```

Import the new story book in `stories/index.stories.js`

```jsx
import createNewWidgetStory from './NewWidget/index.story'

createNewWidgetStory(widgetStory)
```

Run the storybook `npm run storybook` and you will see it at `http://localhost:6006`. \_\_

_**NOTE**: Please write the code in alphabetical order._

#### 5.  Git Push and create a PR.

That's it! Please bear in mind to call `npm build` before submitting your code, and then create a PR for code review at [a10-gui-widgets](https://github.com/a10networks/a10-gui-widgets).

## Widgets   <a id="core-components"></a>

### General

[A10Button](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FGeneral&selectedStory=A10Button&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Icon](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FGeneral&selectedStory=A10Icon&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)

### Layout

[A10Grid](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FLayout&selectedStory=A10Grid&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Layout](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FLayout&selectedStory=A10Layout&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)

### Navigation

[A10Affix](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FNavigation&selectedStory=A10Affix&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Breadcrumb](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FNavigation&selectedStory=A10Breadcrumb&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Dropdown](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FNavigation&selectedStory=A10Dropdown&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10DropdownMenu](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FNavigation&selectedStory=A10DropdownMenu&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Menu](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FNavigation&selectedStory=A10Menu&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10MenuPopover](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FNavigation&selectedStory=A10MenuPopover&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel) [A10Pagination](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FNavigation&selectedStory=A10Pagination&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Steps](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FNavigation&selectedStory=A10Steps&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Explorer](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FNavigation&selectedStory=A10Explorer&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)

### Data Entry

[A10AutoComplete](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10AutoComplete&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Checkbox](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10Checkbox&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Cascader](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10Cascader&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10CompoundConfigList](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10CompoundConfigList&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10CompoundTable ](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10CompoundTable&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel) [A10ConfigList](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10ConfigList&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10DatePicker](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10DatePicker&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Form](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10Form&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10InputNumber](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10InputNumber&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Input](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10Input&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10ListInput](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10ListInput&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Mention](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10Mention&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Rate](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10Rate&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Radio](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10Radio&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Switch](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10Switch&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Silder](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10Slider&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Select](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10Select&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10TreeSelect](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10TreeSelect&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Transfer](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10Transfer&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10TimePicker](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10TimePicker&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel) [A10Upload ](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Entry&selectedStory=A10Upload&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)

### Data Display

[A10Avatar](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Avatar&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Badge](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Badge&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Carousel](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Carousel&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Card](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Card&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Calendar](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Calendar&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Chart](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Chart&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Comment](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Comment&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10ContextMenu ](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10ContextMenu&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel) [A10Collapse](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Collapse&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Datatable](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Datatable&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Diff](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Diff&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10DnDTable](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10DnDTable&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10DnDBasic](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10DnDBasic&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10List](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10List&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10LogFilterBar](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10LogFilterBar&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10LogSearchBar](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10LogSearchBar&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10MultiItem](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10MultiItem&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10MultiSearch](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10MultiSearch&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Popover](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Popover&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10SearchableSelector](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10SearchableSelector&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10SearchBar ](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10SearchBar&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)[A10Table](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Table&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Tabs](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Tabs&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Tag](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Tag&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Timeline](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Timeline&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Tooltip](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Tooltip&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Tree](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FData%20Display&selectedStory=A10Tree&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel) 

### Feedback

[A10Alert](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FFeedback&selectedStory=A10Alert&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Drawer](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FFeedback&selectedStory=A10Drawer&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Modal](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FFeedback&selectedStory=A10Modal&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Message](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FFeedback&selectedStory=A10Message&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Notification](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FFeedback&selectedStory=A10Notification&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Progress](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FFeedback&selectedStory=A10Progress&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Popconfirm](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FFeedback&selectedStory=A10Popconfirm&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10SlidingPage](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FFeedback&selectedStory=A10SlidingPage&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Spin](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FFeedback&selectedStory=A10Spin&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Skeleton](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FFeedback&selectedStory=A10Skeleton&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)

### Other

 [A10Anchor](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FOther&selectedStory=A10Anchor&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10BackTop](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FOther&selectedStory=A10BackTop&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10ConfigProvider](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FOther&selectedStory=A10ConfigProvider&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10Divider](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FOther&selectedStory=A10Divider&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel)  [A10LocaleProvider](https://a10networks.github.io/a10-gui-storybook-widgets/?selectedKind=A10%20Widgets%20%28v1.0.0%29%2FOther&selectedStory=A10LocaleProvider&full=0&addons=1&stories=1&panelRight=1&addonPanel=REACT_STORYBOOK%2Freadme%2Fpanel) 

## ​[FAQ](https://a10-gui.gitbook.io/ugf/faq/a10-gui-framework)​  <a id="faq"></a>

