
# Site

*This model accepts additional fields of type Object.*

## Structure

`Site`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `SiteId` | `Integer` | Optional | The id of a site.<br><br>**Constraints**: `>= 1` | Integer getSiteId() | setSiteId(Integer siteId) |
| `Title` | `String` | Optional | - | String getTitle() | setTitle(String title) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.Site;
import java.io.IOException;

Site site = new Site.Builder()
    .siteId(14)
    .title("title0")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

