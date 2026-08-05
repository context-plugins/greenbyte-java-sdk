# Data

This section contains operations related to either time-series or aggregated signal data.

## Data signals

Data signals are binary code signals which transmit information like temperature, wind speed, and power from an asset or device to the Greenbyte Platform. In addition the Greenbyte Platform provides KPIs and other advanced calculations that are also exposed as signals.

## Data resolution

Data can be returned in different resolutions, for example ten minute resolution or daily resolution.

## Data aggregation

Different kinds of data are aggregated (combined) in different ways. The calculation mode of the signal determines how individual data points are aggregated. All signals have a default calculation mode, for example:

* *Sum* is used for energy signals, which means data values are summed.
* *Average* for wind speed signals, which means that data values are averaged.
  When combining data from several devices you can also choose if the data is aggregated per individual device or per site or if all of the data is combined into one value.
  [Signal Calculations in the Greenbyte Platform documentation](https://help.greenbyte.com/Greenbyte/en/signal-calculations.html)

```java
DataApi dataApi = client.getDataApi();
```

## Class Name

`DataApi`

## Methods

* [Get Data Signals](../../doc/controllers/data.md#get-data-signals)
* [Get Data](../../doc/controllers/data.md#get-data)
* [Get Real Time Data](../../doc/controllers/data.md#get-real-time-data)
* [Get Data per Category](../../doc/controllers/data.md#get-data-per-category)
* [Get High Res Data](../../doc/controllers/data.md#get-high-res-data)


# Get Data Signals

Gets authorized data signals for one or more devices.

_🔐 This endpoint requires the **Data** endpoint permission._

_This request can also be made using the POST method,
with a request to `datasignals.json` and
a JSON request body instead of query parameters._

```java
CompletableFuture<ApiResponse<List<DataSignalItem>>> getDataSignalsAsync(
    final List<Integer> deviceIds)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `deviceIds` | `List<Integer>` | Query, Optional | What devices to get data signals for.<br><br>**Constraints**: `>= 1` |

## Response Type

**200**: The data signals available for one or several of the devices.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<DataSignalItem>`](../../doc/models/data-signal-item.md).

## Example Usage

```java
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

dataApi.getDataSignalsAsync(deviceIds).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Datasignals400ErrorException) {
        Datasignals400ErrorException datasignals400ErrorException = (Datasignals400ErrorException) cause;
        datasignals400ErrorException.printStackTrace();
    } else if (cause instanceof Datasignals429ErrorException) {
        Datasignals429ErrorException datasignals429ErrorException = (Datasignals429ErrorException) cause;
        datasignals429ErrorException.printStackTrace();
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
    "dataSignalId": 1,
    "title": "Wind speed",
    "type": "Wind speed",
    "unit": "m/s",
    "deviceType": {
      "deviceTypeId": 1,
      "title": "Turbine"
    }
  },
  {
    "dataSignalId": 5,
    "title": "Power",
    "type": "Power",
    "unit": "kW",
    "deviceType": {
      "deviceTypeId": 1,
      "title": "Turbine"
    }
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Datasignals400ErrorException`](../../doc/models/datasignals-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Datasignals429ErrorException`](../../doc/models/datasignals-429-error-exception.md) |


# Get Data

Gets data for multiple devices and data signals in the given
resolution. The timestamps are in the time zone configured in the Greenbyte Platform.
Use the useUtc flag to get timestamps in UTC for all resolutions other than daily, weekly, monthly and yearly.

_🔐 This endpoint requires the **Data** endpoint permission._

_This request can also be made using the POST method,
with a request to `data.json` and
a JSON request body instead of query parameters._

```java
CompletableFuture<ApiResponse<List<DataItem>>> getDataAsync(
    final List<Integer> deviceIds,
    final List<Integer> dataSignalIds,
    final LocalDateTime timestampStart,
    final LocalDateTime timestampEnd,
    final Boolean useUtc,
    final Resolution resolution,
    final AggregateMode aggregate,
    final Integer aggregateLevel,
    final CalculationMode calculation)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `deviceIds` | `List<Integer>` | Query, Required | Which devices to get data for.<br><br>**Constraints**: `>= 1` |
| `dataSignalIds` | `List<Integer>` | Query, Required | Which data signals to get data for.<br><br>**Constraints**: `>= 1` |
| `timestampStart` | `LocalDateTime` | Query, Required | The beginning of the time interval to get data for (inclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The start timestamp **is** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `timestampEnd` | `LocalDateTime` | Query, Required | The end of the time interval to get data for (exclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The end timestamp is **not** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC. UTC timestamps are available for all resolutions other than daily, weekly, monthly and yearly.<br><br>**Default**: `false` |
| `resolution` | [`Resolution`](../../doc/models/resolution.md) | Query, Optional | The desired data resolution. |
| `aggregate` | [`AggregateMode`](../../doc/models/aggregate-mode.md) | Query, Optional | How the data should be aggregated with regards to device(s) or site(s). |
| `aggregateLevel` | `Integer` | Query, Optional | When AggregateMode `siteLevel` is used this parameter controls down to which level in the hierarchy to aggregate.<br><br>**Default**: `0` |
| `calculation` | [`CalculationMode`](../../doc/models/calculation-mode.md) | Query, Optional | The calculation used when aggregating data, both over time and across devices. The default is the data signal default. |

## Response Type

**200**: The data grouped by data signal and aggregate.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<DataItem>`](../../doc/models/data-item.md).

## Example Usage

```java
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

List<Integer> dataSignalIds = Arrays.asList(
    1,
    5
);

LocalDateTime timestampStart = DateTimeHelper.fromRfc8601DateTime("01/01/2024 00:00:00");
LocalDateTime timestampEnd = DateTimeHelper.fromRfc8601DateTime("01/08/2024 00:00:00");
Boolean useUtc = false;
Integer aggregateLevel = 0;

dataApi.getDataAsync(deviceIds, dataSignalIds, timestampStart, timestampEnd, useUtc, null, null, aggregateLevel, null).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Data400ErrorException) {
        Data400ErrorException data400ErrorException = (Data400ErrorException) cause;
        data400ErrorException.printStackTrace();
    } else if (cause instanceof Data429ErrorException) {
        Data429ErrorException data429ErrorException = (Data429ErrorException) cause;
        data429ErrorException.printStackTrace();
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
    "aggregate": "device",
    "aggregateId": 1,
    "aggregatePathNames": [],
    "deviceIds": [
      1
    ],
    "resolution": "hourly",
    "calculation": "sum",
    "dataSignal": {
      "dataSignalId": 1,
      "title": "Wind speed",
      "unit": "m/s"
    },
    "data": {
      "2020-01-01T00:00:00": 6.89,
      "2020-01-01T01:00:00": 8.33
    }
  },
  {
    "aggregate": "device",
    "aggregateId": 1,
    "aggregatePathNames": [],
    "deviceIds": [
      1
    ],
    "resolution": "hourly",
    "calculation": "sum",
    "dataSignal": {
      "dataSignalId": 5,
      "title": "Power",
      "unit": "kW"
    },
    "data": {
      "2020-01-01T00:00:00": 584.33,
      "2020-01-01T01:00:00": 1014
    }
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Data400ErrorException`](../../doc/models/data-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Data429ErrorException`](../../doc/models/data-429-error-exception.md) |


# Get Real Time Data

Gets the most recent data point for each
specified device and data signal. The timestamps are in UTC.

_🔐 This endpoint requires the **Data** endpoint permission._

_This request can also be made using the POST method,
with a request to `realtimedata.json` and
a JSON request body instead of query parameters._

```java
CompletableFuture<ApiResponse<List<DataRealTimeItem>>> getRealTimeDataAsync(
    final List<Integer> deviceIds,
    final List<Integer> dataSignalIds,
    final AggregateMode aggregate,
    final Integer aggregateLevel,
    final CalculationModeRealTime calculation)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `deviceIds` | `List<Integer>` | Query, Required | Which devices to get data for.<br><br>**Constraints**: `>= 1` |
| `dataSignalIds` | `List<Integer>` | Query, Required | Which data signals to get data for.<br><br>**Constraints**: `>= 1` |
| `aggregate` | [`AggregateMode`](../../doc/models/aggregate-mode.md) | Query, Optional | How the data should be aggregated with regards to device(s) or site(s). |
| `aggregateLevel` | `Integer` | Query, Optional | When AggregateMode `siteLevel` is used this parameter controls down to which level in the hierarchy to aggregate.<br><br>**Default**: `0` |
| `calculation` | [`CalculationModeRealTime`](../../doc/models/calculation-mode-real-time.md) | Query, Optional | The calculation used when aggregating data, both over time and across devices. The default is the data signal default. |

## Response Type

**200**: The most recent data points grouped by data signal and aggregate.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<DataRealTimeItem>`](../../doc/models/data-real-time-item.md).

## Example Usage

```java
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

List<Integer> dataSignalIds = Arrays.asList(
    1,
    5
);

Integer aggregateLevel = 0;

dataApi.getRealTimeDataAsync(deviceIds, dataSignalIds, null, aggregateLevel, null).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Realtimedata400ErrorException) {
        Realtimedata400ErrorException realtimedata400ErrorException = (Realtimedata400ErrorException) cause;
        realtimedata400ErrorException.printStackTrace();
    } else if (cause instanceof Realtimedata429ErrorException) {
        Realtimedata429ErrorException realtimedata429ErrorException = (Realtimedata429ErrorException) cause;
        realtimedata429ErrorException.printStackTrace();
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
    "aggregate": "device",
    "aggregateId": 24,
    "aggregatePathNames": [],
    "deviceIds": [
      24
    ],
    "calculation": "sum",
    "dataSignal": {
      "dataSignalId": 5,
      "title": "Power",
      "unit": "kW"
    },
    "data": {
      "2020-03-17T12:50:02Z": 2174
    }
  },
  {
    "aggregate": "device",
    "aggregateId": 24,
    "aggregatePathNames": [],
    "deviceIds": [
      24
    ],
    "calculation": "sum",
    "dataSignal": {
      "dataSignalId": 1,
      "title": "Wind speed",
      "unit": "m/s"
    },
    "data": {
      "2020-03-17T12:50:02Z": 12.2
    }
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Realtimedata400ErrorException`](../../doc/models/realtimedata-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Realtimedata429ErrorException`](../../doc/models/realtimedata-429-error-exception.md) |


# Get Data per Category

Gets signal data aggregated per availability contract category.

_🔐 This endpoint requires the **Data** and **Statuses** endpoint permissions._

_This request can also be made using the POST method,
with a request to `datapercategory.json` and
a JSON request body instead of query parameters._

```java
CompletableFuture<ApiResponse<DatapercategoryResponse1>> getDataPerCategoryAsync(
    final List<Integer> deviceIds,
    final int dataSignalId,
    final LocalDateTime timestampStart,
    final LocalDateTime timestampEnd,
    final AggregateMode aggregate,
    final Integer aggregateLevel,
    final List<StatusCategory> category,
    final ContractType1 contractType)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `deviceIds` | `List<Integer>` | Query, Required | Which devices to get data for.<br><br>**Constraints**: `>= 1` |
| `dataSignalId` | `int` | Query, Required | Which signal to get data for; only Lost Production signals are supported at the moment.<br><br>**Constraints**: `>= 1` |
| `timestampStart` | `LocalDateTime` | Query, Required | The beginning of the time interval to get data for (inclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The start timestamp **is** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `timestampEnd` | `LocalDateTime` | Query, Required | The end of the time interval to get data for (exclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The end timestamp is **not** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `aggregate` | [`AggregateMode`](../../doc/models/aggregate-mode.md) | Query, Optional | How the data should be aggregated with regards to device(s) or site(s). |
| `aggregateLevel` | `Integer` | Query, Optional | When AggregateMode `siteLevel` is used this parameter controls down to which level in the hierarchy to aggregate.<br><br>**Default**: `0` |
| `category` | [`List<StatusCategory>`](../../doc/models/status-category.md) | Query, Optional | Which status categories to include. By default all categories are included. |
| `contractType` | [`ContractType1`](../../doc/models/contract-type-1.md) | Query, Optional | Which contract type to use if using multiple availability contracts. |

## Response Type

**200**: The data grouped by aggregate (device, site, etc.) and contract category.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`DatapercategoryResponse1`](../../doc/models/datapercategory-response-1.md).

## Example Usage

```java
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

int dataSignalId = 248;
LocalDateTime timestampStart = DateTimeHelper.fromRfc8601DateTime("01/01/2024 00:00:00");
LocalDateTime timestampEnd = DateTimeHelper.fromRfc8601DateTime("01/08/2024 00:00:00");
Integer aggregateLevel = 0;
List<StatusCategory> category = Arrays.asList(
    StatusCategory.STOP
);


dataApi.getDataPerCategoryAsync(deviceIds, dataSignalId, timestampStart, timestampEnd, null, aggregateLevel, category, null).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Datapercategory400ErrorException) {
        Datapercategory400ErrorException datapercategory400ErrorException = (Datapercategory400ErrorException) cause;
        datapercategory400ErrorException.printStackTrace();
    } else if (cause instanceof Datapercategory429ErrorException) {
        Datapercategory429ErrorException datapercategory429ErrorException = (Datapercategory429ErrorException) cause;
        datapercategory429ErrorException.printStackTrace();
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
  "dataSignal": {
    "dataSignalId": 248,
    "title": "Lost Production (Contractual)",
    "unit": "kWh"
  },
  "calculation": "sum",
  "data": [
    {
      "aggregateId": 6,
      "aggregatePathNames": [],
      "deviceIds": [
        1,
        2,
        3
      ],
      "contractTitle": "Vestas 1",
      "categoryTitle": "Icing",
      "categoryTime": "available",
      "value": 104.55,
      "duration": 150
    },
    {
      "aggregateId": 6,
      "aggregatePathNames": [],
      "deviceIds": [
        1,
        2,
        3
      ],
      "contractTitle": "Vestas 1",
      "categoryTitle": "Utility",
      "categoryTime": "excluded",
      "value": 73,
      "duration": 50.3
    }
  ]
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Datapercategory400ErrorException`](../../doc/models/datapercategory-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Datapercategory429ErrorException`](../../doc/models/datapercategory-429-error-exception.md) |


# Get High Res Data

Gets high resolution data for a data signal for each
specified device. The timestamps are in UTC.

The endpoint returns up to an hour's worth of high resolution data for the provided device IDs and data signal ID.
It is possible to request data for up to 10 separate devices and one data signal ID.
Timestamp start and end are optional. The default time span returned is the latest hour.
If supplied, timestamp start must be within the past 12 hours.
Timestamp end will by default be an hour after timestamp start but can be set for shorter intervals.

There is no high resolution data available for data signals that are calculated.
The data for those signals can be retrieved through the data endpoint.

_🔐 This endpoint requires the **HighResolution** endpoint permission._

```java
CompletableFuture<ApiResponse<List<HighresdataResponse>>> getHighResDataAsync(
    final List<Integer> deviceIds,
    final int dataSignalId,
    final LocalDateTime timestampStart,
    final LocalDateTime timestampEnd)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `deviceIds` | `List<Integer>` | Query, Required | Which devices to get data for.<br><br>**Constraints**: `>= 1` |
| `dataSignalId` | `int` | Query, Required | Which data signal to get data for.<br><br>**Constraints**: `>= 1` |
| `timestampStart` | `LocalDateTime` | Query, Optional | The beginning of the time interval to get data for (inclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The start timestamp **is** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `timestampEnd` | `LocalDateTime` | Query, Optional | The end of the time interval to get data for (exclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The end timestamp is **not** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |

## Response Type

**200**: High resolution data from different devices for a certain data signal.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<HighresdataResponse>`](../../doc/models/highresdata-response.md).

## Example Usage

```java
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

int dataSignalId = 1;
LocalDateTime timestampStart = DateTimeHelper.fromRfc8601DateTime("01/01/2024 00:00:00");
LocalDateTime timestampEnd = DateTimeHelper.fromRfc8601DateTime("01/08/2024 00:00:00");

dataApi.getHighResDataAsync(deviceIds, dataSignalId, timestampStart, timestampEnd).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Highresdata400ErrorException) {
        Highresdata400ErrorException highresdata400ErrorException = (Highresdata400ErrorException) cause;
        highresdata400ErrorException.printStackTrace();
    } else if (cause instanceof Highresdata429ErrorException) {
        Highresdata429ErrorException highresdata429ErrorException = (Highresdata429ErrorException) cause;
        highresdata429ErrorException.printStackTrace();
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
    "deviceId": 24,
    "dataSignal": {
      "dataSignalId": 1,
      "title": "Wind speed",
      "unit": "m/s"
    },
    "data": {
      "2021-04-09T04:14:18Z": 6.21827459335327,
      "2021-04-09T04:14:48Z": 6.46509933471681,
      "2021-04-09T04:15:18Z": 7.41247510910034,
      "2021-04-09T04:15:48Z": 6.71687459945679,
      "2021-04-09T04:16:20Z": 5.66159963607788
    }
  },
  {
    "deviceId": 25,
    "dataSignal": {
      "dataSignalId": 1,
      "title": "Wind speed",
      "unit": "m/s"
    },
    "data": {
      "2021-04-09T04:14:18Z": 5.81789970397949,
      "2021-04-09T04:14:48Z": 5.43127489089966,
      "2021-04-09T04:15:18Z": 7.41247510910034,
      "2021-04-09T04:15:48Z": 5.58427476882935,
      "2021-04-09T04:16:20Z": 6.80189990997314
    }
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Highresdata400ErrorException`](../../doc/models/highresdata-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Highresdata429ErrorException`](../../doc/models/highresdata-429-error-exception.md) |

