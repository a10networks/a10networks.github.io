# A10 GUI Widgets

## Introduction <a id="introduction"></a>

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

NOTE: ~ means importing the less file from node\_modules

By css

import '~a10-gui-widgets/dist/widgets.bundle.css'

NOTE: ~ means importing the less file from node\_modules

How to use

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

[A10Affix](../)   A10Alert   A10Anchor   A10AutoComplete   A10Avatar   A10BackTop   A10Badge A10Breadcrumb   A10Button   A10Calendar   A10Card   A10Carousel   A10Cascader   A10Chart A10Checkbox   A10Collapse   A10CompoundConfigList   A10CompoundTable   A10ConfigList A10ContextMenu   A10Datatable   A10DatePicker   A10Diff   A10Divider   A10Dropdown   A10DropdownMenu   A10Explorer   A10Form   A10Grid   A10Icon   A10Input   A10InputNumber   A10Label A10Layout   A10Link   A10List   A10ListInput   A10WidgetLocaleProvider   A10LogFilterBar  A10LogRangeBar   A10LogSearchBar   A10Mention   A10Menu   A10MenuPopover   A10Message A10Modal   A10MultiItem   A10MultiSearch   A10Notification   A10Pagination   A10Popconfirm   A10Popover   A10Progress   A10Radio   A10Rate   A10SearchableSelector   A10SearchBar   A10Select   A10Silder   A10SlidingPage   A10Spin   A10Steps   A10Switch   A10Table   A10Tabs   A10Timeline   A10TimePicker   A10Tooltip   A10Transfer   A10Tree   A10TreeSelect   A10Upload



### def <a id="def"></a>



## Widget contribution

widget guideline

## ​[FAQ](https://a10-gui.gitbook.io/ugf/faq/a10-gui-framework)​ <a id="faq"></a>

