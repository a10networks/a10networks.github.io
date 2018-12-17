# A10 GUI Common Library

## Introduction <a id="introduction"></a>

#### Repo path: [https://git.a10networks.com:8443/scm/guinext/a10-gui-common.git](https://lhuo@git.a10networks.com:8443/scm/guinext/a10-gui-common.git) <a id="repo-path"></a>

#### Install <a id="install"></a>

 1. Add `a10-gui-common` into your package.json.

  "a10-gui-common": "[git+https://git.a10networks.com:8443/scm/guinext/a10-gui-common.git](https://git.a10networks.com:8443/projects/GUINEXT/repos/a10-gui-common/null)"

2. Execute `npm i a10-gui-common` 

 `$ npm i a10-gui-common`

 _**NOTE:** `a10-gui-common` requires `a10-gui-framework` and `a10-gui-widgets`_

#### How to use

Usage of Auto-Config Form

```text
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

## Components <a id="core-components"></a>

A10Panel   SubPanel   AsyncComponent   Loading   normalizeVal   normalizeTimestamp   formatDatetime   getHelpPage   prettyMs   browser

### def <a id="def"></a>



## Component contribution

Component guideline





## To do list

what-how



## ​[FAQ](https://a10-gui.gitbook.io/ugf/faq/a10-gui-framework)​ <a id="faq"></a>

