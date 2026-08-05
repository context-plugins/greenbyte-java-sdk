
# Site with Data

*This model accepts additional fields of type Object.*

## Structure

`SiteWithData`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `SiteId` | `Integer` | Optional | The id of a site.<br><br>**Constraints**: `>= 1` | Integer getSiteId() | setSiteId(Integer siteId) |
| `Title` | `String` | Optional | - | String getTitle() | setTitle(String title) |
| `Country` | `String` | Optional | - | String getCountry() | setCountry(String country) |
| `Identity` | `String` | Optional | - | String getIdentity() | setIdentity(String identity) |
| `Metadata` | [`List<MetadataField>`](../../doc/models/metadata-field.md) | Optional | A list of metadata fields and their values. | List<MetadataField> getMetadata() | setMetadata(List<MetadataField> metadata) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.MetadataField;
import cloud.greenbyte.intro.models.SiteWithData;
import java.io.IOException;
import java.util.Arrays;

SiteWithData siteWithData = new SiteWithData.Builder()
    .siteId(212)
    .title("title4")
    .country("country4")
    .identity("identity4")
    .metadata(Arrays.asList(
        new MetadataField.Builder()
            .key("key6")
            .value("value8")
        .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
            .build()
    ))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

