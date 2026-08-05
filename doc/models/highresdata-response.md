
# Highresdata Response

An object containing a single data point for a specific device and data signal.

*This model accepts additional fields of type Object.*

## Structure

`HighresdataResponse`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `DeviceId` | `int` | Required | The id of a device.<br><br>**Constraints**: `>= 1` | int getDeviceId() | setDeviceId(int deviceId) |
| `DataSignal` | [`DataSignal1`](../../doc/models/data-signal-1.md) | Required | - | DataSignal1 getDataSignal() | setDataSignal(DataSignal1 dataSignal) |
| `Data` | `Map<String, Double>` | Required | One or more key value pairs with timestamp as key and the data measurement as value. The timestamps are in UTC. | Map<String, Double> getData() | setData(Map<String, Double> data) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.DataSignal1;
import cloud.greenbyte.intro.models.HighresdataResponse;
import java.io.IOException;
import java.util.LinkedHashMap;

HighresdataResponse highresdataResponse = new HighresdataResponse.Builder(
    102,
    new DataSignal1.Builder(
        24,
        "title8",
        "unit4"
    )
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build(),
    new LinkedHashMap<String, Double>() {{
        put("2021-04-09T04:14:18Z", 5.81789970397949D);
        put("2021-04-09T04:14:48Z", 5.43127489089966D);
        put("2021-04-09T04:15:18Z", 7.41247510910034D);
        put("2021-04-09T04:15:48Z", 5.58427476882935D);
    }}
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

