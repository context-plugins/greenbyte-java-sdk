
# Device

*This model accepts additional fields of type Object.*

## Structure

`Device`

## Fields

| Name | Type | Tags | Description | Getter | Setter |
|  --- | --- | --- | --- | --- | --- |
| `DeviceId` | `Integer` | Optional | The id of a device.<br><br>**Constraints**: `>= 1` | Integer getDeviceId() | setDeviceId(Integer deviceId) |
| `Title` | `String` | Optional | - | String getTitle() | setTitle(String title) |
| `AltTitle` | `String` | Optional | An alternative title. | String getAltTitle() | setAltTitle(String altTitle) |
| `Identity` | `String` | Optional | Device identification number. | String getIdentity() | setIdentity(String identity) |
| `Site` | [`Site`](../../doc/models/site.md) | Optional | - | Site getSite() | setSite(Site site) |
| `DeviceType` | `String` | Optional | The string representation of the device type. | String getDeviceType() | setDeviceType(String deviceType) |
| `DeviceTypeId` | `Integer` | Optional | The id of a device type.<br><br>**Constraints**: `>= 1` | Integer getDeviceTypeId() | setDeviceTypeId(Integer deviceTypeId) |
| `ParentId` | `Integer` | Optional | The id of the parent device, if any.<br><br>**Constraints**: `>= 1` | Integer getParentId() | setParentId(Integer parentId) |
| `ChildIds` | `List<Integer>` | Optional | Ids of child devices, if any.<br><br>**Constraints**: `>= 1` | List<Integer> getChildIds() | setChildIds(List<Integer> childIds) |
| `DeviceModel` | `Object` | Optional | - | Object getDeviceModel() | setDeviceModel(Object deviceModel) |
| `TurbineType` | `Object` | Optional | - | Object getTurbineType() | setTurbineType(Object turbineType) |
| `MaxPower` | `Double` | Optional | The maximum power for a device. | Double getMaxPower() | setMaxPower(Double maxPower) |
| `BiddingArea` | `String` | Optional | Only applies to Nordic countries and the UK. | String getBiddingArea() | setBiddingArea(String biddingArea) |
| `TimestampStart` | `LocalDateTime` | Optional | The earliest timestamp device data is available for. | LocalDateTime getTimestampStart() | setTimestampStart(LocalDateTime timestampStart) |
| `Latitude` | `String` | Optional | The latitude of the device in the WGS84 system. | String getLatitude() | setLatitude(String latitude) |
| `Longitude` | `String` | Optional | The longitude of the device in the WGS84 system. | String getLongitude() | setLongitude(String longitude) |
| `Elevation` | `String` | Optional | The elevation of the device in meters above sea level. | String getElevation() | setElevation(String elevation) |
| `TargetAvailability` | `Double` | Optional | The target availability for the device.<br><br>**Constraints**: `>= 0`, `<= 100` | Double getTargetAvailability() | setTargetAvailability(Double targetAvailability) |
| `Metadata` | [`List<MetadataField>`](../../doc/models/metadata-field.md) | Optional | A list of metadata fields and their values. | List<MetadataField> getMetadata() | setMetadata(List<MetadataField> metadata) |
| `AdditionalProperties` | `Map<String, Object>` | Optional | - | Object getAdditionalProperty(String key) | additionalProperty(String key, Object value) |

## Example

```java
import cloud.greenbyte.intro.ApiHelper;
import cloud.greenbyte.intro.models.Device;
import cloud.greenbyte.intro.models.Site;
import java.io.IOException;

Device device = new Device.Builder()
    .deviceId(240)
    .title("title2")
    .altTitle("altTitle4")
    .identity("identity0")
    .site(new Site.Builder()
        .siteId(14)
        .title("title0")
    .additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
        .build())
    .deviceType("Turbine")
.additionalProperty("exampleAdditionalProperty", ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}"))
    .build();
```

