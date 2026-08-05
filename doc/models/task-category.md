
# Task Category

Basic information about a task category.

*This model accepts additional fields of type Object.*

## Structure

`TaskCategory`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `CategoryId` | `int` | Required | The id of a task category.<br><br>**Constraints**: `>= 1` | int getCategoryId() | setCategoryId(int categoryId) |
| `Title` | `String` | Required | - | String getTitle() | setTitle(String title) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.TaskCategory;
import java.io.IOException;

TaskCategory taskCategory = new TaskCategory.Builder(
    152,
    "Scheduled maintenance"
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

