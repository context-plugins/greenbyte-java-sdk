# Assets

This section contains operations related to assets, such as sites and devices.

## Devices

In this context, *devices* are power-producing devices such as wind turbines and inverters as well as instruments such as met masts and grid meters, which measure, record, and communicate data and metadata for a site or device.

## Power curves

Power curves are graphs which indicate how large the electrical power output of a wind turbine will be at different wind speeds.

Power curves are used for potential power calculation and for performance KPIs. The default power curve is defined when the wind turbine is installed in the Greenbyte Platform, but you can alter the default or add power curves as needed. Having multiple power curves enables calculations in the system to adapt to different circumstances, like curtailment, sector management, or technical management.

```java
AssetsApi assetsApi = client.getAssetsApi();
```

## Class Name

`AssetsApi`

## Methods

* [Get Devices](../../doc/controllers/assets.md#get-devices)
* [Get Devices Published After Date](../../doc/controllers/assets.md#get-devices-published-after-date)
* [Get Sites](../../doc/controllers/assets.md#get-sites)
* [Get Power Curves](../../doc/controllers/assets.md#get-power-curves)


# Get Devices

Gets a list of devices that the API key has permissions for.

_🔐 This endpoint requires the **Assets** endpoint permission._

_This request can also be made using the POST method,
with a request to `devices.json` and
a JSON request body instead of query parameters._

```java
CompletableFuture<ApiResponse<List<Device>>> getDevicesAsync(
    final List<Integer> deviceTypeIds,
    final List<Integer> siteIds,
    final List<Integer> parentIds,
    final List<String> fields,
    final Integer pageSize,
    final Integer page,
    final Boolean useUtc)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `deviceTypeIds` | `List<Integer>` | Query, Optional | Only include devices of these types.<br>Examples:<br><br>* 1 - Wind turbine<br>* 2 - Production meter<br>* 3 - Met mast<br>* 4 - Inverter<br>* 5 - Substation<br>* 10 - Device group<br>* 11 - Grid meter<br>* 12 - Combiner box<br>* 23 - String<br>* 27 - Virtual Meteo Sensor<br><br>**Constraints**: `>= 1` |
| `siteIds` | `List<Integer>` | Query, Optional | Only include devices at these sites.<br><br>**Constraints**: `>= 1` |
| `parentIds` | `List<Integer>` | Query, Optional | Only include devices with these parent devices.<br><br>**Constraints**: `>= 1` |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `Device` schema (See Response Type). By default all fields are included. |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A list of devices with associated metadata.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<Device>`](../../doc/models/device.md).

## Example Usage

```java
List<Integer> deviceTypeIds = Arrays.asList(
    1,
    2,
    3
);

List<Integer> siteIds = Arrays.asList(
    1,
    2,
    3
);

List<Integer> parentIds = Arrays.asList(
    1,
    2,
    3
);

Integer pageSize = 50;
Integer page = 1;
Boolean useUtc = false;

assetsApi.getDevicesAsync(deviceTypeIds, siteIds, parentIds, null, pageSize, page, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Devices400ErrorException) {
        Devices400ErrorException devices400ErrorException = (Devices400ErrorException) cause;
        devices400ErrorException.printStackTrace();
    } else if (cause instanceof Devices429ErrorException) {
        Devices429ErrorException devices429ErrorException = (Devices429ErrorException) cause;
        devices429ErrorException.printStackTrace();
    } else {
        // fallback for unexpected errors
        exception.printStackTrace();
    }

    return null;
});
```

## Example Response *(as JSON)*

```json
[
  {
    "deviceId": 1121,
    "title": "Enerburg group A",
    "altTitle": null,
    "identity": null,
    "site": {
      "siteId": 7,
      "title": "Enerburg"
    },
    "deviceType": "Group",
    "deviceTypeId": 10,
    "parentId": null,
    "childIds": [
      69,
      70
    ],
    "deviceModel": {
      "deviceModelId": 41,
      "manufacturer": "Generic group",
      "model": "Generic"
    },
    "maxPower": 0,
    "timestampStart": "2013-10-01T02:00:00",
    "latitude": "32.36431",
    "longitude": "-88.7037",
    "elevation": "0",
    "metadata": []
  },
  {
    "deviceId": 69,
    "title": "Enerburg 1",
    "altTitle": null,
    "identity": null,
    "site": {
      "siteId": 7,
      "title": "Enerburg"
    },
    "deviceType": "Turbine",
    "deviceTypeId": 1,
    "parentId": 1121,
    "childIds": [],
    "deviceModel": null,
    "turbineType": {
      "turbineTypeId": 1,
      "title": "Enercon E-82 E2 2.3MW",
      "manufacturer": "Enercon",
      "model": "E-82",
      "controller": "CS82a",
      "ratedPower": 2300,
      "maxRotorSpeed": 18
    },
    "maxPower": 2300,
    "biddingArea": null,
    "timestampStart": "2013-10-01T02:00:00",
    "latitude": "32.36431",
    "longitude": "-88.7037",
    "elevation": "0",
    "targetAvailability": 97,
    "metadata": [
      {
        "key": "Hub Height",
        "value": "120"
      },
      {
        "key": "Direct Drive",
        "value": "no"
      },
      {
        "key": "Blade Heating",
        "value": "yes"
      }
    ]
  },
  {
    "deviceId": 70,
    "title": "Enerburg 2",
    "altTitle": null,
    "identity": null,
    "site": {
      "siteId": 7,
      "title": "Enerburg"
    },
    "deviceType": "Turbine",
    "deviceTypeId": 1,
    "parentId": 1121,
    "childIds": [],
    "deviceModel": null,
    "turbineType": {
      "turbineTypeId": 1,
      "title": "Enercon E-82 E2 2.3MW",
      "manufacturer": "Enercon",
      "model": "E-82",
      "controller": "CS82a",
      "ratedPower": 2300,
      "maxRotorSpeed": 18
    },
    "maxPower": 2300,
    "biddingArea": null,
    "timestampStart": "2013-10-01T02:00:00",
    "latitude": "32.3602",
    "longitude": "-88.7194",
    "elevation": "0",
    "targetAvailability": null,
    "metadata": [
      {
        "key": "Hub Height",
        "value": "120"
      },
      {
        "key": "Direct Drive",
        "value": "no"
      },
      {
        "key": "Blade Heating",
        "value": "yes"
      }
    ]
  },
  {
    "deviceId": 71,
    "title": "Enerburg 3",
    "altTitle": null,
    "identity": null,
    "site": {
      "siteId": 7,
      "title": "Enerburg"
    },
    "deviceType": "Turbine",
    "deviceModel": null,
    "parentId": null,
    "childIds": [],
    "deviceTypeId": 1,
    "turbineType": {
      "turbineTypeId": 1,
      "title": "Enercon E-82 E2 2.3MW",
      "manufacturer": "Enercon",
      "model": "E-82",
      "controller": "CS82a",
      "ratedPower": 2300,
      "maxRotorSpeed": 18
    },
    "maxPower": 2300,
    "biddingArea": null,
    "timestampStart": "2013-10-01T02:00:00",
    "latitude": "32.35697",
    "longitude": "-88.7182",
    "elevation": "0",
    "targetAvailability": null,
    "metadata": []
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Devices400ErrorException`](../../doc/models/devices-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Devices429ErrorException`](../../doc/models/devices-429-error-exception.md) |


# Get Devices Published After Date

Gets the number of devices published on a site after a certain date as well as the IDs of the authorized devices.

_🔐 This endpoint requires the **Assets** endpoint permission._

```java
CompletableFuture<ApiResponse<DevicesPublishedAfterDateResponse>> getDevicesPublishedAfterDateAsync(
    final int siteId,
    final LocalDateTime date)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `siteId` | `int` | Query, Required | **Constraints**: `>= 1` |
| `date` | `LocalDateTime` | Query, Required | Date after which published devices will be fetched. |

## Response Type

**200**: A list of devices with associated metadata.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`DevicesPublishedAfterDateResponse`](../../doc/models/devices-published-after-date-response.md).

## Example Usage

```java
int siteId = 222;
LocalDateTime date = DateTimeHelper.fromRfc8601DateTime("04/01/2023 00:00:00");

assetsApi.getDevicesPublishedAfterDateAsync(siteId, date).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof DevicesPublishedAfterDate400ErrorException) {
        DevicesPublishedAfterDate400ErrorException devicesPublishedAfterDate400ErrorException = (DevicesPublishedAfterDate400ErrorException) cause;
        devicesPublishedAfterDate400ErrorException.printStackTrace();
    } else if (cause instanceof DevicesPublishedAfterDate429ErrorException) {
        DevicesPublishedAfterDate429ErrorException devicesPublishedAfterDate429ErrorException = (DevicesPublishedAfterDate429ErrorException) cause;
        devicesPublishedAfterDate429ErrorException.printStackTrace();
    } else {
        // fallback for unexpected errors
        exception.printStackTrace();
    }

    return null;
});
```

## Example Response *(as JSON)*

```json
{
  "numberOfDevices": 4,
  "authorizedDeviceIds": [
    2,
    3,
    4
  ]
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`DevicesPublishedAfterDate400ErrorException`](../../doc/models/devices-published-after-date-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`DevicesPublishedAfterDate429ErrorException`](../../doc/models/devices-published-after-date-429-error-exception.md) |


# Get Sites

Gets a list of sites that the API key has permissions
for.

_🔐 This endpoint requires the **Assets** endpoint permission._

_This request can also be made using the POST method,
with a request to `sites.json` and
a JSON request body instead of query parameters._

```java
CompletableFuture<ApiResponse<List<SiteWithData>>> getSitesAsync(
    final List<String> fields,
    final Integer pageSize,
    final Integer page)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `SiteWithData` schema (See Response Type). By default all fields are included. |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |

## Response Type

**200**: A list of sites with associated metadata.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<SiteWithData>`](../../doc/models/site-with-data.md).

## Example Usage

```java
List<String> fields = Arrays.asList(
    "siteId",
    "title"
);

Integer pageSize = 50;
Integer page = 1;

assetsApi.getSitesAsync(fields, pageSize, page).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Sites400ErrorException) {
        Sites400ErrorException sites400ErrorException = (Sites400ErrorException) cause;
        sites400ErrorException.printStackTrace();
    } else if (cause instanceof Sites429ErrorException) {
        Sites429ErrorException sites429ErrorException = (Sites429ErrorException) cause;
        sites429ErrorException.printStackTrace();
    } else {
        // fallback for unexpected errors
        exception.printStackTrace();
    }

    return null;
});
```

## Example Response *(as JSON)*

```json
[
  {
    "siteId": 1,
    "title": "Wind farm 1",
    "country": "Sweden",
    "identity": "SE-WF1",
    "metadata": [
      {
        "key": "Address",
        "value": "Wind Street 123"
      },
      {
        "key": "Phone",
        "value": "555 123 456"
      }
    ]
  },
  {
    "siteId": 2,
    "title": "Solar site 1",
    "country": "Spain",
    "identity": "ES-SS1",
    "metadata": [
      {
        "key": "Address",
        "value": "Sun Street 456"
      },
      {
        "key": "Phone",
        "value": "555 456 789"
      }
    ]
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Sites400ErrorException`](../../doc/models/sites-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Sites429ErrorException`](../../doc/models/sites-429-error-exception.md) |


# Get Power Curves

Gets the default or learned power curves for wind turbines.
Other device types are not supported.

_🔐 This endpoint requires the **PowerCurves** endpoint permission._

_This request can also be made using the POST method,
with a request to `powercurves.json` and
a JSON request body instead of query parameters._

```java
CompletableFuture<ApiResponse<List<PowerCurve>>> getPowerCurvesAsync(
    final List<Integer> deviceIds,
    final LocalDate timestamp,
    final Boolean learned)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `deviceIds` | `List<Integer>` | Query, Required | What devices to get power curves for. Only wind turbines are supported.<br><br>**Constraints**: `>= 1` |
| `timestamp` | `LocalDate` | Query, Optional | The date for which to get power curves. The default is the current date. |
| `learned` | `Boolean` | Query, Optional | Whether to get learned power curves instead of default power curves.<br><br>**Default**: `false` |

## Response Type

**200**: A list of objects containing device ids and associated power curves.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<PowerCurve>`](../../doc/models/power-curve.md).

## Example Usage

```java
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

LocalDate timestamp = DateTimeHelper.fromSimpleDate("2023-03-01");
Boolean learned = false;

assetsApi.getPowerCurvesAsync(deviceIds, timestamp, learned).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Powercurves400ErrorException) {
        Powercurves400ErrorException powercurves400ErrorException = (Powercurves400ErrorException) cause;
        powercurves400ErrorException.printStackTrace();
    } else if (cause instanceof Powercurves429ErrorException) {
        Powercurves429ErrorException powercurves429ErrorException = (Powercurves429ErrorException) cause;
        powercurves429ErrorException.printStackTrace();
    } else {
        // fallback for unexpected errors
        exception.printStackTrace();
    }

    return null;
});
```

## Example Response *(as JSON)*

```json
[
  {
    "deviceId": 1,
    "title": "Enercon E-82 Noise mode 0",
    "values": [
      {
        "windSpeed": 1,
        "power": 0
      },
      {
        "windSpeed": 4,
        "power": 88
      },
      {
        "windSpeed": 5,
        "power": 205
      },
      {
        "windSpeed": 6,
        "power": 371
      },
      {
        "windSpeed": 7,
        "power": 601
      },
      {
        "windSpeed": 8,
        "power": 901
      },
      {
        "windSpeed": 9,
        "power": 1243
      },
      {
        "windSpeed": 10,
        "power": 1591
      },
      {
        "windSpeed": 11,
        "power": 1876
      },
      {
        "windSpeed": 12,
        "power": 1979
      },
      {
        "windSpeed": 13,
        "power": 1999
      },
      {
        "windSpeed": 14,
        "power": 2000
      },
      {
        "windSpeed": 15,
        "power": 2000
      },
      {
        "windSpeed": 16,
        "power": 2000
      },
      {
        "windSpeed": 17,
        "power": 2000
      },
      {
        "windSpeed": 18,
        "power": 2000
      },
      {
        "windSpeed": 19,
        "power": 2000
      },
      {
        "windSpeed": 20,
        "power": 2000
      },
      {
        "windSpeed": 21,
        "power": 2000
      },
      {
        "windSpeed": 22,
        "power": 2000
      },
      {
        "windSpeed": 23,
        "power": 2000
      },
      {
        "windSpeed": 24,
        "power": 2000
      },
      {
        "windSpeed": 25,
        "power": 2000
      }
    ]
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Powercurves400ErrorException`](../../doc/models/powercurves-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Powercurves429ErrorException`](../../doc/models/powercurves-429-error-exception.md) |

