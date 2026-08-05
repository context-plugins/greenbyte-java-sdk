
# Client

*This model accepts additional fields of type Object.*

## Structure

`Client`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `Title` | `String` | Required | The title of your Greenbyte Platform website. | String getTitle() | setTitle(String title) |
| `Tag` | `String` | Required | Your internal customer tag. | String getTag() | setTag(String tag) |
| `UrlWeb` | `String` | Required | Your URL to access the Greenbyte Platform website. | String getUrlWeb() | setUrlWeb(String urlWeb) |
| `UrlApi` | `String` | Required | Your URL to access the Greenbyte Platform API. | String getUrlApi() | setUrlApi(String urlApi) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.Client;
import java.io.IOException;

Client client = new Client.Builder(
    "intro",
    "intro",
    "https://intro.greenbyte.cloud/",
    "https://intro.greenbyte.cloud/api/2/"
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

