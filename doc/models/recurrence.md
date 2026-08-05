
# Recurrence

Recurrence settings for the task. To calculate when the
task is recurring, use the `timestampStart` field and
then add to it multiples of the specified interval; the
`intervalType` field determines if the task is recurring
on daily, weekly, monthly, or yearly basis.

If the task is not recurring, this field is null.

**Note:** Only the main (first) task in a recurring
series have recurrence settings. For the other tasks in
the series, the field `mainTaskId` can be used to find
it.

*This model accepts additional fields of type Object.*

## Structure

`Recurrence`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `Duration` | `Integer` | Optional | The interval with which the task repeats. | Integer getDuration() | setDuration(Integer duration) |
| `DurationType` | [`DurationType`](../../doc/models/duration-type.md) | Optional | - | DurationType getDurationType() | setDurationType(DurationType durationType) |
| `DateEnd` | `LocalDate` | Optional | When the recurring task series ends (exclusive).<br><br>The end date is **not** included in the<br>recurring task series: for example, to have a<br>task series occur until and including the last<br>day of March 2020, set `dateEnd` to<br>"2020-04-01". | LocalDate getDateEnd() | setDateEnd(LocalDate dateEnd) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.DurationType;
import cloud.greenbyte.intro.models.Recurrence;
import java.io.IOException;

Recurrence recurrence = new Recurrence.Builder()
    .duration(86)
    .durationType(DurationType.DAY)
    .dateEnd(DateTimeHelper.fromSimpleDate("2016-03-13"))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

