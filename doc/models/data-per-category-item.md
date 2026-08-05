
# Data per Category Item

Data for a single aggregate group and contract category combination.

*This model accepts additional fields of type Object.*

## Structure

`DataPerCategoryItem`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `AggregateId` | `int` | Required | The id of this aggregate group: device id, site id, or the constant -1 for portfolio. For `siteLevel` aggregation a generated unique id is used. | int getAggregateId() | setAggregateId(int aggregateId) |
| `AggregatePathNames` | `List<String>` | Optional | For `siteLevel` aggregation this contains the title for each level in the hierarchy. For other types of aggregation it will be empty. | List<String> getAggregatePathNames() | setAggregatePathNames(List<String> aggregatePathNames) |
| `DeviceIds` | `List<Integer>` | Required | The ids of the devices in this aggregate group.<br><br>**Constraints**: `>= 1` | List<Integer> getDeviceIds() | setDeviceIds(List<Integer> deviceIds) |
| `ContractTitle` | `String` | Required | - | String getContractTitle() | setContractTitle(String contractTitle) |
| `CategoryTitle` | `String` | Required | - | String getCategoryTitle() | setCategoryTitle(String categoryTitle) |
| `CategoryTime` | [`CategoryTime`](../../doc/models/category-time.md) | Required | - | CategoryTime getCategoryTime() | setCategoryTime(CategoryTime categoryTime) |
| `Value` | `double` | Required | The aggregated value of the selected data signal. | double getValue() | setValue(double value) |
| `Duration` | `Double` | Optional | The summed duration in seconds allocated to this contract category and aggregate group. | Double getDuration() | setDuration(Double duration) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.CategoryTime;
import cloud.greenbyte.intro.models.DataPerCategoryItem;
import java.io.IOException;
import java.util.Arrays;

DataPerCategoryItem dataPerCategoryItem = new DataPerCategoryItem.Builder(
    6,
    Arrays.asList(
        1,
        2,
        3
    ),
    "Vestas 1",
    "Icing",
    CategoryTime.AVAILABLE,
    104.55D
)
.aggregatePathNames(Arrays.asList(
        "aggregatePathNames6"
    ))
.duration(150D)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

