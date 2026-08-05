
# Tasks Files Response

*This model accepts additional fields of type Object.*

## Structure

`TasksFilesResponse`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `FileId` | `int` | Required | The id of a file.<br><br>**Constraints**: `>= 1` | int getFileId() | setFileId(int fileId) |
| `FileName` | `String` | Required | - | String getFileName() | setFileName(String fileName) |
| `TimestampUploaded` | `LocalDateTime` | Required | The timestamp when the file was uploaded. | LocalDateTime getTimestampUploaded() | setTimestampUploaded(LocalDateTime timestampUploaded) |
| `UploadedBy` | [`User`](../../doc/models/user.md) | Required | - | User getUploadedBy() | setUploadedBy(User uploadedBy) |
| `Description` | `String` | Optional | - | String getDescription() | setDescription(String description) |
| `Category` | [`TaskFileCategory`](../../doc/models/task-file-category.md) | Optional | - | TaskFileCategory getCategory() | setCategory(TaskFileCategory category) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.DateTimeHelper;
import cloud.greenbyte.intro.models.TaskFileCategory;
import cloud.greenbyte.intro.models.TasksFilesResponse;
import cloud.greenbyte.intro.models.User;
import java.io.IOException;

TasksFilesResponse tasksFilesResponse = new TasksFilesResponse.Builder(
    250,
    "250.png",
    DateTimeHelper.fromRfc8601DateTime("2020-01-08T00:00:00"),
    new User.Builder(
        "firstName0",
        "lastName8"
    )
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build()
)
.description("A photo of the nacelle")
.category(TaskFileCategory.OTHER)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

