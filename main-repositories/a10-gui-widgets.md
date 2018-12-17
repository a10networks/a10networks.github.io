# A10 GUI Widgets

## Introduction <a id="introduction"></a>

 Widgets are common components that are reused across all A10 apps. This widget library is the extension of `a10-gui-framework` to facilitate the A10 GUI development process. With the sharable widgets under the same framework, different apps are using the same structure and codebase. The consistency, modularity, and maintainability of A10 apps are maximized.

#### Repo path: [https://git.a10networks.com:8443/scm/guinext/a10-gui-widgets.git](https://git.a10networks.com:8443/scm/guinext/a10-gui-widgets.git) <a id="repo-path"></a>

#### Install <a id="install"></a>

1.Add a10-gui-widgets in the dependency of package.json

```text
 "dependencies": {
    "a10-gui-widgets": "git https://git.a10networks.com:8443/scm/guinext/a10-gui-widgets.git",
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

#### How to use

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

## Widgets  <a id="core-components"></a>

[A10Affix](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Alert](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Anchor](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [ A10AutoComplete](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [ A10Avatar ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src) [ A10BackTop](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Badge ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)[A10Breadcrumb](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Button ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10Calendar](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Card ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10Carousel](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Cascader ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10Chart ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)[A10Checkbox ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10Collapse](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10CompoundConfigList](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10CompoundTable ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10ConfigList ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)[A10ContextMenu](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Datatable](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10DatePicker](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Diff ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10Divider](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Dropdown  ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src) [A10DropdownMenu](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Explorer ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10Form](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Grid](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Icon](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Input ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10InputNumber](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Label ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)[A10Layout  ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src) [A10Link ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10List](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10ListInput](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10WidgetLocaleProvider](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10LogFilterBar](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10LogRangeBar ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10LogSearchBar](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Mention](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Menu](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10MenuPopover](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Message](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src) [A10Modal](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10MultiItem ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10MultiSearch ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10Notification](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Pagination](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Popconfirm ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10Popover](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Progress](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Radio](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Rate](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10SearchableSelector](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [ A10SearchBar](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Select  ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src) [A10Silder ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10SlidingPage ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10Spin](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Steps](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Switch ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10Table](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Tabs](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Timeline ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10TimePicker](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Tooltip  ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src) [A10Transfer  ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src) [A10Tree ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)  [A10TreeSelect](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)   [A10Upload](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/browse/src)

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

 That's it!. Please bear in mind doing `npm build` before submitting your code, and then create a PR for code review at [a10-gui-widgets](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-widgets/).





## ​[FAQ](https://a10-gui.gitbook.io/ugf/faq/a10-gui-framework)​ <a id="faq"></a>

