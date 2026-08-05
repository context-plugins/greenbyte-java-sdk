
# Predict Comment

A comment on a Predict alert.

*This model accepts additional fields of type Object.*

## Structure

`PredictComment`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `UserName` | `String` | Optional | - | String getUserName() | setUserName(String userName) |
| `Text` | `String` | Optional | - | String getText() | setText(String text) |
| `Timestamp` | `LocalDateTime` | Optional | - | LocalDateTime getTimestamp() | setTimestamp(LocalDateTime timestamp) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.PredictComment;
import java.io.IOException;

PredictComment predictComment = new PredictComment.Builder()
    .userName("userName0")
    .text("text8")
    .timestamp(DateTimeHelper.fromRfc8601DateTime("2020-01-01T00:00:00"))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

