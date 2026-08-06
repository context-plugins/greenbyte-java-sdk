
# Getting Started with Greenbyte API

## Building

Supported Java version is **8+**.

The generated code uses a few Maven dependencies e.g., Jackson, OkHttp,
and Apache HttpClient. The reference to these dependencies is already
added in the pom.xml file will be installed automatically. Therefore,
you will need internet access for a successful build.

* In order to open the client library in Eclipse click on `File -> Import`.

![Importing SDK into Eclipse - Step 1](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=import0)

* In the import dialog, select `Existing Java Project` and click `Next`.

![Importing SDK into Eclipse - Step 2](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=import1)

* Browse to locate the folder containing the source code. Select the detected location of the project and click `Finish`.

![Importing SDK into Eclipse - Step 3](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=import2)

* Upon successful import, the project will be automatically built by Eclipse after automatically resolving the dependencies.

![Importing SDK into Eclipse - Step 4](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=import3)

* After successfully building the project, the client library needs to be installed as a Maven package in your local cache. Right-click on the project, select `Show in Local Terminal -> Terminal` or use `Ctrl + Alt + T` to open Terminal.

![Importing SDK into Eclipse - Step 5](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=openTerminal)

* In the terminal dialog, run the following command to install client library.

```
mvn install -Dmaven.test.skip=true -Dmaven.javadoc.skip=true
```

![Importing SDK into Eclipse - Step 6](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=installCommand)

## Installation

The following section explains how to use the Greenbyte library in a new project.

### 1. Starting a new project

For starting a new project, click the menu command `File > New > Project`.

![Add a new project in Eclipse](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=createNewProject0)

Next, choose `Maven > Maven Project` and click `Next`.

![Create a new Maven Project - Step 1](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=createNewProject1)

Here, make sure to use the current workspace by choosing `Use default Workspace location`, as shown in the picture below and click `Next`.

![Create a new Maven Project - Step 2](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=createNewProject2)

Following this, select the *quick start* project type to create a simple project with an existing class and a `main` method. To do this, choose `maven-archetype-quickstart` item from the list and click `Next`.

![Create a new Maven Project - Step 3](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=createNewProject3)

In the last step, provide a `Group Id` and `Artifact Id` as shown in the picture below and click `Finish`.

![Create a new Maven Project - Step 4](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=createNewProject4)

### 2. Add reference of the library project

The created Maven project manages its dependencies using its `pom.xml` file. In order to add a dependency on the *Greenbyte* client library, double click on the `pom.xml` file in the `Package Explorer`. Opening the `pom.xml` file will render a graphical view on the canvas. Here, switch to the `Dependencies` tab and click the `Add` button as shown in the picture below.

![Adding dependency to the client library - Step 1](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=testProject0)

Clicking the `Add` button will open a dialog where you need to specify Greenbyte in `Group Id`, greenbyte in `Artifact Id` and 2.2.0-beta in the `Version` fields. Once added click `OK`. Save the `pom.xml` file.

![Adding dependency to the client library - Step 2](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=testProject1)

![Adding sample code](https://apidocs.io/illustration/java?workspaceFolder=Greenbyte-Java&workspaceName=Greenbyte&projectName=Greenbyte&rootNamespace=cloud.greenbyte.intro&groupId=Greenbyte&artifactId=greenbyte&version=2.2.0-beta&step=testProject2)

### 3. Write sample code

Once the `SimpleConsoleApp` is created, a file named `App.java` will be visible in the *Package Explorer* with a `main` method. This is the entry point for the execution of the created project.
Here, you can add code to initialize the client library and instantiate a *Controller* class. Sample code to initialize the client library and using controller methods is given in the subsequent sections.

## Initialize the API Client

**_Note:_** Documentation for the client can be found [here.](doc/client.md)

The following parameters are configurable for the API Client:

| Parameter | Type | Description |
|  --- | --- | --- |
| customer | `String` | The customer sub-domain<br>*Default*: `"intro"` |
| environment | [`Environment`](README.md#environments) | The API environment. <br> **Default: `Environment.PRODUCTION`** |
| httpClientConfig | [`Consumer<HttpClientConfiguration.Builder>`](doc/http-client-configuration-builder.md) | Set up Http Client Configuration instance. |
| loggingConfig | [`Consumer<ApiLoggingConfiguration.Builder>`](doc/api-logging-configuration-builder.md) | Set up Logging Configuration instance. |
| customHeaderAuthenticationCredentials | [`CustomHeaderAuthenticationCredentials`](doc/auth/custom-header-signature.md) | The Credentials Setter for Custom Header Signature |

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

## Environments

The SDK can be configured to use a different environment for making API calls. Available environments are:

### Fields

| Name | Description |
|  --- | --- |
| PRODUCTION | **Default** The Greenbyte API for a specific customer |

## Authorization

This API uses the following authentication schemes.

* [`ApiKeyHeaderAuth (Custom Header Signature)`](doc/auth/custom-header-signature.md)

## List of APIs

* [Configurationdata](doc/controllers/configurationdata.md)
* [Data](doc/controllers/data.md)
* [Statuses](doc/controllers/statuses.md)
* [Assets](doc/controllers/assets.md)
* [Alerts](doc/controllers/alerts.md)
* [Plan](doc/controllers/plan.md)
* [Predict](doc/controllers/predict.md)

## SDK Infrastructure

### Configuration

* [ApiLoggingConfiguration](doc/api-logging-configuration.md)
* [ApiLoggingConfiguration.Builder](doc/api-logging-configuration-builder.md)
* [ApiRequestLoggingConfiguration.Builder](doc/api-request-logging-configuration-builder.md)
* [ApiResponseLoggingConfiguration.Builder](doc/api-response-logging-configuration-builder.md)
* [Configuration Interface](doc/configuration-interface.md)
* [HttpClientConfiguration](doc/http-client-configuration.md)
* [HttpClientConfiguration.Builder](doc/http-client-configuration-builder.md)
* [HttpProxyConfiguration](doc/http-proxy-configuration.md)
* [HttpProxyConfiguration.Builder](doc/http-proxy-configuration-builder.md)

### HTTP

* [Headers](doc/headers.md)
* [HttpCallback Interface](doc/http-callback-interface.md)
* [HttpContext](doc/http-context.md)
* [HttpBodyRequest](doc/http-body-request.md)
* [HttpRequest](doc/http-request.md)
* [HttpResponse](doc/http-response.md)
* [HttpStringResponse](doc/http-string-response.md)

### Utilities

* [ApiException](doc/api-exception.md)
* [ApiResponse](doc/api-response.md)
* [ApiHelper](doc/api-helper.md)
* [FileWrapper](doc/file-wrapper.md)
* [DateTimeHelper](doc/date-time-helper.md)

