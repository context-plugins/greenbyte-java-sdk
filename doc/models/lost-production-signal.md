
# Lost Production Signal

*This model accepts additional fields of type Object.*

## Structure

`LostProductionSignal`

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
import cloud.greenbyte.intro.models.LostProductionSignal;
import java.io.IOException;

LostProductionSignal lostProductionSignal = new LostProductionSignal.Builder(
    208,
    "title6",
    "unit8"
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

