
# Device Accesses Response

*This model accepts additional fields of type Object.*

## Structure

`DeviceAccessesResponse`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `DeviceAccessId` | `Integer` | Optional | The id of a device access.<br><br>**Constraints**: `>= 1` | Integer getDeviceAccessId() | setDeviceAccessId(Integer deviceAccessId) |
| `SiteAccessId` | `Integer` | Optional | The id of a site access.<br><br>**Constraints**: `>= 1` | Integer getSiteAccessId() | setSiteAccessId(Integer siteAccessId) |
| `SiteId` | `Integer` | Optional | The id of a site.<br><br>**Constraints**: `>= 1` | Integer getSiteId() | setSiteId(Integer siteId) |
| `DeviceIds` | `List<Integer>` | Optional | The associated device ids.<br><br>**Constraints**: `>= 1` | List<Integer> getDeviceIds() | setDeviceIds(List<Integer> deviceIds) |
| `PersonnelIds` | `List<Integer>` | Optional | The associated personnel ids.<br><br>**Constraints**: `>= 1` | List<Integer> getPersonnelIds() | setPersonnelIds(List<Integer> personnelIds) |
| `TaskIds` | `List<Integer>` | Optional | The associated task ids.<br><br>**Constraints**: `>= 1` | List<Integer> getTaskIds() | setTaskIds(List<Integer> taskIds) |
| `TimestampStart` | `LocalDateTime` | Optional | The timestamp when the device access is/was planned to start. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampStart() | setTimestampStart(LocalDateTime timestampStart) |
| `TimestampEndExpected` | `LocalDateTime` | Optional | The timestamp when the device access is/was planned to end. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampEndExpected() | setTimestampEndExpected(LocalDateTime timestampEndExpected) |
| `TimestampEnd` | `LocalDateTime` | Optional | The timestamp when the device access actually ended. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampEnd() | setTimestampEnd(LocalDateTime timestampEnd) |
| `LogOnComment` | `String` | Optional | A comment for when logging on to the device. | String getLogOnComment() | setLogOnComment(String logOnComment) |
| `LogOffComment` | `String` | Optional | A comment for when logging off from the device. | String getLogOffComment() | setLogOffComment(String logOffComment) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.DeviceAccessesResponse;
import java.io.IOException;
import java.util.Arrays;

DeviceAccessesResponse deviceAccessesResponse = new DeviceAccessesResponse.Builder()
    .deviceAccessId(168)
    .siteAccessId(196)
    .siteId(16)
    .deviceIds(Arrays.asList(
        96,
        97,
        98
    ))
    .personnelIds(Arrays.asList(
        196,
        197
    ))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

