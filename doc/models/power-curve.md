
# Power Curve

*This model accepts additional fields of type Object.*

## Structure

`PowerCurve`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `DeviceId` | `int` | Required | The id of a device.<br><br>**Constraints**: `>= 1` | int getDeviceId() | setDeviceId(int deviceId) |
| `Title` | `String` | Required | The title of the power curve. | String getTitle() | setTitle(String title) |
| `Values` | [`List<PowerCurveValue>`](../../doc/models/power-curve-value.md) | Required | - | List<PowerCurveValue> getValues() | setValues(List<PowerCurveValue> values) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.PowerCurve;
import cloud.greenbyte.intro.models.PowerCurveValue;
import java.io.IOException;
import java.util.Arrays;

PowerCurve powerCurve = new PowerCurve.Builder(
    30,
    "title8",
    Arrays.asList(
        new PowerCurveValue.Builder(
            28.46D,
            248.04D
        )
        .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
        .build()
    )
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

