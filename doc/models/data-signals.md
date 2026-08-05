
# Data Signals

*This model accepts additional fields of type Object.*

## Structure

`DataSignals`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `AvailabilityTimeDataSignalId` | `int` | Required | The id of the data signal used for time-based availability data.<br><br>**Constraints**: `>= 1` | int getAvailabilityTimeDataSignalId() | setAvailabilityTimeDataSignalId(int availabilityTimeDataSignalId) |
| `AvailabilityProductionDataSignalId` | `int` | Required | The id of the data signal used for production-based availability data.<br><br>**Constraints**: `>= 1` | int getAvailabilityProductionDataSignalId() | setAvailabilityProductionDataSignalId(int availabilityProductionDataSignalId) |
| `LostProductionDataSignalId` | `int` | Required | The id of the data signal used for lost production data.<br><br>**Constraints**: `>= 1` | int getLostProductionDataSignalId() | setLostProductionDataSignalId(int lostProductionDataSignalId) |
| `PerformanceDataSignalId` | `int` | Required | The id of the data signal used for performance data.<br><br>**Constraints**: `>= 1` | int getPerformanceDataSignalId() | setPerformanceDataSignalId(int performanceDataSignalId) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.DataSignals;
import java.io.IOException;

DataSignals dataSignals = new DataSignals.Builder(
    202,
    74,
    130,
    30
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

