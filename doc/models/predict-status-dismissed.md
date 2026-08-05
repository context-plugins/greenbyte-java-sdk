
# Predict Status Dismissed

Status info for a dismissed Predict alert.

*This model accepts additional fields of type Object.*

## Structure

`PredictStatusDismissed`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `TimestampDismissed` | `LocalDateTime` | Optional | When the alert was dismissed. | LocalDateTime getTimestampDismissed() | setTimestampDismissed(LocalDateTime timestampDismissed) |
| `DismissedBy` | `String` | Optional | The user who dismissed the alert | String getDismissedBy() | setDismissedBy(String dismissedBy) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.PredictStatusDismissed;
import java.io.IOException;

PredictStatusDismissed predictStatusDismissed = new PredictStatusDismissed.Builder()
    .timestampDismissed(DateTimeHelper.fromRfc8601DateTime("2021-01-01T00:00:00"))
    .dismissedBy("Jane Doe")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

