
# Device Model

General device model information.

*This model accepts additional fields of type Object.*

## Structure

`DeviceModel`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `DeviceModelId` | `Integer` | Optional | - | Integer getDeviceModelId() | setDeviceModelId(Integer deviceModelId) |
| `Manufacturer` | `String` | Optional | - | String getManufacturer() | setManufacturer(String manufacturer) |
| `Model` | `String` | Optional | - | String getModel() | setModel(String model) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.DeviceModel;
import java.io.IOException;

DeviceModel deviceModel = new DeviceModel.Builder()
    .deviceModelId(202)
    .manufacturer("manufacturer4")
    .model("model0")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

