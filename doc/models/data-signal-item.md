
# Data Signal Item

A data signal, including type.

*This model accepts additional fields of type Object.*

## Structure

`DataSignalItem`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `DataSignalId` | `int` | Required | The unique id of a data signal.<br><br>**Constraints**: `>= 1` | int getDataSignalId() | setDataSignalId(int dataSignalId) |
| `Title` | `String` | Required | - | String getTitle() | setTitle(String title) |
| `Type` | `String` | Required | - | String getType() | setType(String type) |
| `Unit` | `String` | Required | - | String getUnit() | setUnit(String unit) |
| `DeviceType` | `Object` | Optional | - | Object getDeviceType() | setDeviceType(Object deviceType) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.DataSignalItem;
import java.io.IOException;

DataSignalItem dataSignalItem = new DataSignalItem.Builder(
    1,
    "Wind speed",
    "Wind speed",
    "m/s"
)
.deviceType(ApiHelper.deserialize("{\"deviceTypeId\":1,\"title\":\"Turbine\"}"))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

