
# Datapercategory Response 1

*This model accepts additional fields of type Object.*

## Structure

`DatapercategoryResponse1`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `DataSignal` | [`DataSignal1`](../../doc/models/data-signal-1.md) | Required | - | DataSignal1 getDataSignal() | setDataSignal(DataSignal1 dataSignal) |
| `Calculation` | [`CalculationMode`](../../doc/models/calculation-mode.md) | Required | - | CalculationMode getCalculation() | setCalculation(CalculationMode calculation) |
| `Data` | [`List<DataPerCategoryItem>`](../../doc/models/data-per-category-item.md) | Required | A list of objects: one per combination of<br><br>* aggregate<br>* contract category | List<DataPerCategoryItem> getData() | setData(List<DataPerCategoryItem> data) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.CalculationMode;
import cloud.greenbyte.intro.models.CategoryTime;
import cloud.greenbyte.intro.models.DataPerCategoryItem;
import cloud.greenbyte.intro.models.DataSignal1;
import cloud.greenbyte.intro.models.DatapercategoryResponse1;
import java.io.IOException;
import java.util.Arrays;

DatapercategoryResponse1 datapercategoryResponse1 = new DatapercategoryResponse1.Builder(
    new DataSignal1.Builder(
        24,
        "title8",
        "unit4"
    )
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build(),
    CalculationMode.SUM,
    Arrays.asList(
        new DataPerCategoryItem.Builder(
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
                "aggregatePathNames4"
            ))
        .duration(150D)
        .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
        .build()
    )
)
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
.build();
```

