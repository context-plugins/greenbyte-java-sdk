
# Predict Status Resolved

Status info for a resolved Predict alert.

*This model accepts additional fields of type Object.*

## Structure

`PredictStatusResolved`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `TimestampResolved` | `LocalDateTime` | Optional | When the alert was resolved. | LocalDateTime getTimestampResolved() | setTimestampResolved(LocalDateTime timestampResolved) |
| `ActionTaken` | `String` | Optional | The action that was taken to resolve the alert. | String getActionTaken() | setActionTaken(String actionTaken) |
| `ComponentResolved` | [`ComponentResolved`](../../doc/models/component-resolved.md) | Optional | - | ComponentResolved getComponentResolved() | setComponentResolved(ComponentResolved componentResolved) |
| `ResolvedBy` | [`PredictAction`](../../doc/models/predict-action.md) | Optional | - | PredictAction getResolvedBy() | setResolvedBy(PredictAction resolvedBy) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.ComponentResolved;
import cloud.greenbyte.intro.models.PredictAction;
import cloud.greenbyte.intro.models.PredictStatusResolved;
import java.io.IOException;

PredictStatusResolved predictStatusResolved = new PredictStatusResolved.Builder()
    .timestampResolved(DateTimeHelper.fromRfc8601DateTime("2021-01-01T00:00:00"))
    .actionTaken("repair")
    .componentResolved(new ComponentResolved.Builder()
        .componentId(52)
        .componentName("componentName2")
        .componentTag("componentTag2")
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
        .build())
    .resolvedBy(PredictAction.NONE)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

