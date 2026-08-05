# Predict

```java
PredictApi predictApi = client.getPredictApi();
```

## Class Name

`PredictApi`


# Get Predict Alerts

Gets a list of Predict alerts based on filter criteria. The timestamps are in the time zone configured in the Greenbyte Platform. Use the useUtc flag to get timestamps in UTC.

_🔐 This endpoint requires the **Predict** endpoint permission._

_This is a beta feature. Some details might change before it is
released as a stable version._

```java
CompletableFuture<ApiResponse<List<PredictAlertsResponse>>> getPredictAlertsAsync(
    final List<Integer> deviceIds,
    final LocalDateTime timestampStart,
    final LocalDateTime timestampEnd,
    final List<Integer> siteIds,
    final List<Integer> componentIds,
    final PredictStatus status,
    final PredictSeverity severity,
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
| `deviceIds` | `List<Integer>` | Query, Required | What devices to get alerts for.<br><br>**Constraints**: `>= 1` |
| `timestampStart` | `LocalDateTime` | Query, Required | The beginning of the time interval to get data for (inclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The start timestamp **is** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `timestampEnd` | `LocalDateTime` | Query, Required | The end of the time interval to get data for (exclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The end timestamp is **not** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `siteIds` | `List<Integer>` | Query, Optional | What sites to get alerts for.<br><br>**Constraints**: `>= 1` |
| `componentIds` | `List<Integer>` | Query, Optional | What components to get alerts for.<br><br>**Constraints**: `>= 1` |
| `status` | [`PredictStatus`](../../doc/models/predict-status.md) | Query, Optional | Which alert status to get alerts for. |
| `severity` | [`PredictSeverity`](../../doc/models/predict-severity.md) | Query, Optional | What severity of alerts to get: high severity or low severity. If<br>not set, both high and low severity alerts are included. |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `PredictAlert` schema (See Response Type). By default all fields are included. |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A list of Predict alerts.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<PredictAlertsResponse>`](../../doc/models/predict-alerts-response.md).

## Example Usage

```java
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

LocalDateTime timestampStart = DateTimeHelper.fromRfc8601DateTime("01/01/2024 00:00:00");
LocalDateTime timestampEnd = DateTimeHelper.fromRfc8601DateTime("01/08/2024 00:00:00");
List<Integer> siteIds = Arrays.asList(
    1,
    2,
    3
);

List<Integer> componentIds = Arrays.asList(
    1,
    2,
    3
);

List<String> fields = Arrays.asList(
    "deviceId",
    "highSeverity"
);

Integer pageSize = 50;
Integer page = 1;
Boolean useUtc = false;

predictApi.getPredictAlertsAsync(deviceIds, timestampStart, timestampEnd, siteIds, componentIds, null, null, fields, pageSize, page, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof PredictAlerts400ErrorException) {
        PredictAlerts400ErrorException predictAlerts400ErrorException = (PredictAlerts400ErrorException) cause;
        predictAlerts400ErrorException.printStackTrace();
    } else if (cause instanceof PredictAlerts429ErrorException) {
        PredictAlerts429ErrorException predictAlerts429ErrorException = (PredictAlerts429ErrorException) cause;
        predictAlerts429ErrorException.printStackTrace();
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
    "deviceId": 260,
    "siteId": 19,
    "componentAlert": {
      "componentId": 46,
      "componentName": "Main gear oil system"
    },
    "highSeverity": true,
    "status": "resolved",
    "comments": [
      {
        "text": "Found high temperatures. Reported to OM team.",
        "userName": "Bill Bao",
        "timestamp": "2019-04-16T12:48:16"
      }
    ],
    "resolvedBy": "Jens Genberg",
    "timestampResolved": "2019-10-25T09:29:55",
    "actionTaken": "Replacement",
    "componentResolved": {
      "componentId": 77,
      "componentName": "Main gear oil system"
    },
    "dismissedBy": null,
    "timestampDismissed": null,
    "recommendations": null
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`PredictAlerts400ErrorException`](../../doc/models/predict-alerts-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`PredictAlerts429ErrorException`](../../doc/models/predict-alerts-429-error-exception.md) |

