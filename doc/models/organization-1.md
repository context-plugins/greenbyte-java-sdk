
# Organization 1

*This model accepts additional fields of type Object.*

## Structure

`Organization1`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `OrganizationId` | `Integer` | Optional | An id of an organization used for tasks and personnel.<br><br>**Constraints**: `>= 1` | Integer getOrganizationId() | setOrganizationId(Integer organizationId) |
| `Name` | `String` | Optional | - | String getName() | setName(String name) |
| `Email` | `String` | Optional | - | String getEmail() | setEmail(String email) |
| `Phone` | `String` | Optional | - | String getPhone() | setPhone(String phone) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.Organization1;
import java.io.IOException;

Organization1 organization1 = new Organization1.Builder()
    .organizationId(94)
    .name("name8")
    .email("email8")
    .phone("phone2")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

