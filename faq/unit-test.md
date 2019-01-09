# Unit Test

## How do I set the values for fields in antform if getFieldsValue is used in the code?

Solution: use setFieldsValue to set value for fields in antform

```typescript
  test('import', (done: any) => {    const testComponent = createRemoteImportForm()    const form = testComponent.root.find(      (node: any) => (node.type as any).name === 'RemoteImportForm',    )    form.instance.props.form.setFieldsValue(getFieldsValueImport)    setImmediate(() => {      form.instance.handleImport()      moxios.wait(() => {        expect(form.instance.props.onClose.mock.calls.length).toBe(1)        done()      })    })  })
```

## What is RDD and how do you write it?

A: RDD = readable driven development

Code:

```typescript
describe("GIFW Table Test", () =>{      describe("Render the table", () =>{            it("Render Column A", () => {});            .....            it("Render Operation Actions", () => {});      });​      describe("Operate the Table", () =>{            it("Click Delete Button", () => {});            .....            it("Search Filter.", () => {});      });​});
```

## Where are the documents for End-to-End and unit testing?

* [Unit test document](https://teams.microsoft.com/_#/docx/viewer/teams/https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture~2FShared%20Documents~2FGeneral~2Fauto-test~2Funittest_handbook.docx?threadId=19%3Ae81ccb01ec2e48f9b6f4fd21da53fad6%40thread.skype&baseUrl=https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture&fileId=ED9FF30D-80C8-4C55-A08E-A6C7D3C378DB&ctx=files&viewerAction=view)​
* [End-to-End test document](https://teams.microsoft.com/_#/docx/viewer/teams/https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture~2FShared%20Documents~2FGeneral~2Fauto-test~2Fe2etest_handbook.docx?threadId=19%3Ae81ccb01ec2e48f9b6f4fd21da53fad6%40thread.skype&baseUrl=https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture&fileId=CC8F2496-CCCB-4CCF-AA05-CCFE5F8922F7&ctx=files&viewerAction=view)​

## Timeout issue on SubGlobalServerList.text.tsx?

In the function 'onUnAssociateSG', serviceGroup API is `/hccapi/v3/provider/${getItem( 'PROVIDER',)}/tenant/${tenant}/shared-object/slb/service-group/${sgName}`. Before testing the function, a provider name needs to be initialized. Otherwise, moxios API will not succeed, and a timeout error will be returned.

```typescript
  test('should call onUnassociateSg in PortList.tsx work', async (done: any) => {
    ;(global as any).sessionStorage.setItem('PROVIDER', 'root')
    ;(global as any).sessionStorage.setItem('tenant', 'test')
    ;(global as any).sessionStorage.setItem('ALLTENANTS', '[{"name": "test"}]')
    mockGetServiceGroupResponse()
    mockPostServiceGroupResponse()
    const testComponent = renderPortList()
    const portListNode = testComponent.root.find(
      (node: any) => node.type.name === 'PortList',
    )
    await portListNode.instance.onUnAssociateSg(
      portListProps.data[0],
      'httpService1-80',
    )
    expect(testComponent.toJSON()).toMatchSnapshot()
    done()
  })
```

## How  do I test if the code has window.location.href?

1 Add a URL to the jest config

```typescript
module.exports = {  testURL: 'http://localhost/',
```

2 Use HTML5 history API

```typescript
window.history.pushState({}, 'Test Title', '/cluster/xyz')
```

## If you are using Redux state, ignoring A10Theme issue, and cannot run a10-gui-framework store procedure

1 createState

```typescript
import { Map } from 'immutable'
import Settings from 'src/containers/Controller/Dashboard/Settings'

export default () => {
  let data = Map()
  data = data.setIn(Settings.namespace.dashboardEventInfo, Map(Settings.rangePeriod))
  return {
    A10Data: data,
    A10Theme: Map(),
    A10Locale: Map(),
  }
}
```

2 Use initState={state} in HCProvider to add data to Redux store

```typescript
const renderTestComponent = () => {
  // Init Redux Store
  const state = createState()
  const ActivitiesList = require('../index').default
  return TestRenderer.create(
    <HCProvider initState={state>
      <ActivitiesList parent="provider" />
    </HCProvider>,
  )
}
```

## How do I prevent a 'Network Issue' error when running unit test code?

Use a try cach block for the source code.

## How do I find your component in the customized form?

Solution: find it by name inside the moxios.wait function

1 add it into moxios.wait function

```typescript
test('function handleItemChange', async () => {
  mockAPIResponse()
  const testComponent = createGeoListForm()
  moxios.wait(() => {
    const customForm = testComponent.root.find((node: any) => (node.type as any).name === 'GeoListForm')
    let callback = jest.fn()
    let item = { name: '' }
    customForm.instance.handleItemChange('bj2', item, callback)
    expect(item.name).toBe('bj2')
    expect(callback.mock.calls.length).toBe(1)
  })
})
```

2 add it into setImmediate function

```typescript
test('function handleItemChange', (done: any) => {
  mockAPIResponse()
  const testComponent = createGeoListForm()
  setImmediate(() => {
    const customForm = testComponent.root.find((node: any) => (node.type as any).name === 'GeoListForm')
    let callback = jest.fn()
    let item = { name: '' }
    customForm.instance.handleItemChange('bj2', item, callback)
    expect(item.name).toBe('bj2')
    expect(callback.mock.calls.length).toBe(1)
    done()
  })
})
```

