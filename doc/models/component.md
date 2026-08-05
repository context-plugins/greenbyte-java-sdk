
# Component

A component of a wind turbine.

*This model accepts additional fields of type Object.*

## Structure

`Component`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `ComponentId` | `Integer` | Optional | - | Integer getComponentId() | setComponentId(Integer componentId) |
| `ComponentName` | `String` | Optional | The name of the component. | String getComponentName() | setComponentName(String componentName) |
| `ComponentTag` | `String` | Optional | The component tag. | String getComponentTag() | setComponentTag(String componentTag) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.Component;
import java.io.IOException;

Component component = new Component.Builder()
    .componentId(100)
    .componentName("Nacelle")
    .componentTag("MDK30 QL001")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

