# A10 GUI Widgets

## Introduction <a id="introduction"></a>

 Widgets are common components that are reused across all A10 apps. This widget library is the extension of `a10-gui-framework` to facilitate the A10 GUI development process. With the sharable widgets under the same framework, different apps are using the same structure and codebase. The consistency, modularity, and maintainability of A10 apps are maximized.

### Repo path:

[https://github.com/a10networks/a10-gui-widgets](https://github.com/a10networks/a10-gui-widgets)

### Install

1.Add a10-gui-widgets in the dependency of package.json

```text
 "dependencies": {
    "a10-gui-widgets": "git https://github.com/a10networks/a10-gui-widgets
",
```

2.Install a10-gui-widgets using npm install

3.Using a10-gui-widgets in your app:

Take the simple A10Button as an example.

```text
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

There is two ways to import the css of a10-gui-widget in your code.

By Less

```text
import '~a10-gui-widgets/dist/index.less'
```

_**NOTE** ~ means importing the less file from node\_modules_

By css

import '~a10-gui-widgets/dist/widgets.bundle.css'

_**NOTE**: ~ means importing the less file from node\_modules_

### How to use

```text
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

```text
src/
  +-- NewWidget/
    +-- styles/
      +-- index.less  // the less style file
    +-- NewWidget.tsx // your source code
    +-- index.tsx     // the output definition file
    +-- README.md     // the README of this widget for using in Storybook
```

 **IMPORTANT** For partial widgets importing purpose, please **DO NOT** import the styles/index.less of the widget in index.tsx. We have a script \(npm build\) to collect all less files of all widgets into the root index.less \('~a10-gui-widgets/dist/index.less'\).

 _**NOTE**: Please wirte your code in alphabetical order._

#### 2.  Export widget component and props in `src/index.tsx`

These widgets are maintained by A10 devs. PRs are welcomed.

* Create a component
* Wrap the component up with the HOC `createWidget` from **a10-gui-framework**

For example, a simple widget:

```text
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

```text
export * from './NewWidget'
```

 _**NOTE**: Please wirte the code in alphabetical order._

#### 4.  Write storybook for the widget

 Add `NewWidget` folder in stories, and create `index.story.js` file in `NewWidget` folder

 _**NOTE:** The code of storbook is created by JavaScript \(ES6\) instead of TypeScript._

```text
stories/
  +-- NewWidget/
    +-- index.story.js
```

```text
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

```text
import createNewWidgetStory from './NewWidget/index.story'

createNewWidgetStory(widgetStory)
```

Run the storybook `npm run storybook` and you will see it at `http://localhost:6006`. __

_**NOTE**: Please wirte the code in alphabetical order._ 

#### 5.  Git Push and create a PR.

 That's it!. Please bear in mind doing `npm build` before submitting your code, and then create a PR for code review at [a10-gui-widgets](https://github.com/a10networks/a10-gui-widgets).



## Widgets  <a id="core-components"></a>

[A10Affix ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Affix) [ A10Alert ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Alert)  [A10Anchor](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Anchor)   [A10AutoComplete ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/AutoComplete)  [A10Avatar](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Avatar)   [A10BackTop ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/BackTop)  [A10Badge ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Badge)[A10Breadcrumb ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Breadcrumb)  [A10Button ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Button)  [A10Calendar ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Calendar)  [A10Card](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Card)   [A10Carousel](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Carousel)   [A10Cascader](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Cascader)   [A10Chart ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Chart)[A10Checkbox ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Checkbox)  [A10Collapse](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Collapse)  [ A10CompoundConfigList](https://github.com/a10networks/a10-gui-widgets/tree/master/src/CompoundConfigList)  [ A10CompoundTable](https://github.com/a10networks/a10-gui-widgets/tree/master/src/CompoundTable)   [A10ConfigList ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/ConfigList)[A10ContextMenu](https://github.com/a10networks/a10-gui-widgets/tree/master/src/ContextMenu)  [ A10Datatable](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Datatable)   [A10DatePicker](https://github.com/a10networks/a10-gui-widgets/tree/master/src/DatePicker)   [A10Diff ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Diff)  [A10Divider](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Divider)   [A10Dropdown ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Dropdown)  [A10DropdownMenu](https://github.com/a10networks/a10-gui-widgets/tree/master/src/DropdownMenu)   [A10Explorer](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Explorer)   [A10Form  ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Form) [A10Grid](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Grid)   [A10Icon](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Icon)   [A10Input](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Input)   [A10InputNumber](https://github.com/a10networks/a10-gui-widgets/tree/master/src/InputNumber)   [A10Label ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Label)[A10Layout](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Layout)   [A10Link](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Link)   [A10List ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/List)  [A10ListInput](https://github.com/a10networks/a10-gui-widgets/tree/master/src/ListInput)   [A10WidgetLocaleProvider ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/LocaleProvider)  [A10LogFilterBar  ](https://github.com/a10networks/a10-gui-widgets/blob/master/src/Log/FilterBar/FilterBar.tsx)[A10LogRangeBar ](https://github.com/a10networks/a10-gui-widgets/blob/master/src/Log/RangeBar/RangeBar.tsx)  [A10LogSearchBar](https://github.com/a10networks/a10-gui-widgets/blob/master/src/Log/SearchBar/SearchBar.tsx)   [A10Mention ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Mention) [ A10Menu ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Menu)  [A10MenuPopover ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/MenuPopover) [ A10Message ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Message)[A10Modal](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Modal)   [A10MultiItem ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/MultiItem)  [A10MultiSearch ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/MultiSearch) [ A10Notification ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Notification)  [A10Pagination](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Pagination)   [A10Popconfirm  ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Popconfirm) [A10Popover](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Popover)  [ A10Progress](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Progress)   [A10Radio ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Radio)  [A10Rate](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Rate)   [A10SearchableSelector](https://github.com/a10networks/a10-gui-widgets/tree/master/src/SearchableSelector)   [A10SearchBar](https://github.com/a10networks/a10-gui-widgets/tree/master/src/SearchBar)   [A10Select ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Select)  [A10Silder ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Slider)  [A10SlidingPage ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/SlidingPage)  [A10Spin](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Spin)   [A10Steps ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Steps)  [A10Switch](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Switch)   [A10Table](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Table)   [A10Tabs ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Tabs)  [A10Timeline  ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Timeline) [A10TimePicker](https://github.com/a10networks/a10-gui-widgets/tree/master/src/TimePicker)   [A10TextBadge ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/TextBadge)  [A10Tooltip ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Tooltip)  [A10Transfer](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Transfer)   [A10Tree](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Tree)   [A10TreeSelect ](https://github.com/a10networks/a10-gui-widgets/tree/master/src/TreeSelect)  [A10Upload](https://github.com/a10networks/a10-gui-widgets/tree/master/src/Upload)

## ​[FAQ](https://a10-gui.gitbook.io/ugf/faq/a10-gui-framework)​ <a id="faq"></a>

