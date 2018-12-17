# A10 GUI Framework

## Introduction

A10 GUI Framework is based on modern web design. At the heart of it, we leverage a component based front-end JavaScript framework called React.jsi. Together with Reduxii and our proposals embodied in a set of design patterns, we believe this will go a long way to providing a set of tools to build appealing, modern, and consistent web UI with relative ease and simplicity.

#### Repo path: [https://git.a10networks.com:8443/scm/guinext/a10-gui-framework.git](https://git.a10networks.com:8443/scm/guinext/a10-gui-framework.git)

#### Install

$ npm i -S git+https://git.a10networks.com:8443/scm/guinext/a10-gui-framework.git

#### How to use

Quick start for using a10-gui-framework

```text
// approot/index.ts
import React from 'react'
import ReactDOM from 'react-dom'
import { A10Provider, A10Router } from 'a10-gui-framework'

import CONFIG from 'approot/configs/global'
import middlewares from 'approot/redux/middlewares'
import reducers from 'approot/redux/reducers'
import APP from 'approot/containers/App'

const initState = {}
ReactDOM.render(
  <A10Provider
    CONFIG={CONFIG}
    middlewares={middlewares}
    reducers={reducers}
    initState={initState}
  >
    <A10Router.Browser>
      <APP />
    </A10Router.Browser>
  </A10Provider>,
  document.getElementById('root'),
)
```

## Core components 

[A10Provider](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-framework/browse/src/appComponents)   [A10Router ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-framework/browse/src/appComponents)  [A10Route ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-framework/browse/src/appComponents) [ A10Switch](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-framework/browse/src/appComponents)   [A10Root](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-framework/browse/src/appComponents)   [A10Component ](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-framework/browse/src/basicComponents/index.tsx)  [A10Container](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-framework/browse/src/basicComponents/index.tsx)







[Design document](https://github.com/a10networks/a10networks.github.io/blob/0.7.0/design-docs/A10-GUI-Framework-Design-v1.1a.docx)

### 





## [FAQ](https://a10-gui.gitbook.io/ugf/faq/a10-gui-framework)

### 



