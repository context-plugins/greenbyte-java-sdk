
# Sites 429 Error Exception

*This model accepts additional fields of type Object.*

## Structure

`Sites429ErrorException`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `Status` | `int` | Required | - | int getStatus() | setStatus(int status) |
| `Title` | `String` | Required | - | String getTitle() | setTitle(String title) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
try {
    // make the API call
} catch (Sites429ErrorException e) {
    e.printStackTrace();
} catch (ApiException e) {
    e.printStackTrace();
}
```

