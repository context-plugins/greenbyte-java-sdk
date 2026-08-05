
# Personnel Site Induction

A site induction.

*This model accepts additional fields of type Object.*

## Structure

`PersonnelSiteInduction`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `SiteInductionId` | `Integer` | Optional | The id of a personnel site induction.<br><br>**Constraints**: `>= 1` | Integer getSiteInductionId() | setSiteInductionId(Integer siteInductionId) |
| `SiteId` | `Integer` | Optional | The id of a site.<br><br>**Constraints**: `>= 1` | Integer getSiteId() | setSiteId(Integer siteId) |
| `DateExpires` | `LocalDate` | Optional | When the site induction expires. | LocalDate getDateExpires() | setDateExpires(LocalDate dateExpires) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.PersonnelSiteInduction;
import java.io.IOException;

PersonnelSiteInduction personnelSiteInduction = new PersonnelSiteInduction.Builder()
    .siteInductionId(22)
    .siteId(168)
    .dateExpires(DateTimeHelper.fromSimpleDate("2016-03-13"))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

