
# Data Real Time Item

An object containing a single data point for a specific aggregate, data signal and interval.

*This model accepts additional fields of type Object.*

## Structure

`DataRealTimeItem`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `Aggregate` | [`AggregateMode`](../../doc/models/aggregate-mode.md) | Required | - | AggregateMode getAggregate() | setAggregate(AggregateMode aggregate) |
| `AggregateId` | `int` | Required | The id of this aggregate group: device id, site id, or the constant -1 for portfolio. For `siteLevel` aggregation a generated unique id is used. | int getAggregateId() | setAggregateId(int aggregateId) |
| `AggregatePathNames` | `List<String>` | Optional | For `siteLevel` aggregation this contains the title for each level in the hierarchy. For other types of aggregation it will be empty. | List<String> getAggregatePathNames() | setAggregatePathNames(List<String> aggregatePathNames) |
| `DeviceIds` | `List<Integer>` | Required | The ids of the devices in this aggregate group.<br><br>**Constraints**: `>= 1` | List<Integer> getDeviceIds() | setDeviceIds(List<Integer> deviceIds) |
| `Calculation` | [`CalculationModeRealTime`](../../doc/models/calculation-mode-real-time.md) | Required | - | CalculationModeRealTime getCalculation() | setCalculation(CalculationModeRealTime calculation) |
| `DataSignal` | [`DataSignal1`](../../doc/models/data-signal-1.md) | Required | - | DataSignal1 getDataSignal() | setDataSignal(DataSignal1 dataSignal) |
| `Data` | `Map<String, Double>` | Required | A single key value pair with timestamp as key and the data measurement as value. The timestamps are in UTC. | Map<String, Double> getData() | setData(Map<String, Double> data) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.AggregateMode;
import cloud.greenbyte.intro.models.CalculationModeRealTime;
import cloud.greenbyte.intro.models.DataRealTimeItem;
import cloud.greenbyte.intro.models.DataSignal1;
import java.io.IOException;
import java.util.Arrays;
import java.util.LinkedHashMap;

DataRealTimeItem dataRealTimeItem = new DataRealTimeItem.Builder(
    AggregateMode.DEVICE,
    190,
    Arrays.asList(
        220
    ),
    CalculationModeRealTime.AVERAGE,
    new DataSignal1.Builder(
        24,
        "title8",
        "unit4"
    )
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build(),
    new LinkedHashMap<String, Double>() {{
        put("2020-01-01T00:00:00Z", 584.33D);
    }}
)
.aggregatePathNames(Arrays.asList(
        "aggregatePathNames0"
    ))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

