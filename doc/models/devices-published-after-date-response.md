
# Devices Published After Date Response

*This model accepts additional fields of type Object.*

## Structure

`DevicesPublishedAfterDateResponse`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `NumberOfDevices` | `Integer` | Optional | The id of a site. | Integer getNumberOfDevices() | setNumberOfDevices(Integer numberOfDevices) |
| `AuthorizedDeviceIds` | `List<Integer>` | Optional | **Constraints**: `>= 1` | List<Integer> getAuthorizedDeviceIds() | setAuthorizedDeviceIds(List<Integer> authorizedDeviceIds) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.DevicesPublishedAfterDateResponse;
import java.io.IOException;
import java.util.Arrays;

DevicesPublishedAfterDateResponse devicesPublishedAfterDateResponse = new DevicesPublishedAfterDateResponse.Builder()
    .numberOfDevices(142)
    .authorizedDeviceIds(Arrays.asList(
        206,
        207
    ))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

