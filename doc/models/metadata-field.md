
# Metadata Field

A metadata field.

*This model accepts additional fields of type Object.*

## Structure

`MetadataField`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `Key` | `String` | Optional | - | String getKey() | setKey(String key) |
| `Value` | `String` | Optional | - | String getValue() | setValue(String value) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.MetadataField;
import java.io.IOException;

MetadataField metadataField = new MetadataField.Builder()
    .key("key8")
    .value("value0")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

