
# Turbine Type

Turbine-specific type information.

*This model accepts additional fields of type Object.*

## Structure

`TurbineType`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `TurbineTypeId` | `Integer` | Optional | - | Integer getTurbineTypeId() | setTurbineTypeId(Integer turbineTypeId) |
| `Title` | `String` | Optional | - | String getTitle() | setTitle(String title) |
| `Manufacturer` | `String` | Optional | - | String getManufacturer() | setManufacturer(String manufacturer) |
| `Model` | `String` | Optional | - | String getModel() | setModel(String model) |
| `Controller` | `String` | Optional | The model of the turbine controller. | String getController() | setController(String controller) |
| `RatedPower` | `Integer` | Optional | - | Integer getRatedPower() | setRatedPower(Integer ratedPower) |
| `MaxRotorSpeed` | `Double` | Optional | - | Double getMaxRotorSpeed() | setMaxRotorSpeed(Double maxRotorSpeed) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.TurbineType;
import java.io.IOException;

TurbineType turbineType = new TurbineType.Builder()
    .turbineTypeId(156)
    .title("title2")
    .manufacturer("manufacturer0")
    .model("model4")
    .controller("controller6")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

