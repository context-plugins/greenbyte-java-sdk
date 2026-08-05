
# Task Assignee Other

Information about some other entity assigned to a task.

*This model accepts additional fields of type Object.*

## Structure

`TaskAssigneeOther`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `AssigneeType` | [`TaskAssigneeType`](../../doc/models/task-assignee-type.md) | Required | - | TaskAssigneeType getAssigneeType() | setAssigneeType(TaskAssigneeType assigneeType) |
| `Text` | `String` | Required | Free-text description of the assignee. | String getText() | setText(String text) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.TaskAssigneeOther;
import cloud.greenbyte.intro.models.TaskAssigneeType;
import java.io.IOException;

TaskAssigneeOther taskAssigneeOther = new TaskAssigneeOther.Builder(
    TaskAssigneeType.MANUFACTURER,
    "text2"
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

