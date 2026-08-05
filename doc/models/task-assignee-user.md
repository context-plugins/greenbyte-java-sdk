
# Task Assignee User

*This model accepts additional fields of type Object.*

## Structure

`TaskAssigneeUser`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `FirstName` | `String` | Required | - | String getFirstName() | setFirstName(String firstName) |
| `LastName` | `String` | Required | - | String getLastName() | setLastName(String lastName) |
| `AssigneeType` | [`TaskAssigneeType`](../../doc/models/task-assignee-type.md) | Required | - | TaskAssigneeType getAssigneeType() | setAssigneeType(TaskAssigneeType assigneeType) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.TaskAssigneeType;
import cloud.greenbyte.intro.models.TaskAssigneeUser;
import java.io.IOException;

TaskAssigneeUser taskAssigneeUser = new TaskAssigneeUser.Builder(
    "firstName2",
    "lastName6",
    TaskAssigneeType.MANUFACTURER
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

