
# Device Type

*This model accepts additional fields of type Object.*

## Structure

`DeviceType`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `DeviceTypeId` | `Integer` | Optional | The id of a device type.<br><br>**Constraints**: `>= 1` | Integer getDeviceTypeId() | setDeviceTypeId(Integer deviceTypeId) |
| `Title` | `String` | Optional | The string representation of the device type. | String getTitle() | setTitle(String title) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.DeviceType;
import java.io.IOException;

DeviceType deviceType = new DeviceType.Builder()
    .deviceTypeId(216)
    .title("Turbine")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

