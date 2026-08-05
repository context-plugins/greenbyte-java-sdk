
# User

*This model accepts additional fields of type Object.*

## Structure

`User`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `FirstName` | `String` | Required | - | String getFirstName() | setFirstName(String firstName) |
| `LastName` | `String` | Required | - | String getLastName() | setLastName(String lastName) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.User;
import java.io.IOException;

User user = new User.Builder(
    "firstName4",
    "lastName4"
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

