# Troubleshooting

{% api-method method="get" host="https://api.cakes.com" path="/v1/cakes/:id" %}
{% api-method-summary %}
Get Cakes
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get free cakes.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="boolean" %}
ID of the cake to get, for free of course.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Authentication token to track down who is emptying our stocks.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="recipe" type="string" %}
The API will do its best to find a cake matching the provided recipe.
{% endapi-method-parameter %}

{% api-method-parameter name="gluten" type="boolean" %}
Whether the cake should be gluten-free or not.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Cake successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
    "name": "Cake's name",
    "recipe": "Cake's recipe name",
    "cake": "Binary cake"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a cake matching this query.
{% endapi-method-response-example-description %}

```javascript
{
    "message": "Ain't no cake like that."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Git trouble-shooting

**Filename being too long**

```text
$ git reset HEAD --hard
error: unable to create file src/metaComponents/cm/System/ResourceAccounting/ResourceAccounting.Oper/ResourceAccounting.Oper.PartitionResource/ResourceAccountingOper.Oper.ResType/ResourceAccountingOperOper.Oper.Resources/ResourceAccountingOperOper.Oper.Resources.gen.tsx: Filename too long
fatal: Could not reset index file to revision 'HEAD'.
```

 Solution - run the following command:

```text
git config --system core.longpaths true
```

 Please note that you may need `sudo` privilege to run it.

```text
$ git config --system core.longpaths true
error: could not lock config file C:\Program Files\Git\mingw64/etc/gitconfig: Permission denied
```

 If you see such message above in Windows, run `cmd` with system admin role.

