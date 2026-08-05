
# Problem Details

An object describing the problem with the request, following the [RFC 7807](https://tools.ietf.org/html/rfc7807) format.

*This model accepts additional fields of type Object.*

## Structure

`ProblemDetails`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `Status` | `int` | Required | - | int getStatus() | setStatus(int status) |
| `Title` | `String` | Required | - | String getTitle() | setTitle(String title) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.ProblemDetails;
import java.io.IOException;

ProblemDetails problemDetails = new ProblemDetails.Builder(
    122,
    "title2"
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

