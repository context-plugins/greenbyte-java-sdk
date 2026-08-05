
# Personnel Qualification

A personnel qualification.

*This model accepts additional fields of type Object.*

## Structure

`PersonnelQualification`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `QualificationId` | `Integer` | Optional | The id of a personnel qualification.<br><br>**Constraints**: `>= 1` | Integer getQualificationId() | setQualificationId(Integer qualificationId) |
| `Manufacturer` | `String` | Optional | - | String getManufacturer() | setManufacturer(String manufacturer) |
| `QualificationType` | `String` | Optional | - | String getQualificationType() | setQualificationType(String qualificationType) |
| `QualificationDescription` | `String` | Optional | - | String getQualificationDescription() | setQualificationDescription(String qualificationDescription) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.PersonnelQualification;
import java.io.IOException;

PersonnelQualification personnelQualification = new PersonnelQualification.Builder()
    .qualificationId(166)
    .manufacturer("manufacturer8")
    .qualificationType("qualificationType2")
    .qualificationDescription("qualificationDescription4")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

