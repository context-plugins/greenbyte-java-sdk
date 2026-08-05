
# Data Item

An object containing time-series data for a specific aggregate, data signal and interval.

*This model accepts additional fields of type Object.*

## Structure

`DataItem`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `Aggregate` | [`AggregateMode`](../../doc/models/aggregate-mode.md) | Required | - | AggregateMode getAggregate() | setAggregate(AggregateMode aggregate) |
| `AggregateId` | `int` | Required | The id of this aggregate group: device id, site id, or the constant -1 for portfolio. For `siteLevel` aggregation a generated unique id is used. | int getAggregateId() | setAggregateId(int aggregateId) |
| `AggregatePathNames` | `List<String>` | Optional | For `siteLevel` aggregation this contains the title for each level in the hierarchy. For other types of aggregation it will be empty. | List<String> getAggregatePathNames() | setAggregatePathNames(List<String> aggregatePathNames) |
| `DeviceIds` | `List<Integer>` | Required | The ids of the devices in this aggregate group.<br><br>**Constraints**: `>= 1` | List<Integer> getDeviceIds() | setDeviceIds(List<Integer> deviceIds) |
| `Resolution` | [`Resolution`](../../doc/models/resolution.md) | Required | - | Resolution getResolution() | setResolution(Resolution resolution) |
| `Calculation` | [`CalculationMode`](../../doc/models/calculation-mode.md) | Required | - | CalculationMode getCalculation() | setCalculation(CalculationMode calculation) |
| `DataSignal` | [`DataSignal1`](../../doc/models/data-signal-1.md) | Required | - | DataSignal1 getDataSignal() | setDataSignal(DataSignal1 dataSignal) |
| `Data` | `Map<String, Double>` | Required | A dictionary with the **timestamp** as key and the **data measurement** as value.<br><br>The format of the timestamp(s) depends on the **useUtc** attribute you specified in the request.<br><br>In case you specified `useUtc = true` you will get the timestamps in UTC format. Example:<br><br>```<br>{<br>"2022-05-01T00:00:00Z": 8.1,<br>"2022-05-01T00:10:00Z": 6.9,<br>"2022-05-01T00:20:00Z": 6.6,<br>...<br>```<br><br>If you omitted the **useUtc** attribute (*default is* `false`) or you explicitly specified it to `false` you will get the timestamps in the time zone configured in the Greenbyte Platform, in the format stated in the example. Example:<br><br>```<br>{<br>"2022-05-01T02:00:00": 8.1,<br>"2022-05-01T02:10:00": 6.9,<br>"2022-05-01T02:20:00": 6.6,<br>...<br>```<br><br>**Attention**: please notice the lack of the letter `Z` at the end of the timestamp. Also, the configured time zone for the given example is *UTC+2*. | Map<String, Double> getData() | setData(Map<String, Double> data) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.AggregateMode;
import cloud.greenbyte.intro.models.CalculationMode;
import cloud.greenbyte.intro.models.DataItem;
import cloud.greenbyte.intro.models.DataSignal1;
import cloud.greenbyte.intro.models.Resolution;
import java.io.IOException;
import java.util.Arrays;
import java.util.LinkedHashMap;

DataItem dataItem = new DataItem.Builder(
    AggregateMode.DEVICE,
    212,
    Arrays.asList(
        242,
        243
    ),
    Resolution.MONTHLY,
    CalculationMode.SUM,
    new DataSignal1.Builder(
        24,
        "title8",
        "unit4"
    )
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build(),
    new LinkedHashMap<String, Double>() {{
        put("key0", 153.67D);
    }}
)
.aggregatePathNames(Arrays.asList(
        "aggregatePathNames0",
        "aggregatePathNames9",
        "aggregatePathNames8"
    ))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

