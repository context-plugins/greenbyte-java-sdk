
# Site Access

A site access.

*This model accepts additional fields of type Object.*

## Structure

`SiteAccess`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `SiteAccessId` | `Integer` | Optional | The id of a site access.<br><br>**Constraints**: `>= 1` | Integer getSiteAccessId() | setSiteAccessId(Integer siteAccessId) |
| `SiteId` | `Integer` | Optional | The id of a site.<br><br>**Constraints**: `>= 1` | Integer getSiteId() | setSiteId(Integer siteId) |
| `DeviceIds` | `List<Integer>` | Optional | Device ids associated with the site access.<br><br>**Constraints**: `>= 1` | List<Integer> getDeviceIds() | setDeviceIds(List<Integer> deviceIds) |
| `TaskIds` | `List<Integer>` | Optional | Task ids associated with the site access.<br><br>**Constraints**: `>= 1` | List<Integer> getTaskIds() | setTaskIds(List<Integer> taskIds) |
| `SiteAccessPersonnel` | [`List<SiteAccessPersonnel>`](../../doc/models/site-access-personnel.md) | Optional | Personnel associated with the site access. | List<SiteAccessPersonnel> getSiteAccessPersonnel() | setSiteAccessPersonnel(List<SiteAccessPersonnel> siteAccessPersonnel) |
| `TimestampStart` | `LocalDateTime` | Optional | The timestamp when the site access is/was planned to start. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampStart() | setTimestampStart(LocalDateTime timestampStart) |
| `TimestampEndExpected` | `LocalDateTime` | Optional | The timestamp when the site access is/was planned to end. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampEndExpected() | setTimestampEndExpected(LocalDateTime timestampEndExpected) |
| `TimestampEnd` | `LocalDateTime` | Optional | The timestamp when the site access actually ended. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampEnd() | setTimestampEnd(LocalDateTime timestampEnd) |
| `LogOnComment` | `String` | Optional | A comment for when logging on to the site. | String getLogOnComment() | setLogOnComment(String logOnComment) |
| `LogOffComment` | `String` | Optional | A comment for when logging off from the site. | String getLogOffComment() | setLogOffComment(String logOffComment) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.SiteAccess;
import cloud.greenbyte.intro.models.SiteAccessPersonnel;
import java.io.IOException;
import java.util.Arrays;

SiteAccess siteAccess = new SiteAccess.Builder()
    .siteAccessId(32)
    .siteId(244)
    .deviceIds(Arrays.asList(
        124,
        125
    ))
    .taskIds(Arrays.asList(
        136,
        137,
        138
    ))
    .siteAccessPersonnel(Arrays.asList(
        new SiteAccessPersonnel.Builder()
            .personnelId(170)
            .firstName("firstName4")
            .lastName("lastName2")
            .company("company8")
            .phoneNumber("phoneNumber8")
        .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
            .build()
    ))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

