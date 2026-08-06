
# Custom Header Signature



Documentation for accessing and setting credentials for ApiKeyHeaderAuth.

## Auth Credentials

| Name | Type | Description | Setter | Getter |
|  --- | --- | --- | --- | --- |
| X-Api-Key | `String` | - | `xApiKey` | `getXApiKey()` |



**Note:** Auth credentials can be set using `customHeaderAuthenticationCredentials` in the client builder and accessed through `getCustomHeaderAuthenticationCredentials` method in the client instance.

## Usage Example

### Client Initialization

You must provide credentials in the client as shown in the following code snippet.

```java
import cloud.greenbyte.intro.GreenbyteClient;
import cloud.greenbyte.intro.authentication.CustomHeaderAuthenticationModel;

public class Program {
    public static void main(String[] args) {
        GreenbyteClient client = new GreenbyteClient.Builder()
            .customHeaderAuthenticationCredentials(new CustomHeaderAuthenticationModel.Builder(
                    "X-Api-Key"
                )
                .build())
            .build();
    }
}
```


