
# Site Access Personnel

Site access personnel.

*This model accepts additional fields of type Object.*

## Structure

`SiteAccessPersonnel`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `PersonnelId` | `Integer` | Optional | The id of a person in the personnel list.<br><br>**Constraints**: `>= 1` | Integer getPersonnelId() | setPersonnelId(Integer personnelId) |
| `FirstName` | `String` | Optional | - | String getFirstName() | setFirstName(String firstName) |
| `LastName` | `String` | Optional | - | String getLastName() | setLastName(String lastName) |
| `Company` | `String` | Optional | - | String getCompany() | setCompany(String company) |
| `PhoneNumber` | `String` | Optional | - | String getPhoneNumber() | setPhoneNumber(String phoneNumber) |
| `VehicleRegistration` | `String` | Optional | - | String getVehicleRegistration() | setVehicleRegistration(String vehicleRegistration) |
| `Comment` | `String` | Optional | - | String getComment() | setComment(String comment) |
| `TimestampStart` | `LocalDateTime` | Optional | - | LocalDateTime getTimestampStart() | setTimestampStart(LocalDateTime timestampStart) |
| `TimestampEnd` | `LocalDateTime` | Optional | - | LocalDateTime getTimestampEnd() | setTimestampEnd(LocalDateTime timestampEnd) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.SiteAccessPersonnel;
import java.io.IOException;

SiteAccessPersonnel siteAccessPersonnel = new SiteAccessPersonnel.Builder()
    .personnelId(170)
    .firstName("firstName4")
    .lastName("lastName2")
    .company("company8")
    .phoneNumber("phoneNumber8")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

