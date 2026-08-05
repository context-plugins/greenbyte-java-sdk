
# Downtime Events Response

*This model accepts additional fields of type Object.*

## Structure

`DowntimeEventsResponse`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `DowntimeEventId` | `Integer` | Optional | The id of a downtime event.<br><br>**Constraints**: `>= 1` | Integer getDowntimeEventId() | setDowntimeEventId(Integer downtimeEventId) |
| `TimestampStart` | `LocalDateTime` | Optional | The timestamp when the downtime is/was planned to start. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampStart() | setTimestampStart(LocalDateTime timestampStart) |
| `TimestampEnd` | `LocalDateTime` | Optional | The timestamp when the downtime is/was planned to end. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampEnd() | setTimestampEnd(LocalDateTime timestampEnd) |
| `Comment` | `String` | Optional | A comment describing the downtime event. | String getComment() | setComment(String comment) |
| `DeviceIds` | `List<Integer>` | Optional | **Constraints**: `>= 1` | List<Integer> getDeviceIds() | setDeviceIds(List<Integer> deviceIds) |
| `SiteIds` | `List<Integer>` | Optional | **Constraints**: `>= 1` | List<Integer> getSiteIds() | setSiteIds(List<Integer> siteIds) |
| `TaskIds` | `List<Integer>` | Optional | **Constraints**: `>= 1` | List<Integer> getTaskIds() | setTaskIds(List<Integer> taskIds) |
| `RemainingCapacityPercentage` | `Double` | Optional | - | Double getRemainingCapacityPercentage() | setRemainingCapacityPercentage(Double remainingCapacityPercentage) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.DowntimeEventsResponse;
import java.io.IOException;
import java.util.Arrays;

DowntimeEventsResponse downtimeEventsResponse = new DowntimeEventsResponse.Builder()
    .downtimeEventId(192)
    .timestampStart(DateTimeHelper.fromRfc8601DateTime("2020-01-01T00:00:00"))
    .timestampEnd(DateTimeHelper.fromRfc8601DateTime("2020-01-08T00:00:00"))
    .comment("comment6")
    .deviceIds(Arrays.asList(
        250,
        251
    ))
    .remainingCapacityPercentage(50.5D)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

