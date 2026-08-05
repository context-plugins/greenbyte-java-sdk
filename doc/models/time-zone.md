
# Time Zone

*This model accepts additional fields of type Object.*

## Structure

`TimeZone`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `Title` | `String` | Required | The title of the time zone. | String getTitle() | setTitle(String title) |
| `UtcOffset` | `double` | Required | The UTC offset for the time zone. | double getUtcOffset() | setUtcOffset(double utcOffset) |
| `UtcOffsetDst` | `double` | Required | The UTC offset for the time zone during daylight savings time. | double getUtcOffsetDst() | setUtcOffsetDst(double utcOffsetDst) |
| `DstTimestampStart` | `LocalDateTime` | Required | The start of daylight savings time in the time zone. This timestamp is given in UTC. | LocalDateTime getDstTimestampStart() | setDstTimestampStart(LocalDateTime dstTimestampStart) |
| `DstTimestampEnd` | `LocalDateTime` | Required | The end of daylight savings time in the time zone. This timestamp is given in UTC. | LocalDateTime getDstTimestampEnd() | setDstTimestampEnd(LocalDateTime dstTimestampEnd) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.TimeZone;
import java.io.IOException;

TimeZone timeZone = new TimeZone.Builder(
    "Europe/Stockholm",
    1D,
    2D,
    DateTimeHelper.fromRfc8601DateTime("2020-03-29T01:00:00"),
    DateTimeHelper.fromRfc8601DateTime("2020-10-25T01:00:00")
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

