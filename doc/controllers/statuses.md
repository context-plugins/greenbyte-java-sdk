# Statuses

This section contains operations related to device statuses. Device statuses are related to availability contracts.
[Availability contracts in the Greenbyte Platform documentation](https://help.greenbyte.com/Greenbyte/en/availability-contracts.html)

```java
StatusesApi statusesApi = client.getStatusesApi();
```

## Class Name

`StatusesApi`

## Methods

* [Get Statuses](../../doc/controllers/statuses.md#get-statuses)
* [Get Active Statuses](../../doc/controllers/statuses.md#get-active-statuses)


# Get Statuses

Gets statuses for multiple devices during the given time period.
The timestamps are in the time zone configured in the Greenbyte Platform.
Use the useUtc flag to get timestamps in UTC.

_🔐 This endpoint requires the **Statuses** endpoint permission._

_This request can also be made using the POST method,
with a request to `status.json` and
a JSON request body instead of query parameters._

```java
CompletableFuture<ApiResponse<List<StatusItem>>> getStatusesAsync(
    final List<Integer> deviceIds,
    final LocalDateTime timestampStart,
    final LocalDateTime timestampEnd,
    final List<StatusCategory> category,
    final Integer lostProductionSignalId,
    final List<String> fields,
    final List<String> sortBy,
    final Boolean sortAsc,
    final Integer pageSize,
    final Integer page,
    final Boolean useUtc,
    final ContractType1 contractType)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `deviceIds` | `List<Integer>` | Query, Required | Which devices to get statuses for.<br><br>**Constraints**: `>= 1` |
| `timestampStart` | `LocalDateTime` | Query, Required | The beginning of the time interval to get data for (inclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The start timestamp **is** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `timestampEnd` | `LocalDateTime` | Query, Required | The end of the time interval to get data for (exclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The end timestamp is **not** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `category` | [`List<StatusCategory>`](../../doc/models/status-category.md) | Query, Optional | Which status categories to get statuses for. |
| `lostProductionSignalId` | `Integer` | Query, Optional | Which data signal to use for calculating lost production. Defaults to the configured default lost production signal.<br><br>**Constraints**: `>= 1` |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `StatusItem` schema (See Response Type). By default all fields are included. |
| `sortBy` | `List<String>` | Query, Optional | Which fields to sort the response items by. |
| `sortAsc` | `Boolean` | Query, Optional | Whether to sort the items in ascending order.<br><br>**Default**: `false` |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |
| `contractType` | [`ContractType1`](../../doc/models/contract-type-1.md) | Query, Optional | Which contract type to use if using multiple availability contracts. |

## Response Type

**200**: A list of statuses with related data.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<StatusItem>`](../../doc/models/status-item.md).

## Example Usage

```java
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

LocalDateTime timestampStart = DateTimeHelper.fromRfc8601DateTime("01/01/2024 00:00:00");
LocalDateTime timestampEnd = DateTimeHelper.fromRfc8601DateTime("01/08/2024 00:00:00");
Integer lostProductionSignalId = 432;
List<String> fields = Arrays.asList(
    "deviceId",
    "message",
    "lostProduction"
);

Boolean sortAsc = false;
Integer pageSize = 50;
Integer page = 1;
Boolean useUtc = false;

statusesApi.getStatusesAsync(deviceIds, timestampStart, timestampEnd, null, lostProductionSignalId, fields, null, sortAsc, pageSize, page, useUtc, null).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Status400ErrorException) {
        Status400ErrorException status400ErrorException = (Status400ErrorException) cause;
        status400ErrorException.printStackTrace();
    } else if (cause instanceof Status429ErrorException) {
        Status429ErrorException status429ErrorException = (Status429ErrorException) cause;
        status429ErrorException.printStackTrace();
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
    "turbineStatusId": 8983231,
    "lostProductionSignal": {
      "dataSignalId": 432,
      "title": "Lost Production to Downtime",
      "unit": "kWh"
    },
    "lostProduction": 3899.53096699953,
    "categoryIec": "Requested Shutdown",
    "categoryContract": "Preventive Maintenance",
    "categoryGlobalContract": null,
    "categoryCustomContract": null,
    "subStatus": [],
    "deviceId": 25,
    "timestampStart": "2021-12-12T22:07:10",
    "timestampEnd": "2021-12-13T07:16:48",
    "hasTimestampEnd": true,
    "category": "stop",
    "code": 615,
    "message": "Maintenance: Maintenance",
    "comment": null,
    "acknowledged": false,
    "component": {
      "componentId": 123,
      "componentName": "Converter System",
      "componentTag": "MSE"
    }
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Status400ErrorException`](../../doc/models/status-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Status429ErrorException`](../../doc/models/status-429-error-exception.md) |


# Get Active Statuses

Gets active statuses for multiple devices.
The timestamps are in the time zone configured in the Greenbyte Platform.
Use the useUtc flag to get timestamps in UTC.

_🔐 This endpoint requires the **Statuses** endpoint permission._

_This request can also be made using the POST method,
with a request to `activestatus.json` and
a JSON request body instead of query parameters._

```java
CompletableFuture<ApiResponse<List<StatusItem>>> getActiveStatusesAsync(
    final List<Integer> deviceIds,
    final List<StatusCategory> category,
    final Integer lostProductionSignalId,
    final List<String> fields,
    final List<String> sortBy,
    final Boolean sortAsc,
    final Integer pageSize,
    final Integer page,
    final Boolean useUtc,
    final ContractType1 contractType)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `deviceIds` | `List<Integer>` | Query, Required | Which devices to get statuses for.<br><br>**Constraints**: `>= 1` |
| `category` | [`List<StatusCategory>`](../../doc/models/status-category.md) | Query, Optional | Which status categories to get statuses for. |
| `lostProductionSignalId` | `Integer` | Query, Optional | Which data signal to use for calculating lost production. Defaults to the configured default lost production signal.<br><br>**Constraints**: `>= 1` |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `StatusItem` schema (See Response Type). By default all fields are included. |
| `sortBy` | `List<String>` | Query, Optional | Which fields to sort the response items by. |
| `sortAsc` | `Boolean` | Query, Optional | Whether to sort the items in ascending order.<br><br>**Default**: `false` |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |
| `contractType` | [`ContractType1`](../../doc/models/contract-type-1.md) | Query, Optional | Which contract type to use if using multiple availability contracts. |

## Response Type

**200**: A list of active statuses with related data.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<StatusItem>`](../../doc/models/status-item.md).

## Example Usage

```java
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

Integer lostProductionSignalId = 432;
List<String> fields = Arrays.asList(
    "deviceId",
    "message",
    "lostProduction"
);

Boolean sortAsc = false;
Integer pageSize = 50;
Integer page = 1;
Boolean useUtc = false;

statusesApi.getActiveStatusesAsync(deviceIds, null, lostProductionSignalId, fields, null, sortAsc, pageSize, page, useUtc, null).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Activestatus400ErrorException) {
        Activestatus400ErrorException activestatus400ErrorException = (Activestatus400ErrorException) cause;
        activestatus400ErrorException.printStackTrace();
    } else if (cause instanceof Activestatus429ErrorException) {
        Activestatus429ErrorException activestatus429ErrorException = (Activestatus429ErrorException) cause;
        activestatus429ErrorException.printStackTrace();
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
    "lostProduction": 696.16,
    "lostProductionSignal": {
      "dataSignalId": 432,
      "title": "Lost Production to Downtime",
      "unit": "kWh"
    },
    "deviceId": 4,
    "code": 8000,
    "message": "Maintenance: Maintenance"
  },
  {
    "lostProduction": 0,
    "lostProductionSignal": {
      "dataSignalId": 432,
      "title": "Lost Production to Downtime",
      "unit": "kWh"
    },
    "deviceId": 4,
    "code": 21001,
    "message": "Cable twisted: Left (2-3 turns)"
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Activestatus400ErrorException`](../../doc/models/activestatus-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Activestatus429ErrorException`](../../doc/models/activestatus-429-error-exception.md) |

