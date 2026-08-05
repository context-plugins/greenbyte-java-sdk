
# Task Assignee Manufacturer

The manufacturer assigned to a task.

*This model accepts additional fields of type Object.*

## Structure

`TaskAssigneeManufacturer`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `AssigneeType` | [`TaskAssigneeType`](../../doc/models/task-assignee-type.md) | Required | - | TaskAssigneeType getAssigneeType() | setAssigneeType(TaskAssigneeType assigneeType) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.TaskAssigneeManufacturer;
import cloud.greenbyte.intro.models.TaskAssigneeType;
import java.io.IOException;

TaskAssigneeManufacturer taskAssigneeManufacturer = new TaskAssigneeManufacturer.Builder(
    TaskAssigneeType.MANUFACTURER
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

