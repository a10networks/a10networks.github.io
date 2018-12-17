# Unit Test

## How to set value for fields in antform because getFieldsValue is used in codes?  <a id="how-to-set-value-for-fields-in-antform-because-getfieldsvalue-is-used-in-codes"></a>

Solution: use setFieldsValue to set value for fields in antform

```text
  test('import', (done: any) => {    const testComponent = createRemoteImportForm()    const form = testComponent.root.find(      (node: any) => (node.type as any).name === 'RemoteImportForm',    )    form.instance.props.form.setFieldsValue(getFieldsValueImport)    setImmediate(() => {      form.instance.handleImport()      moxios.wait(() => {        expect(form.instance.props.onClose.mock.calls.length).toBe(1)        done()      })    })  })
```

## What is RDD and how to write?  <a id="what-is-rdd-and-how-to-write"></a>

A: RDD = readable driven development

Code:

```text
describe("GIFW Table Test", () =>{      describe("Render the table", () =>{            it("Render Column A", () => {});            .....            it("Render Operation Actions", () => {});      });​      describe("Operate the Table", () =>{            it("Click Delete Button", () => {});            .....            it("Search Filter.", () => {});      });​});
```

## Where is the document for End-to-End and unit test?  <a id="where-is-the-document-for-end-to-end-and-unit-test"></a>

* Unit test: [https://teams.microsoft.com/\_\#/docx/viewer/teams/https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture~2FShared%20Documents~2FGeneral~2Fauto-test~2Funittest\_handbook.docx?threadId=19%3Ae81ccb01ec2e48f9b6f4fd21da53fad6%40thread.skype&baseUrl=https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture&fileId=ED9FF30D-80C8-4C55-A08E-A6C7D3C378DB&ctx=files&viewerAction=view](https://teams.microsoft.com/_#/docx/viewer/teams/https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture~2FShared%20Documents~2FGeneral~2Fauto-test~2Funittest_handbook.docx?threadId=19%3Ae81ccb01ec2e48f9b6f4fd21da53fad6%40thread.skype&baseUrl=https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture&fileId=ED9FF30D-80C8-4C55-A08E-A6C7D3C378DB&ctx=files&viewerAction=view)​
* End-to-End test: [https://teams.microsoft.com/\_\#/docx/viewer/teams/https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture~2FShared%20Documents~2FGeneral~2Fauto-test~2Fe2etest\_handbook.docx?threadId=19%3Ae81ccb01ec2e48f9b6f4fd21da53fad6%40thread.skype&baseUrl=https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture&fileId=CC8F2496-CCCB-4CCF-AA05-CCFE5F8922F7&ctx=files&viewerAction=view](https://teams.microsoft.com/_#/docx/viewer/teams/https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture~2FShared%20Documents~2FGeneral~2Fauto-test~2Fe2etest_handbook.docx?threadId=19%3Ae81ccb01ec2e48f9b6f4fd21da53fad6%40thread.skype&baseUrl=https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture&fileId=CC8F2496-CCCB-4CCF-AA05-CCFE5F8922F7&ctx=files&viewerAction=view)​

## Timeout issue on SubGlobalServerList.text.tsx?  <a id="timeout-issue-on-subglobalserverlist-text-tsx"></a>

In the function 'onUnAssociateSG', serviceGroup API is `/hccapi/v3/provider/${getItem( 'PROVIDER',)}/tenant/${tenant}/shared-object/slb/service-group/${sgName}`. Before testing the function, provider name needs to be initialized. Otherwise, moxios API won't succeed, timeout error will be returned.

```text
 test('should call onUnassociateSg in PortList.tsx work', async (done: any) => {    ;(global as any).sessionStorage.setItem('PROVIDER', 'root')    ;(global as any).sessionStorage.setItem('tenant', 'test')    ;(global as any).sessionStorage.setItem('ALLTENANTS', '[{"name": "test"}]')    mockGetServiceGroupResponse()    mockPostServiceGroupResponse()    const testComponent = renderPortList()    const portListNode = testComponent.root.find(      (node: any) => node.type.name === 'PortList',    )    await portListNode.instance.onUnAssociateSg(      portListProps.data[0],      'httpService1-80',    )    expect(testComponent.toJSON()).toMatchSnapshot()    done()  })
```

## How to test the code having window.location.href?  <a id="how-to-test-the-code-having-window-location-href"></a>

1 Add URL in the jest config

```text
module.exports = {  testURL: 'http://localhost/',
```

2 Use HTML5 history API

```text
window.history.pushState({}, 'Test Title', '/cluster/xyz')
```

## Use Redux state and ignore A10Theme issue and cannot run a10-gui-framework store procedure.  <a id="use-redux-state-and-ignore-a-10-theme-issue-and-cannot-run-a-10-gui-framework-store-procedure"></a>

1 createState

```text
import { Map } from 'immutable'import Settings from 'src/containers/Controller/Dashboard/Settings'​export default () => {  let data = Map()  data = data.setIn(Settings.namespace.dashboardEventInfo, Map(Settings.rangePeriod))  return {    A10Data: data,    A10Theme: Map(),    A10Locale: Map(),  }}
```

2 Use initState={state} in HCProvider to add data to Redux store

```text
const renderTestComponent = () => {  // Init Redux Store  const state = createState()  const ActivitiesList = require('../index').default  return TestRenderer.create(    <HCProvider initState={state>      <ActivitiesList parent="provider" />    </HCProvider>,  )}
```

## How to find your component in the customzied form?  <a id="how-to-find-your-component-in-the-customzied-form"></a>

Solution: find it by name inside the moxios.wait function

1 add it into moxios.wait function

```text
test('function handleItemChange', async () => {  mockAPIResponse()  const testComponent = createGeoListForm()  moxios.wait(() => {    const customForm = testComponent.root.find((node: any) => (node.type as any).name === 'GeoListForm')    let callback = jest.fn()    let item = { name: '' }    customForm.instance.handleItemChange('bj2', item, callback)    expect(item.name).toBe('bj2')    expect(callback.mock.calls.length).toBe(1)  })})
```

2 add it into setImmediate function

```text
test('function handleItemChange', (done: any) => {  mockAPIResponse()  const testComponent = createGeoListForm()  setImmediate(() => {    const customForm = testComponent.root.find((node: any) => (node.type as any).name === 'GeoListForm')    let callback = jest.fn()    let item = { name: '' }    customForm.instance.handleItemChange('bj2', item, callback)    expect(item.name).toBe('bj2')    expect(callback.mock.calls.length).toBe(1)    done()  })})
```

