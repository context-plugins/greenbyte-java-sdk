
# Worklog Response 1

*This model accepts additional fields of type Object.*

## Structure

`WorklogResponse1`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `WorklogItemId` | `Integer` | Optional | The id of a worklog item.<br><br>**Constraints**: `>= 1` | Integer getWorklogItemId() | setWorklogItemId(Integer worklogItemId) |
| `Timestamp` | `LocalDateTime` | Optional | The timestamp when the worklog item was entered. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestamp() | setTimestamp(LocalDateTime timestamp) |
| `SiteId` | `Integer` | Optional | The id of a site.<br><br>**Constraints**: `>= 1` | Integer getSiteId() | setSiteId(Integer siteId) |
| `HoursWorked` | `Double` | Optional | The number of hours worked on the worklog item. | Double getHoursWorked() | setHoursWorked(Double hoursWorked) |
| `Comment` | `String` | Optional | The comment related to the worklog item. | String getComment() | setComment(String comment) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.WorklogResponse1;
import java.io.IOException;

WorklogResponse1 worklogResponse1 = new WorklogResponse1.Builder()
    .worklogItemId(198)
    .timestamp(DateTimeHelper.fromRfc8601DateTime("2023-01-01T00:00:00"))
    .siteId(14)
    .hoursWorked(2.5D)
    .comment("Inverter B Offline With Repeated Fault\n- Work Performed: INV B was cleaned\n")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

