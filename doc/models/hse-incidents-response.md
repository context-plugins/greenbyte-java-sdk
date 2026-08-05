
# Hse Incidents Response

An HSE incident.

*This model accepts additional fields of type Object.*

## Structure

`HseIncidentsResponse`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `HseIncidentId` | `Integer` | Optional | The id of an HSE incident.<br><br>**Constraints**: `>= 1` | Integer getHseIncidentId() | setHseIncidentId(Integer hseIncidentId) |
| `SiteId` | `Integer` | Optional | The id of a site.<br><br>**Constraints**: `>= 1` | Integer getSiteId() | setSiteId(Integer siteId) |
| `DeviceId` | `Integer` | Optional | The id of a device.<br><br>**Constraints**: `>= 1` | Integer getDeviceId() | setDeviceId(Integer deviceId) |
| `Timestamp` | `LocalDateTime` | Optional | The timestamp when the incident occurred.<br>The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestamp() | setTimestamp(LocalDateTime timestamp) |
| `HseCategory` | [`HseCategory`](../../doc/models/hse-category.md) | Optional | - | HseCategory getHseCategory() | setHseCategory(HseCategory hseCategory) |
| `LostTimeInjury` | `Boolean` | Optional | Whether or not the incident resulted in an injury sustained on the job, causing loss of productive work time.<br><br>**Default**: `false` | Boolean getLostTimeInjury() | setLostTimeInjury(Boolean lostTimeInjury) |
| `IncidentDescription` | `String` | Optional | The description related to the incident. | String getIncidentDescription() | setIncidentDescription(String incidentDescription) |
| `Resolved` | `Boolean` | Optional | Whether or not the incident has been resolved.<br><br>**Default**: `false` | Boolean getResolved() | setResolved(Boolean resolved) |
| `ResolvedTimestamp` | `LocalDateTime` | Optional | The timestamp when the incident has been resolved. | LocalDateTime getResolvedTimestamp() | setResolvedTimestamp(LocalDateTime resolvedTimestamp) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.HseCategory;
import cloud.greenbyte.intro.models.HseIncidentsResponse;
import java.io.IOException;

HseIncidentsResponse hseIncidentsResponse = new HseIncidentsResponse.Builder()
    .hseIncidentId(208)
    .siteId(14)
    .deviceId(158)
    .timestamp(DateTimeHelper.fromRfc8601DateTime("2022-12-18T09:45:00"))
    .hseCategory(HseCategory.HAZARDOBSERVATION)
    .lostTimeInjury(false)
    .incidentDescription("Met mast wires are rusty and mast is unstable.")
    .resolved(false)
    .resolvedTimestamp(DateTimeHelper.fromRfc8601DateTime("2022-12-18T11:15:00"))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

