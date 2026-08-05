
# Data Signal

A data signal.

*This model accepts additional fields of type Object.*

## Structure

`DataSignal`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `DataSignalId` | `int` | Required | The unique id of a data signal.<br><br>**Constraints**: `>= 1` | int getDataSignalId() | setDataSignalId(int dataSignalId) |
| `Title` | `String` | Required | - | String getTitle() | setTitle(String title) |
| `Unit` | `String` | Required | - | String getUnit() | setUnit(String unit) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.DataSignal;
import java.io.IOException;

DataSignal dataSignal = new DataSignal.Builder(
    1,
    "Wind Speed",
    "m/s"
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

