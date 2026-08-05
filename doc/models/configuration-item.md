
# Configuration Item

Your configuration data.

*This model accepts additional fields of type Object.*

## Structure

`ConfigurationItem`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `Client` | [`Client`](../../doc/models/client.md) | Required | - | Client getClient() | setClient(Client client) |
| `TimeZone` | [`TimeZone`](../../doc/models/time-zone.md) | Required | - | TimeZone getTimeZone() | setTimeZone(TimeZone timeZone) |
| `DataSignals` | [`DataSignals`](../../doc/models/data-signals.md) | Required | - | DataSignals getDataSignals() | setDataSignals(DataSignals dataSignals) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.Client;
import cloud.greenbyte.intro.models.ConfigurationItem;
import cloud.greenbyte.intro.models.DataSignals;
import cloud.greenbyte.intro.models.TimeZone;
import java.io.IOException;

ConfigurationItem configurationItem = new ConfigurationItem.Builder(
    new Client.Builder(
        "intro",
        "intro",
        "https://intro.greenbyte.cloud/",
        "https://intro.greenbyte.cloud/api/2/"
    )
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build(),
    new TimeZone.Builder(
        "Europe/Stockholm",
        1D,
        2D,
        DateTimeHelper.fromRfc8601DateTime("2020-03-29T01:00:00"),
        DateTimeHelper.fromRfc8601DateTime("2020-10-25T01:00:00")
    )
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build(),
    new DataSignals.Builder(
        202,
        74,
        130,
        30
    )
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build()
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

