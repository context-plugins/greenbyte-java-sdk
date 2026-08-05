# Configurationdata

```java
ConfigurationdataApi configurationdataApi = client.getConfigurationdataApi();
```

## Class Name

`ConfigurationdataApi`


# Get Configuration

Gets your system-wide configuration data.

_🔐 This endpoint requires the **Configuration** endpoint permission._

_This request can also be made using the POST method,
with a request to `configuration.json` and
a JSON request body instead of query parameters._

```java
CompletableFuture<ApiResponse<List<ConfigurationItem>>> getConfigurationAsync()
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Response Type

**200**: An array with a single item containing configuration data.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<ConfigurationItem>`](../../doc/models/configuration-item.md).

## Example Usage

```java
configurationdataApi.getConfigurationAsync().thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Configuration400ErrorException) {
        Configuration400ErrorException configuration400ErrorException = (Configuration400ErrorException) cause;
        configuration400ErrorException.printStackTrace();
    } else if (cause instanceof Configuration429ErrorException) {
        Configuration429ErrorException configuration429ErrorException = (Configuration429ErrorException) cause;
        configuration429ErrorException.printStackTrace();
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
    "client": {
      "title": "Intro (Greenbyte AB)",
      "tag": "intro",
      "urlWeb": "https://intro.greenbyte.cloud/",
      "urlApi": "https://intro.greenbyte.cloud/api/2/"
    },
    "timeZone": {
      "title": "Europe/Stockholm",
      "utcOffset": 1,
      "utcOffsetDst": 2,
      "dstTimestampStart": "2020-03-29T01:00:00",
      "dstTimestampEnd": "2020-10-25T01:00:00"
    },
    "dataSignals": {
      "availabilityTimeDataSignalId": 430,
      "availabilityProductionDataSignalId": 445,
      "lostProductionDataSignalId": 432,
      "performanceDataSignalId": 436
    }
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Configuration400ErrorException`](../../doc/models/configuration-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Configuration429ErrorException`](../../doc/models/configuration-429-error-exception.md) |

