
# Alert Item

An alert generated for a device based on a rule.

*This model accepts additional fields of type Object.*

## Structure

`AlertItem`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `DeviceId` | `Integer` | Optional | The id of the device the alert was generated for.<br><br>**Constraints**: `>= 1` | Integer getDeviceId() | setDeviceId(Integer deviceId) |
| `RuleId` | `Integer` | Optional | The id of the rule the alert is based on.<br><br>**Constraints**: `>= 1` | Integer getRuleId() | setRuleId(Integer ruleId) |
| `TimestampStart` | `LocalDateTime` | Optional | The timestamp when the alert began. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampStart() | setTimestampStart(LocalDateTime timestampStart) |
| `TimestampEnd` | `LocalDateTime` | Optional | The timestamp when the alert ended. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampEnd() | setTimestampEnd(LocalDateTime timestampEnd) |
| `Message` | `String` | Optional | The title of the rule the alert is based on. | String getMessage() | setMessage(String message) |
| `Comment` | `String` | Optional | A user comment associated with the alert. | String getComment() | setComment(String comment) |
| `Description` | `String` | Optional | A description explaning the rule the alert is based on. | String getDescription() | setDescription(String description) |
| `Details` | `String` | Optional | Additional details for the alert. Note that the structure of this data is subject to change. | String getDetails() | setDetails(String details) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.AlertItem;
import java.io.IOException;

AlertItem alertItem = new AlertItem.Builder()
    .deviceId(120)
    .ruleId(84)
    .timestampStart(DateTimeHelper.fromRfc8601DateTime("2020-01-01T00:00:00"))
    .timestampEnd(DateTimeHelper.fromRfc8601DateTime("2020-01-08T00:00:00"))
    .message("message8")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

