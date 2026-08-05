
# Tasks Response

*This model accepts additional fields of type Object.*

## Structure

`TasksResponse`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `TaskId` | `int` | Required | The id of a task.<br><br>**Constraints**: `>= 1` | int getTaskId() | setTaskId(int taskId) |
| `Title` | `String` | Required | - | String getTitle() | setTitle(String title) |
| `CreatedBy` | [`User`](../../doc/models/user.md) | Required | - | User getCreatedBy() | setCreatedBy(User createdBy) |
| `Description` | `String` | Optional | - | String getDescription() | setDescription(String description) |
| `Category` | [`Category`](../../doc/models/category.md) | Optional | - | Category getCategory() | setCategory(Category category) |
| `Priority` | [`TaskPriority`](../../doc/models/task-priority.md) | Required | - | TaskPriority getPriority() | setPriority(TaskPriority priority) |
| `TimestampStart` | `LocalDateTime` | Required | The timestamp when the task is/was planned to start. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampStart() | setTimestampStart(LocalDateTime timestampStart) |
| `TimestampEnd` | `LocalDateTime` | Required | The timestamp when the is/was planned to end. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampEnd() | setTimestampEnd(LocalDateTime timestampEnd) |
| `State` | [`TaskState`](../../doc/models/task-state.md) | Required | - | TaskState getState() | setState(TaskState state) |
| `Resolved` | `boolean` | Required | - | boolean getResolved() | setResolved(boolean resolved) |
| `TimestampResolved` | `LocalDateTime` | Optional | The timestamp when the task was resolved. The timestamp is in the time zone configured in the Greenbyte Platform without UTC offset. | LocalDateTime getTimestampResolved() | setTimestampResolved(LocalDateTime timestampResolved) |
| `DeviceIds` | `List<Integer>` | Optional | Ids of the devices assigned to the task.<br><br>**Constraints**: `>= 1` | List<Integer> getDeviceIds() | setDeviceIds(List<Integer> deviceIds) |
| `SiteIds` | `List<Integer>` | Optional | Ids of the sites assigned to the task.<br><br>**Constraints**: `>= 1` | List<Integer> getSiteIds() | setSiteIds(List<Integer> siteIds) |
| `SiteAccessIds` | `List<Integer>` | Optional | Ids of the site accesses linked to the task.<br><br>**Constraints**: `>= 1` | List<Integer> getSiteAccessIds() | setSiteAccessIds(List<Integer> siteAccessIds) |
| `DowntimeEventIds` | `List<Integer>` | Optional | Ids of the downtime events linked to the task.<br><br>**Constraints**: `>= 1` | List<Integer> getDowntimeEventIds() | setDowntimeEventIds(List<Integer> downtimeEventIds) |
| `StatusIds` | `List<Integer>` | Optional | Ids of the statuses linked to the task.<br><br>**Constraints**: `>= 1` | List<Integer> getStatusIds() | setStatusIds(List<Integer> statusIds) |
| `NumberOfComments` | `int` | Required | **Constraints**: `>= 0` | int getNumberOfComments() | setNumberOfComments(int numberOfComments) |
| `Comments` | [`List<TaskComment>`](../../doc/models/task-comment.md) | Optional | The comments belonging to the task. | List<TaskComment> getComments() | setComments(List<TaskComment> comments) |
| `Recurrence` | `Object` | Optional | - | Object getRecurrence() | setRecurrence(Object recurrence) |
| `MainTaskId` | `Integer` | Optional | **Constraints**: `>= 1` | Integer getMainTaskId() | setMainTaskId(Integer mainTaskId) |
| `Assignee` | [`TasksResponseAssignee`](../../doc/models/containers/tasks-response-assignee.md) | Optional | This is a container for one-of cases. | TasksResponseAssignee getAssignee() | setAssignee(TasksResponseAssignee assignee) |
| `Metadata` | [`List<MetadataField>`](../../doc/models/metadata-field.md) | Optional | A list of metadata fields and their values. | List<MetadataField> getMetadata() | setMetadata(List<MetadataField> metadata) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.Category;
import cloud.greenbyte.intro.models.TaskPriority;
import cloud.greenbyte.intro.models.TaskState;
import cloud.greenbyte.intro.models.TasksResponse;
import cloud.greenbyte.intro.models.User;
import java.io.IOException;
import java.util.Arrays;

TasksResponse tasksResponse = new TasksResponse.Builder(
    248,
    "Maintenance",
    new User.Builder(
        "firstName2",
        "lastName6"
    )
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build(),
    TaskPriority.HIGH,
    DateTimeHelper.fromRfc8601DateTime("2020-01-01T00:00:00"),
    DateTimeHelper.fromRfc8601DateTime("2020-01-08T00:00:00"),
    TaskState.UNRESOLVED,
    true,
    3
)
.description("Gearbox maintenance")
.category(new Category.Builder(
        120,
        "title2"
    )
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build())
.timestampResolved(DateTimeHelper.fromRfc8601DateTime("2020-01-08T00:00:00"))
.deviceIds(Arrays.asList(
        230,
        231,
        232
    ))
.siteIds(Arrays.asList(
        210
    ))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

