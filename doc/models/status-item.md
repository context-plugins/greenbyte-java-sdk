
# Status Item

A status that may contain statuses of the same type as sub-statuses. Note that for sub-statuses the fields `categoryIec`, `categoryContract`, and `subStatus` will always be null.

*This model accepts additional fields of type Object.*

## Structure

`StatusItem`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `TurbineStatusId` | `Integer` | Optional | The id of a turbine status.<br><br>**Constraints**: `>= 1` | Integer getTurbineStatusId() | setTurbineStatusId(Integer turbineStatusId) |
| `DeviceId` | `Integer` | Optional | The id of a device.<br><br>**Constraints**: `>= 1` | Integer getDeviceId() | setDeviceId(Integer deviceId) |
| `TimestampStart` | `LocalDateTime` | Optional | The timestamp when the status began. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampStart() | setTimestampStart(LocalDateTime timestampStart) |
| `TimestampEnd` | `LocalDateTime` | Optional | The timestamp when the status ended. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampEnd() | setTimestampEnd(LocalDateTime timestampEnd) |
| `HasTimestampEnd` | `Boolean` | Optional | Indicates whether the status has a duration. | Boolean getHasTimestampEnd() | setHasTimestampEnd(Boolean hasTimestampEnd) |
| `Category` | [`StatusCategory`](../../doc/models/status-category.md) | Optional | - | StatusCategory getCategory() | setCategory(StatusCategory category) |
| `Code` | `Integer` | Optional | The status code. | Integer getCode() | setCode(Integer code) |
| `Message` | `String` | Optional | A description of the status code. | String getMessage() | setMessage(String message) |
| `Comment` | `String` | Optional | A user comment associated with the status. | String getComment() | setComment(String comment) |
| `LostProductionSignal` | [`LostProductionSignal`](../../doc/models/lost-production-signal.md) | Optional | - | LostProductionSignal getLostProductionSignal() | setLostProductionSignal(LostProductionSignal lostProductionSignal) |
| `LostProduction` | `Double` | Optional | The lost production in kWh associated with the status. This field<br>will be null if the caller is not authorized for the system-configured<br>lost production signal. The configured lost production signal is available<br>via the `/configuration.json` endpoint (`DataSignalConfiguration` schema). | Double getLostProduction() | setLostProduction(Double lostProduction) |
| `CategoryIec` | `String` | Optional | The status category as defined by the IEC. | String getCategoryIec() | setCategoryIec(String categoryIec) |
| `CategoryContract` | `String` | Optional | The status category as defined in the service availability contract assigned to the site. | String getCategoryContract() | setCategoryContract(String categoryContract) |
| `CategoryGlobalContract` | `String` | Optional | The status category as defined in the global availability contract assigned to the site. | String getCategoryGlobalContract() | setCategoryGlobalContract(String categoryGlobalContract) |
| `CategoryCustomContract` | `String` | Optional | The status category as defined in the custom availability contract assigned to the site. | String getCategoryCustomContract() | setCategoryCustomContract(String categoryCustomContract) |
| `SubStatus` | [`List<StatusItem>`](../../doc/models/status-item.md) | Optional | Statuses of the same type that have been grouped under this status. | List<StatusItem> getSubStatus() | setSubStatus(List<StatusItem> subStatus) |
| `Acknowledged` | `Boolean` | Optional | Indicates whether the status has been acknowledged. | Boolean getAcknowledged() | setAcknowledged(Boolean acknowledged) |
| `Component` | `Object` | Optional | The status component categorization. | Object getComponent() | setComponent(Object component) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.StatusItem;
import java.io.IOException;

StatusItem statusItem = new StatusItem.Builder()
    .turbineStatusId(6)
    .deviceId(120)
    .timestampStart(DateTimeHelper.fromRfc8601DateTime("2020-01-01T00:00:00"))
    .timestampEnd(DateTimeHelper.fromRfc8601DateTime("2020-01-08T00:00:00"))
    .hasTimestampEnd(false)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

