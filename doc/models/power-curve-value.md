
# Power Curve Value

The power at a specific wind speed according to a power curve.

*This model accepts additional fields of type Object.*

## Structure

`PowerCurveValue`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `WindSpeed` | `double` | Required | Wind speed in m/s | double getWindSpeed() | setWindSpeed(double windSpeed) |
| `Power` | `double` | Required | Power in kW | double getPower() | setPower(double power) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.PowerCurveValue;
import java.io.IOException;

PowerCurveValue powerCurveValue = new PowerCurveValue.Builder(
    178.98D,
    142.56D
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

