
# Predict Status Active

Status info for an active Predict alert.

*This model accepts additional fields of type Object.*

## Structure

`PredictStatusActive`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `Recommendations` | [`List<PredictRecommendation>`](../../doc/models/predict-recommendation.md) | Optional | Recommended actions for resolving the alert. Will be null if not calculated yet. | List<PredictRecommendation> getRecommendations() | setRecommendations(List<PredictRecommendation> recommendations) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.PredictRecommendation;
import cloud.greenbyte.intro.models.PredictStatusActive;
import java.io.IOException;
import java.util.Arrays;

PredictStatusActive predictStatusActive = new PredictStatusActive.Builder()
    .recommendations(Arrays.asList(
        new PredictRecommendation.Builder()
            .component("component6")
            .action("action4")
            .confidence(68)
        .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
            .build(),
        new PredictRecommendation.Builder()
            .component("component6")
            .action("action4")
            .confidence(68)
        .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
            .build()
    ))
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

