
# Data Signal Configuration

Your data signal configuration. These only apply to wind devices.

*This model accepts additional fields of type Object.*

## Structure

`DataSignalConfiguration`

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
import cloud.greenbyte.intro.models.DataSignalConfiguration;
import java.io.IOException;

DataSignalConfiguration dataSignalConfiguration = new DataSignalConfiguration.Builder(
    40,
    60,
    116,
    212
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

