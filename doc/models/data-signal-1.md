
# Data Signal 1

*This model accepts additional fields of type Object.*

## Structure

`DataSignal1`

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
import cloud.greenbyte.intro.models.DataSignal1;
import java.io.IOException;

DataSignal1 dataSignal1 = new DataSignal1.Builder(
    34,
    "title2",
    "unit4"
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

