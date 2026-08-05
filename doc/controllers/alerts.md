# Alerts

This section contains operations related to device alerts.

## Alerts

Alerts analyze incoming data based on a set of rules defined by a user. For example, you can set up rules to check that a data signal is above a certain threshold, or that the data signals of two different units follow the same pattern. This can help you gain a better understanding of your portfolio.

```java
AlertsApi alertsApi = client.getAlertsApi();
```

## Class Name

`AlertsApi`

## Methods

* [Get Active Alerts](../../doc/controllers/alerts.md#get-active-alerts)
* [Get Alerts](../../doc/controllers/alerts.md#get-alerts)


# Get Active Alerts

Gets active alerts for multiple devices.
The timestamps are in the time zone configured in the Greenbyte Platform.
Use the useUtc flag to get timestamps in UTC.

_🔐 This endpoint requires the **Alerts** endpoint permission._

_This request can also be made using the POST method,
with a request to `activealerts.json` and
a JSON request body instead of query parameters._

```java
CompletableFuture<ApiResponse<List<AlertItem>>> getActiveAlertsAsync(
    final List<Integer> deviceIds,
    final List<String> fields,
    final List<String> sortBy,
    final Boolean sortAsc,
    final Integer pageSize,
    final Integer page,
    final Boolean useUtc)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `deviceIds` | `List<Integer>` | Query, Required | What devices to get alerts for.<br><br>**Constraints**: `>= 1` |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `AlertItem` schema (See Response Type). By default all fields are included. |
| `sortBy` | `List<String>` | Query, Optional | Which fields to sort the response items by. |
| `sortAsc` | `Boolean` | Query, Optional | Whether to sort the items in ascending order.<br><br>**Default**: `false` |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A list of alerts.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<AlertItem>`](../../doc/models/alert-item.md).

## Example Usage

```java
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

List<String> fields = Arrays.asList(
    "ruleId",
    "timestampStart"
);

Boolean sortAsc = false;
Integer pageSize = 50;
Integer page = 1;
Boolean useUtc = false;

alertsApi.getActiveAlertsAsync(deviceIds, fields, null, sortAsc, pageSize, page, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Activealerts400ErrorException) {
        Activealerts400ErrorException activealerts400ErrorException = (Activealerts400ErrorException) cause;
        activealerts400ErrorException.printStackTrace();
    } else if (cause instanceof Activealerts429ErrorException) {
        Activealerts429ErrorException activealerts429ErrorException = (Activealerts429ErrorException) cause;
        activealerts429ErrorException.printStackTrace();
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
    "deviceId": 179,
    "ruleId": 104,
    "description": "Power curve less than 90%",
    "details": "Evaluation period: 6 hours\nData coverage: 70% of devices\nExclude data during: Active Stop or Warning status\nData condition: The consecutive value of the performance index of Backen 2 is less than 90%\nData condition: The consecutive value of the wind speed of Backen 2 is greater than 5 m/s",
    "timestampStart": "2020-03-18T06:50:00",
    "timestampEnd": "2020-03-18T14:00:00",
    "message": "Low Performance Wind",
    "comment": "A comment"
  },
  {
    "deviceId": 183,
    "ruleId": 104,
    "description": "Power curve less than 90%",
    "details": "Evaluation period: 6 hours\nData coverage: 70% of devices\nExclude data during: Active Stop or Warning status\nData condition: The consecutive value of the performance index of Backen 6 is less than 90%\nData condition: The consecutive value of the wind speed of Backen 6 is greater than 5 m/s",
    "timestampStart": "2020-03-18T07:40:00",
    "timestampEnd": "2020-03-18T14:00:00",
    "message": "Low Performance Wind",
    "comment": "A comment"
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Activealerts400ErrorException`](../../doc/models/activealerts-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Activealerts429ErrorException`](../../doc/models/activealerts-429-error-exception.md) |


# Get Alerts

Gets alerts for multiple devices and the given time period.
The timestamps are in the time zone configured in the Greenbyte Platform.
Use the useUtc flag to get timestamps in UTC.

_🔐 This endpoint requires the **Alerts** endpoint permission._

_This request can also be made using the POST method,
with a request to `alerts.json` and
a JSON request body instead of query parameters._

```java
CompletableFuture<ApiResponse<List<AlertItem>>> getAlertsAsync(
    final List<Integer> deviceIds,
    final LocalDateTime timestampStart,
    final LocalDateTime timestampEnd,
    final List<String> fields,
    final List<String> sortBy,
    final Boolean sortAsc,
    final Integer pageSize,
    final Integer page,
    final Boolean useUtc)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `deviceIds` | `List<Integer>` | Query, Required | What devices to get alerts for.<br><br>**Constraints**: `>= 1` |
| `timestampStart` | `LocalDateTime` | Query, Required | The beginning of the time interval to get data for (inclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The start timestamp **is** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `timestampEnd` | `LocalDateTime` | Query, Required | The end of the time interval to get data for (exclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The end timestamp is **not** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `AlertItem` schema (See Response Type). By default all fields are included. |
| `sortBy` | `List<String>` | Query, Optional | Which fields to sort the response items by. |
| `sortAsc` | `Boolean` | Query, Optional | Whether to sort the items in ascending order.<br><br>**Default**: `false` |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A list of alerts.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<AlertItem>`](../../doc/models/alert-item.md).

## Example Usage

```java
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

LocalDateTime timestampStart = DateTimeHelper.fromRfc8601DateTime("01/01/2024 00:00:00");
LocalDateTime timestampEnd = DateTimeHelper.fromRfc8601DateTime("01/08/2024 00:00:00");
List<String> fields = Arrays.asList(
    "ruleId",
    "timestampStart"
);

Boolean sortAsc = false;
Integer pageSize = 50;
Integer page = 1;
Boolean useUtc = false;

alertsApi.getAlertsAsync(deviceIds, timestampStart, timestampEnd, fields, null, sortAsc, pageSize, page, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Alerts400ErrorException) {
        Alerts400ErrorException alerts400ErrorException = (Alerts400ErrorException) cause;
        alerts400ErrorException.printStackTrace();
    } else if (cause instanceof Alerts429ErrorException) {
        Alerts429ErrorException alerts429ErrorException = (Alerts429ErrorException) cause;
        alerts429ErrorException.printStackTrace();
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
    "deviceId": 179,
    "ruleId": 104,
    "description": "Power curve less than 90%",
    "details": "Evaluation period: 6 hours\nData coverage: 70% of devices\nExclude data during: Active Stop or Warning status\nData condition: The consecutive value of the performance index of Backen 2 is less than 90%\nData condition: The consecutive value of the wind speed of Backen 2 is greater than 5 m/s",
    "timestampStart": "2020-03-18T06:50:00",
    "timestampEnd": "2020-03-18T14:00:00",
    "message": "Low Performance Wind",
    "comment": "A comment"
  },
  {
    "deviceId": 183,
    "ruleId": 104,
    "description": "Power curve less than 90%",
    "details": "Evaluation period: 6 hours\nData coverage: 70% of devices\nExclude data during: Active Stop or Warning status\nData condition: The consecutive value of the performance index of Backen 6 is less than 90%\nData condition: The consecutive value of the wind speed of Backen 6 is greater than 5 m/s",
    "timestampStart": "2020-03-18T07:40:00",
    "timestampEnd": "2020-03-18T14:00:00",
    "message": "Low Performance Wind",
    "comment": "A comment"
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Alerts400ErrorException`](../../doc/models/alerts-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Alerts429ErrorException`](../../doc/models/alerts-429-error-exception.md) |

