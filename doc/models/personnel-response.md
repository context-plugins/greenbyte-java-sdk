
# Personnel Response

*This model accepts additional fields of type Object.*

## Structure

`PersonnelResponse`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `PersonnelId` | `Integer` | Optional | The id of a person in the personnel list.<br><br>**Constraints**: `>= 1` | Integer getPersonnelId() | setPersonnelId(Integer personnelId) |
| `FirstName` | `String` | Optional | - | String getFirstName() | setFirstName(String firstName) |
| `LastName` | `String` | Optional | - | String getLastName() | setLastName(String lastName) |
| `Email` | `String` | Optional | - | String getEmail() | setEmail(String email) |
| `Phone` | `String` | Optional | - | String getPhone() | setPhone(String phone) |
| `Mobile` | `String` | Optional | - | String getMobile() | setMobile(String mobile) |
| `Organization` | [`Organization1`](../../doc/models/organization-1.md) | Optional | - | Organization1 getOrganization() | setOrganization(Organization1 organization) |
| `Qualifications` | [`List<PersonnelQualification>`](../../doc/models/personnel-qualification.md) | Optional | - | List<PersonnelQualification> getQualifications() | setQualifications(List<PersonnelQualification> qualifications) |
| `SiteInductions` | [`List<PersonnelSiteInduction>`](../../doc/models/personnel-site-induction.md) | Optional | - | List<PersonnelSiteInduction> getSiteInductions() | setSiteInductions(List<PersonnelSiteInduction> siteInductions) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.PersonnelResponse;
import java.io.IOException;

PersonnelResponse personnelResponse = new PersonnelResponse.Builder()
    .personnelId(244)
    .firstName("firstName6")
    .lastName("lastName4")
    .email("email6")
    .phone("phone0")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

