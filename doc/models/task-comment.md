
# Task Comment

A comment added to a task.

*This model accepts additional fields of type Object.*

## Structure

`TaskComment`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `CommentId` | `int` | Required | The id of a task comment.<br><br>**Constraints**: `>= 1` | int getCommentId() | setCommentId(int commentId) |
| `TaskId` | `int` | Required | The id of a task.<br><br>**Constraints**: `>= 1` | int getTaskId() | setTaskId(int taskId) |
| `Text` | `String` | Required | - | String getText() | setText(String text) |
| `TimestampCreated` | `LocalDateTime` | Required | The timestamp when the comment was created (added to the<br>task). The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampCreated() | setTimestampCreated(LocalDateTime timestampCreated) |
| `CreatedBy` | [`User`](../../doc/models/user.md) | Required | - | User getCreatedBy() | setCreatedBy(User createdBy) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.TaskComment;
import cloud.greenbyte.intro.models.User;
import java.io.IOException;

TaskComment taskComment = new TaskComment.Builder(
    86,
    54,
    "Task updated",
    DateTimeHelper.fromRfc8601DateTime("2020-01-01T00:00:00"),
    new User.Builder(
        "firstName2",
        "lastName6"
    )
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build()
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

