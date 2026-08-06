
# Client Class Documentation

The following parameters are configurable for the API Client:

| Parameter | Type | Description |
|  --- | --- | --- |
| customer | `String` | The customer sub-domain<br>*Default*: `"intro"` |
| environment | [`Environment`](../README.md#environments) | The API environment. <br> **Default: `Environment.PRODUCTION`** |
| httpClientConfig | [`Consumer<HttpClientConfiguration.Builder>`](../doc/http-client-configuration-builder.md) | Set up Http Client Configuration instance. |
| loggingConfig | [`Consumer<ApiLoggingConfiguration.Builder>`](../doc/api-logging-configuration-builder.md) | Set up Logging Configuration instance. |
| customHeaderAuthenticationCredentials | [`CustomHeaderAuthenticationCredentials`](auth/custom-header-signature.md) | The Credentials Setter for Custom Header Signature |

The API client can be initialized as follows:

```java
import cloud.greenbyte.intro.Environment;
import cloud.greenbyte.intro.GreenbyteClient;
import cloud.greenbyte.intro.authentication.CustomHeaderAuthenticationModel;
import cloud.greenbyte.intro.exceptions.ApiException;
import cloud.greenbyte.intro.http.response.ApiResponse;
import org.slf4j.event.Level;

public class Program {
    public static void main(String[] args) {
        GreenbyteClient client = new GreenbyteClient.Builder()
            .loggingConfig(builder -> builder
                    .level(Level.DEBUG)
                    .requestConfig(logConfigBuilder -> logConfigBuilder.body(true))
                    .responseConfig(logConfigBuilder -> logConfigBuilder.headers(true)))
            .httpClientConfig(configBuilder -> configBuilder
                    .timeout(0))
            .customHeaderAuthenticationCredentials(new CustomHeaderAuthenticationModel.Builder(
                    "X-Api-Key"
                )
                .build())
            .environment(Environment.PRODUCTION)
            .customer("intro")
            .build();

    }
}
```

## Greenbyte APIClient Class

The gateway for the SDK. This class acts as a factory for the Apis and also holds the configuration of the SDK.

### Apis

| Name | Description | Return Type |
|  --- | --- | --- |
| `getDataApi()` | Provides access to Data controller. | `DataApi` |
| `getStatusesApi()` | Provides access to Statuses controller. | `StatusesApi` |
| `getConfigurationdataApi()` | Provides access to Configurationdata controller. | `ConfigurationdataApi` |
| `getAssetsApi()` | Provides access to Assets controller. | `AssetsApi` |
| `getAlertsApi()` | Provides access to Alerts controller. | `AlertsApi` |
| `getPlanApi()` | Provides access to Plan controller. | `PlanApi` |
| `getPredictApi()` | Provides access to Predict controller. | `PredictApi` |

### Methods

| Name | Description | Return Type |
|  --- | --- | --- |
| `shutdown()` | Shutdown the underlying HttpClient instance. | `void` |
| `getEnvironment()` | Current API environment. | `Environment` |
| `getCustomer()` | The customer sub-domain | `String` |
| `getHttpClient()` | The HTTP Client instance to use for making HTTP requests. | `HttpClient` |
| `getHttpClientConfig()` | Http Client Configuration instance. | [`ReadonlyHttpClientConfiguration`](../doc/http-client-configuration.md) |
| `getLoggingConfig()` | Logging Configuration instance. | [`ReadonlyLoggingConfiguration`](../doc/api-logging-configuration.md) |
| `getCustomHeaderAuthenticationCredentials()` | The credentials to use with CustomHeaderAuthentication. | [`CustomHeaderAuthenticationCredentials`](auth/custom-header-signature.md) |
| `getBaseUri(Server server)` | Get base URI by current environment | `String` |
| `getBaseUri()` | Get base URI by current environment | `String` |

