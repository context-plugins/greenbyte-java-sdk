# Plan

This section contains operations related to the configuration of future events.
This includes tasks, site accesses (and their connected device accesses), downtimes, personnel and organizations.

```java
PlanApi planApi = client.getPlanApi();
```

## Class Name

`PlanApi`

## Methods

* [List Tasks](../../doc/controllers/plan.md#list-tasks)
* [Get Task](../../doc/controllers/plan.md#get-task)
* [List Task Categories](../../doc/controllers/plan.md#list-task-categories)
* [List Comments for Multiple Tasks](../../doc/controllers/plan.md#list-comments-for-multiple-tasks)
* [List Task Files](../../doc/controllers/plan.md#list-task-files)
* [Download Task File](../../doc/controllers/plan.md#download-task-file)
* [List Site Accesses](../../doc/controllers/plan.md#list-site-accesses)
* [Get Site Access](../../doc/controllers/plan.md#get-site-access)
* [List Device Accesses for Multiple Site Accesses](../../doc/controllers/plan.md#list-device-accesses-for-multiple-site-accesses)
* [Get Device Access](../../doc/controllers/plan.md#get-device-access)
* [List Downtime Events](../../doc/controllers/plan.md#list-downtime-events)
* [Get Downtime Event](../../doc/controllers/plan.md#get-downtime-event)
* [List Personnel](../../doc/controllers/plan.md#list-personnel)
* [Get Personnel](../../doc/controllers/plan.md#get-personnel)
* [List Organizations](../../doc/controllers/plan.md#list-organizations)
* [List Hse Incidents](../../doc/controllers/plan.md#list-hse-incidents)
* [Get Hse Incident](../../doc/controllers/plan.md#get-hse-incident)
* [List Worklog Items](../../doc/controllers/plan.md#list-worklog-items)
* [Get Worklog Item](../../doc/controllers/plan.md#get-worklog-item)


# List Tasks

Gets a list of tasks.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<List<Task>>> listTasksAsync(
    final LocalDateTime timestampStart,
    final LocalDateTime timestampEnd,
    final List<Integer> deviceIds,
    final List<Integer> siteIds,
    final List<Integer> categoryIds,
    final TaskState state,
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
| `timestampStart` | `LocalDateTime` | Query, Required | The beginning of the time interval to get data for (inclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The start timestamp **is** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `timestampEnd` | `LocalDateTime` | Query, Required | The end of the time interval to get data for (exclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The end timestamp is **not** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `deviceIds` | `List<Integer>` | Query, Optional | What devices to get tasks for.<br><br>**Constraints**: `>= 1` |
| `siteIds` | `List<Integer>` | Query, Optional | What sites to get tasks for.<br><br>**Constraints**: `>= 1` |
| `categoryIds` | `List<Integer>` | Query, Optional | What task categories to include.<br><br>**Constraints**: `>= 1` |
| `state` | [`TaskState`](../../doc/models/task-state.md) | Query, Optional | What state of tasks to get: resolved and unresolved. If not set, both resolved and unresolved tasks are included. |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `Task` schema (See Response Type). By default all fields are included. |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A list of tasks matching the filter parameters.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<Task>`](../../doc/models/task.md).

## Example Usage

```java
LocalDateTime timestampStart = DateTimeHelper.fromRfc8601DateTime("01/01/2024 00:00:00");
LocalDateTime timestampEnd = DateTimeHelper.fromRfc8601DateTime("01/08/2024 00:00:00");
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

List<Integer> siteIds = Arrays.asList(
    1,
    2,
    3
);

List<Integer> categoryIds = Arrays.asList(
    1,
    2,
    3
);

List<String> fields = Arrays.asList(
    "taskId",
    "title"
);

Integer pageSize = 50;
Integer page = 1;
Boolean useUtc = false;

planApi.listTasksAsync(timestampStart, timestampEnd, deviceIds, siteIds, categoryIds, null, fields, pageSize, page, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Tasks400ErrorException) {
        Tasks400ErrorException tasks400ErrorException = (Tasks400ErrorException) cause;
        tasks400ErrorException.printStackTrace();
    } else if (cause instanceof Tasks429ErrorException) {
        Tasks429ErrorException tasks429ErrorException = (Tasks429ErrorException) cause;
        tasks429ErrorException.printStackTrace();
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
    "taskId": 10,
    "title": "Maintenance",
    "createdBy": {
      "firstName": "Greenbyte",
      "lastName": "Support"
    },
    "description": "maintenance on site",
    "category": {
      "categoryId": 5,
      "title": "Site visit without downtime"
    },
    "priority": "medium",
    "timestampStart": "2020-01-01T00:00:00",
    "timestampEnd": "2020-01-08T00:00:00",
    "state": "resolved",
    "resolved": true,
    "timestampResolved": "2020-01-08T00:00:00",
    "deviceIds": [
      21,
      22
    ],
    "siteIds": [],
    "siteAccessIds": [
      4177
    ],
    "downtimeEventIds": [],
    "statusIds": [],
    "numberOfComments": 3,
    "recurrence": null,
    "mainTaskId": null,
    "assignee": null,
    "metadata": [
      {
        "key": "Component",
        "value": "Yaw encoder"
      }
    ]
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Tasks400ErrorException`](../../doc/models/tasks-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Tasks429ErrorException`](../../doc/models/tasks-429-error-exception.md) |


# Get Task

Get a single task by ID.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<TasksResponse>> getTaskAsync(
    final int taskId,
    final Boolean useUtc)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `taskId` | `int` | Template, Required | The id of the task to get.<br><br>**Constraints**: `>= 1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A single task.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`TasksResponse`](../../doc/models/tasks-response.md).

## Example Usage

```java
int taskId = 92;
Boolean useUtc = false;

planApi.getTaskAsync(taskId, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Tasks400ErrorException) {
        Tasks400ErrorException tasks400ErrorException = (Tasks400ErrorException) cause;
        tasks400ErrorException.printStackTrace();
    } else if (cause instanceof Tasks429ErrorException) {
        Tasks429ErrorException tasks429ErrorException = (Tasks429ErrorException) cause;
        tasks429ErrorException.printStackTrace();
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
  "taskId": 10,
  "title": "Maintenance",
  "createdBy": {
    "firstName": "Greenbyte",
    "lastName": "Support"
  },
  "description": "Notes go here",
  "category": {
    "categoryId": 32,
    "title": "Scheduled Maintenance"
  },
  "priority": "medium",
  "timestampStart": "2020-01-01T00:00:00.000Z",
  "timestampEnd": "2020-01-08T00:00:00.000Z",
  "state": "unresolved",
  "resolved": true,
  "timestampResolved": null,
  "deviceIds": [],
  "siteIds": [
    1
  ],
  "siteAccessIds": [],
  "downtimeEventIds": [],
  "statusIds": [],
  "numberOfComments": 3,
  "recurrence": {
    "duration": 1,
    "durationType": "year",
    "dateEnd": "2020-11-30"
  },
  "mainTaskId": 1544,
  "assignee": null,
  "metadata": []
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Tasks400ErrorException`](../../doc/models/tasks-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 404 | The requested resource could not be found. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Tasks429ErrorException`](../../doc/models/tasks-429-error-exception.md) |


# List Task Categories

Gets a list of task categories.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<List<TaskCategory>>> listTaskCategoriesAsync()
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Response Type

**200**: A list of task categories.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<TaskCategory>`](../../doc/models/task-category.md).

## Example Usage

```java
planApi.listTaskCategoriesAsync().thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof TaskCategories400ErrorException) {
        TaskCategories400ErrorException taskCategories400ErrorException = (TaskCategories400ErrorException) cause;
        taskCategories400ErrorException.printStackTrace();
    } else if (cause instanceof TaskCategories429ErrorException) {
        TaskCategories429ErrorException taskCategories429ErrorException = (TaskCategories429ErrorException) cause;
        taskCategories429ErrorException.printStackTrace();
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
    "categoryId": 10,
    "title": "Scheduled maintenance"
  },
  {
    "categoryId": 20,
    "title": "Unscheduled maintenance"
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`TaskCategories400ErrorException`](../../doc/models/task-categories-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`TaskCategories429ErrorException`](../../doc/models/task-categories-429-error-exception.md) |


# List Comments for Multiple Tasks

Gets a list of comments belonging to one or more tasks with given taskIds.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<List<TaskComment>>> listCommentsForMultipleTasksAsync(
    final List<Integer> taskIds,
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
| `taskIds` | `List<Integer>` | Query, Required | An array of taskIds.<br><br>**Constraints**: `>= 1` |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `TaskComment` schema (See Response Type). By default all fields are included. |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A list of comments belonging to the task.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<TaskComment>`](../../doc/models/task-comment.md).

## Example Usage

```java
List<Integer> taskIds = Arrays.asList(
    1,
    2,
    3
);

List<String> fields = Arrays.asList(
    "commentId",
    "text"
);

Integer pageSize = 50;
Integer page = 1;
Boolean useUtc = false;

planApi.listCommentsForMultipleTasksAsync(taskIds, fields, pageSize, page, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof TasksComments400ErrorException) {
        TasksComments400ErrorException tasksComments400ErrorException = (TasksComments400ErrorException) cause;
        tasksComments400ErrorException.printStackTrace();
    } else if (cause instanceof TasksComments429ErrorException) {
        TasksComments429ErrorException tasksComments429ErrorException = (TasksComments429ErrorException) cause;
        tasksComments429ErrorException.printStackTrace();
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
    "commentId": 10,
    "taskId": 1,
    "text": "Task started",
    "timestampCreated": "2020-01-01T00:00:00",
    "createdBy": {
      "firstName": "Greenbyte",
      "lastName": "Support"
    }
  },
  {
    "commentId": 11,
    "taskId": 2,
    "text": "Task finished",
    "timestampCreated": "2020-01-02T00:00:00",
    "createdBy": {
      "firstName": "Greenbyte",
      "lastName": "Support"
    }
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`TasksComments400ErrorException`](../../doc/models/tasks-comments-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`TasksComments429ErrorException`](../../doc/models/tasks-comments-429-error-exception.md) |


# List Task Files

Gets a list of files belonging to a task.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<List<TasksFilesResponse>>> listTaskFilesAsync(
    final int taskId,
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
| `taskId` | `int` | Template, Required | The id of the task.<br><br>**Constraints**: `>= 1` |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `TaskFile` schema (See Response Type). By default all fields are included. |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A list with information about files belonging to the task.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<TasksFilesResponse>`](../../doc/models/tasks-files-response.md).

## Example Usage

```java
int taskId = 92;
List<String> fields = Arrays.asList(
    "fileName",
    "description"
);

Integer pageSize = 50;
Integer page = 1;
Boolean useUtc = false;

planApi.listTaskFilesAsync(taskId, fields, pageSize, page, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof TasksFiles400ErrorException) {
        TasksFiles400ErrorException tasksFiles400ErrorException = (TasksFiles400ErrorException) cause;
        tasksFiles400ErrorException.printStackTrace();
    } else if (cause instanceof TasksFiles429ErrorException) {
        TasksFiles429ErrorException tasksFiles429ErrorException = (TasksFiles429ErrorException) cause;
        tasksFiles429ErrorException.printStackTrace();
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
    "fileId": 501,
    "fileName": "Upgrade.docx",
    "timestampUploaded": "2020-05-29T16:12:34",
    "uploadedBy": {
      "firstName": "Greenbyte",
      "lastName": "Support"
    },
    "description": "Aerodynamic upgrade report",
    "category": "Reports"
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`TasksFiles400ErrorException`](../../doc/models/tasks-files-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 404 | The requested resource could not be found. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`TasksFiles429ErrorException`](../../doc/models/tasks-files-429-error-exception.md) |


# Download Task File

Downloads a file belonging to a task.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<InputStream>> downloadTaskFileAsync(
    final int taskId,
    final int fileId)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `taskId` | `int` | Template, Required | The id of the task.<br><br>**Constraints**: `>= 1` |
| `fileId` | `int` | Template, Required | The id of the file.<br><br>**Constraints**: `>= 1` |

## Response Type

**200**: The contents of a file linked to the task.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type `InputStream`.

## Example Usage

```java
int taskId = 92;
int fileId = 12;

planApi.downloadTaskFileAsync(taskId, fileId).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof TasksFilesContent400ErrorException) {
        TasksFilesContent400ErrorException tasksFilesContent400ErrorException = (TasksFilesContent400ErrorException) cause;
        tasksFilesContent400ErrorException.printStackTrace();
    } else if (cause instanceof TasksFilesContent429ErrorException) {
        TasksFilesContent429ErrorException tasksFilesContent429ErrorException = (TasksFilesContent429ErrorException) cause;
        tasksFilesContent429ErrorException.printStackTrace();
    } else {
        // fallback for unexpected errors
        exception.printStackTrace();
    }

    return null;
});
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`TasksFilesContent400ErrorException`](../../doc/models/tasks-files-content-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 404 | The requested resource could not be found. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`TasksFilesContent429ErrorException`](../../doc/models/tasks-files-content-429-error-exception.md) |


# List Site Accesses

Gets a list of site accesses.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<List<SiteAccess>>> listSiteAccessesAsync(
    final LocalDateTime timestampStart,
    final LocalDateTime timestampEnd,
    final List<Integer> deviceIds,
    final List<Integer> siteIds,
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
| `timestampStart` | `LocalDateTime` | Query, Required | The beginning of the time interval to get data for (inclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The start timestamp **is** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `timestampEnd` | `LocalDateTime` | Query, Required | The end of the time interval to get data for (exclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The end timestamp is **not** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `deviceIds` | `List<Integer>` | Query, Optional | What devices to get site accesses for.<br><br>**Constraints**: `>= 1` |
| `siteIds` | `List<Integer>` | Query, Optional | What sites to get site accesses for.<br><br>**Constraints**: `>= 1` |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `SiteAccess` schema (See Response Type). By default all fields are included. |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A list of site accesses matching the filter parameters.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<SiteAccess>`](../../doc/models/site-access.md).

## Example Usage

```java
LocalDateTime timestampStart = DateTimeHelper.fromRfc8601DateTime("01/01/2024 00:00:00");
LocalDateTime timestampEnd = DateTimeHelper.fromRfc8601DateTime("01/08/2024 00:00:00");
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

List<Integer> siteIds = Arrays.asList(
    1,
    2,
    3
);

List<String> fields = Arrays.asList(
    "siteAccessId",
    "timestampStart"
);

Integer pageSize = 50;
Integer page = 1;
Boolean useUtc = false;

planApi.listSiteAccessesAsync(timestampStart, timestampEnd, deviceIds, siteIds, fields, pageSize, page, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof SiteAccesses400ErrorException) {
        SiteAccesses400ErrorException siteAccesses400ErrorException = (SiteAccesses400ErrorException) cause;
        siteAccesses400ErrorException.printStackTrace();
    } else if (cause instanceof SiteAccesses429ErrorException) {
        SiteAccesses429ErrorException siteAccesses429ErrorException = (SiteAccesses429ErrorException) cause;
        siteAccesses429ErrorException.printStackTrace();
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
    "siteAccessId": 10,
    "siteId": 18,
    "deviceIds": [
      11,
      12
    ],
    "taskIds": [
      66
    ],
    "siteAccessPersonnel": [
      {
        "personnelId": 1234,
        "firstName": "Andreas",
        "lastName": "Jonsson",
        "company": "Power Offtakers Inc.",
        "phoneNumber": "456-123",
        "vehicleRegistration": "ABC456",
        "comment": "Site access comment",
        "timestampStart": "2020-04-30T10:03:00",
        "timestampEnd": "2020-04-30T17:39:00"
      }
    ],
    "timestampStart": "2020-01-01T12:00:00",
    "timestampEndExpected": "2020-01-01T13:00:00",
    "timestampEnd": "2020-01-01T13:30:00",
    "logOnComment": "Investigating",
    "logOffComment": "All clear"
  },
  {
    "siteAccessId": 11,
    "siteId": 18,
    "deviceIds": [
      15
    ],
    "taskIds": [
      55,
      56
    ],
    "siteAccessPersonnel": [
      {
        "personnelId": 2345,
        "firstName": "Andrea",
        "lastName": "Larsson",
        "company": "Power Offtakers Inc.",
        "phoneNumber": "123-456",
        "vehicleRegistration": "ABC123",
        "comment": "Site access comment",
        "timestampStart": "2020-04-30T10:04:00",
        "timestampEnd": "2020-04-30T17:39:00"
      }
    ],
    "timestampStart": "2020-01-02T12:00:00",
    "timestampEndExpected": "2020-01-02T13:00:00",
    "timestampEnd": "2020-01-02T13:30:00",
    "logOnComment": "Investigating",
    "logOffComment": "All clear"
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`SiteAccesses400ErrorException`](../../doc/models/site-accesses-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`SiteAccesses429ErrorException`](../../doc/models/site-accesses-429-error-exception.md) |


# Get Site Access

Gets a specific site access.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<SiteAccessesResponse>> getSiteAccessAsync(
    final int siteAccessId,
    final Boolean useUtc)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `siteAccessId` | `int` | Template, Required | The id of the site access.<br><br>**Constraints**: `>= 1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A single site access object.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`SiteAccessesResponse`](../../doc/models/site-accesses-response.md).

## Example Usage

```java
int siteAccessId = 10;
Boolean useUtc = false;

planApi.getSiteAccessAsync(siteAccessId, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof SiteAccesses400ErrorException) {
        SiteAccesses400ErrorException siteAccesses400ErrorException = (SiteAccesses400ErrorException) cause;
        siteAccesses400ErrorException.printStackTrace();
    } else if (cause instanceof SiteAccesses429ErrorException) {
        SiteAccesses429ErrorException siteAccesses429ErrorException = (SiteAccesses429ErrorException) cause;
        siteAccesses429ErrorException.printStackTrace();
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
  "siteAccessId": 10,
  "siteId": 18,
  "deviceIds": [
    11,
    12
  ],
  "taskIds": [
    66
  ],
  "siteAccessPersonnel": [
    {
      "personnelId": 1234,
      "firstName": "Andreas",
      "lastName": "Jonsson",
      "company": "Power Offtakers Inc.",
      "phoneNumber": "456-123",
      "vehicleRegistration": "ABC456",
      "comment": "Site access comment",
      "timestampStart": "2020-04-30T10:03:00",
      "timestampEnd": "2020-04-30T17:39:00"
    }
  ],
  "timestampStart": "2020-01-01T12:00:00",
  "timestampEndExpected": "2020-01-01T13:00:00",
  "timestampEnd": "2020-01-01T13:30:00",
  "logOnComment": "Investigating",
  "logOffComment": "All clear"
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`SiteAccesses400ErrorException`](../../doc/models/site-accesses-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 404 | The requested resource could not be found. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`SiteAccesses429ErrorException`](../../doc/models/site-accesses-429-error-exception.md) |


# List Device Accesses for Multiple Site Accesses

Gets a list of device accesses belonging to site accesses with specified SiteAccessIds.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<List<DeviceAccess>>> listDeviceAccessesForMultipleSiteAccessesAsync(
    final List<Integer> siteAccessIds,
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
| `siteAccessIds` | `List<Integer>` | Query, Required | An array of siteAccessIds.<br><br>**Constraints**: `>= 1` |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `DeviceAccess` schema (See Response Type). By default all fields are included. |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A list of device accesses.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<DeviceAccess>`](../../doc/models/device-access.md).

## Example Usage

```java
List<Integer> siteAccessIds = Arrays.asList(
    1,
    2
);

List<String> fields = Arrays.asList(
    "deviceAccessId",
    "siteId"
);

Integer pageSize = 50;
Integer page = 1;
Boolean useUtc = false;

planApi.listDeviceAccessesForMultipleSiteAccessesAsync(siteAccessIds, fields, pageSize, page, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof DeviceAccesses400ErrorException) {
        DeviceAccesses400ErrorException deviceAccesses400ErrorException = (DeviceAccesses400ErrorException) cause;
        deviceAccesses400ErrorException.printStackTrace();
    } else if (cause instanceof DeviceAccesses429ErrorException) {
        DeviceAccesses429ErrorException deviceAccesses429ErrorException = (DeviceAccesses429ErrorException) cause;
        deviceAccesses429ErrorException.printStackTrace();
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
    "deviceAccessId": 1504,
    "siteId": 50,
    "siteAccessId": 1,
    "deviceIds": [
      15
    ],
    "personnelIds": [
      11,
      12
    ],
    "taskIds": [
      55
    ],
    "timestampStart": "2020-01-02T12:00:00",
    "timestampEnd": "2020-01-02T12:55:00",
    "timestampEndExpected": "2020-01-02T13:00:00",
    "logOnComment": "TOC at 12:01",
    "logOffComment": "Access completed"
  },
  {
    "deviceAccessId": 1560,
    "siteId": 50,
    "siteAccessId": 2,
    "deviceIds": [
      15
    ],
    "personnelIds": [
      11,
      12
    ],
    "taskIds": [
      55
    ],
    "timestampStart": "2020-01-02T13:00:00",
    "timestampEnd": "2020-01-02T13:55:00",
    "timestampEndExpected": "2020-01-02T14:00:00",
    "logOnComment": "TOC at 13:01",
    "logOffComment": "Access completed"
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`DeviceAccesses400ErrorException`](../../doc/models/device-accesses-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`DeviceAccesses429ErrorException`](../../doc/models/device-accesses-429-error-exception.md) |


# Get Device Access

Get a single device access by ID.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<DeviceAccessesResponse>> getDeviceAccessAsync(
    final int deviceAccessId,
    final Boolean useUtc)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `deviceAccessId` | `int` | Template, Required | The id of the device access to get.<br><br>**Constraints**: `>= 1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A single device access.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`DeviceAccessesResponse`](../../doc/models/device-accesses-response.md).

## Example Usage

```java
int deviceAccessId = 38;
Boolean useUtc = false;

planApi.getDeviceAccessAsync(deviceAccessId, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof DeviceAccesses400ErrorException) {
        DeviceAccesses400ErrorException deviceAccesses400ErrorException = (DeviceAccesses400ErrorException) cause;
        deviceAccesses400ErrorException.printStackTrace();
    } else if (cause instanceof DeviceAccesses429ErrorException) {
        DeviceAccesses429ErrorException deviceAccesses429ErrorException = (DeviceAccesses429ErrorException) cause;
        deviceAccesses429ErrorException.printStackTrace();
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
  "deviceAccessId": 1542,
  "siteId": 50,
  "deviceIds": [
    15
  ],
  "personnelIds": [
    11,
    12
  ],
  "taskIds": [
    55
  ],
  "timestampStart": "2020-01-02T12:00:00",
  "timestampEnd": "2020-01-02T12:55:00",
  "timestampEndExpected": "2020-01-02T13:00:00",
  "logOnComment": "TOC at 12:01",
  "logOffComment": "Access completed"
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`DeviceAccesses400ErrorException`](../../doc/models/device-accesses-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 404 | The requested resource could not be found. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`DeviceAccesses429ErrorException`](../../doc/models/device-accesses-429-error-exception.md) |


# List Downtime Events

Gets a list of downtime events.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<List<DowntimeEvent>>> listDowntimeEventsAsync(
    final LocalDateTime timestampStart,
    final LocalDateTime timestampEnd,
    final List<Integer> deviceIds,
    final List<Integer> siteIds,
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
| `timestampStart` | `LocalDateTime` | Query, Required | The beginning of the time interval to get data for (inclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The start timestamp **is** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `timestampEnd` | `LocalDateTime` | Query, Required | The end of the time interval to get data for (exclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The end timestamp is **not** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `deviceIds` | `List<Integer>` | Query, Optional | What devices to get downtime events for.<br><br>**Constraints**: `>= 1` |
| `siteIds` | `List<Integer>` | Query, Optional | What sites to get downtime events for.<br><br>**Constraints**: `>= 1` |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `DowntimeEvent` schema (See Response Type). By default all fields are included. |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A list of downtime events matching the filter parameters.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<DowntimeEvent>`](../../doc/models/downtime-event.md).

## Example Usage

```java
LocalDateTime timestampStart = DateTimeHelper.fromRfc8601DateTime("01/01/2024 00:00:00");
LocalDateTime timestampEnd = DateTimeHelper.fromRfc8601DateTime("01/08/2024 00:00:00");
List<Integer> deviceIds = Arrays.asList(
    1,
    2,
    3
);

List<Integer> siteIds = Arrays.asList(
    1,
    2,
    3
);

List<String> fields = Arrays.asList(
    "deviceIds",
    "timestampStart"
);

Integer pageSize = 50;
Integer page = 1;
Boolean useUtc = false;

planApi.listDowntimeEventsAsync(timestampStart, timestampEnd, deviceIds, siteIds, fields, pageSize, page, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof DowntimeEvents400ErrorException) {
        DowntimeEvents400ErrorException downtimeEvents400ErrorException = (DowntimeEvents400ErrorException) cause;
        downtimeEvents400ErrorException.printStackTrace();
    } else if (cause instanceof DowntimeEvents429ErrorException) {
        DowntimeEvents429ErrorException downtimeEvents429ErrorException = (DowntimeEvents429ErrorException) cause;
        downtimeEvents429ErrorException.printStackTrace();
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
    "downtimeEventId": 1,
    "deviceIds": [
      1,
      2,
      3
    ],
    "timestampStart": "2020-01-01T00:00:00",
    "timestampEnd": "2020-01-02T00:00:00",
    "comment": "Planned downtime",
    "siteIds": [],
    "taskIds": [
      1358
    ],
    "remainingCapacityPercentage": 10
  },
  {
    "downtimeEventId": 2,
    "deviceIds": [
      1,
      2,
      3
    ],
    "timestampStart": "2020-01-10T00:00:00",
    "timestampEnd": "2020-01-12T00:00:00",
    "comment": "Unplanned downtime",
    "siteIds": [
      1
    ],
    "taskIds": [
      1359
    ],
    "remainingCapacityPercentage": 0
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`DowntimeEvents400ErrorException`](../../doc/models/downtime-events-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`DowntimeEvents429ErrorException`](../../doc/models/downtime-events-429-error-exception.md) |


# Get Downtime Event

Gets a single downtime event by ID.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<DowntimeEventsResponse>> getDowntimeEventAsync(
    final int downtimeEventId,
    final Boolean useUtc)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `downtimeEventId` | `int` | Template, Required | The id of the downtime event to get.<br><br>**Constraints**: `>= 1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A single downtime event.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`DowntimeEventsResponse`](../../doc/models/downtime-events-response.md).

## Example Usage

```java
int downtimeEventId = 168;
Boolean useUtc = false;

planApi.getDowntimeEventAsync(downtimeEventId, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof DowntimeEvents400ErrorException) {
        DowntimeEvents400ErrorException downtimeEvents400ErrorException = (DowntimeEvents400ErrorException) cause;
        downtimeEvents400ErrorException.printStackTrace();
    } else if (cause instanceof DowntimeEvents429ErrorException) {
        DowntimeEvents429ErrorException downtimeEvents429ErrorException = (DowntimeEvents429ErrorException) cause;
        downtimeEvents429ErrorException.printStackTrace();
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
  "downtimeEventId": 2,
  "deviceIds": [
    1,
    2,
    3
  ],
  "timestampStart": "2020-01-10T00:00:00",
  "timestampEnd": "2020-01-12T00:00:00",
  "comment": "Unplanned downtime",
  "siteIds": [
    1
  ],
  "taskIds": [
    1359
  ],
  "remainingCapacityPercentage": 5.5
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`DowntimeEvents400ErrorException`](../../doc/models/downtime-events-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 404 | The requested resource could not be found. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`DowntimeEvents429ErrorException`](../../doc/models/downtime-events-429-error-exception.md) |


# List Personnel

Gets a list of personnel.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<List<Personnel>>> listPersonnelAsync(
    final List<String> fields,
    final Integer pageSize,
    final Integer page)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `fields` | `List<String>` | Query, Optional | Which fields to include in the response. Valid fields are those defined in the `Personnel` schema (See Response Type). By default all fields are included. |
| `pageSize` | `Integer` | Query, Optional | The number of items to return per page.<br><br>**Default**: `50` |
| `page` | `Integer` | Query, Optional | Which page to return when the number of items exceed the page size.<br><br>**Default**: `1` |

## Response Type

**200**: A list of personnel matching the filter parameters.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<Personnel>`](../../doc/models/personnel.md).

## Example Usage

```java
List<String> fields = Arrays.asList(
    "lastName",
    "phone"
);

Integer pageSize = 50;
Integer page = 1;

planApi.listPersonnelAsync(fields, pageSize, page).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Personnel400ErrorException) {
        Personnel400ErrorException personnel400ErrorException = (Personnel400ErrorException) cause;
        personnel400ErrorException.printStackTrace();
    } else if (cause instanceof Personnel429ErrorException) {
        Personnel429ErrorException personnel429ErrorException = (Personnel429ErrorException) cause;
        personnel429ErrorException.printStackTrace();
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
    "personnelId": 5,
    "firstName": "Greenbyte",
    "lastName": "Support",
    "email": "support@greenbyte.com",
    "phone": "123-456",
    "mobile": "654-321",
    "organization": {
      "organizationId": 10,
      "name": "Power Offtakers Inc.",
      "email": "support@power-offtakers.example.com",
      "phone": "456-789"
    },
    "qualifications": [
      {
        "qualificationId": 85,
        "manufacturer": "GE",
        "qualificationType": "AP",
        "qualificationDescription": "Authorized Person"
      }
    ],
    "siteInductions": [
      {
        "siteInductionId": 43,
        "siteId": 1,
        "dateExpires": "2020-12-01"
      }
    ]
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Personnel400ErrorException`](../../doc/models/personnel-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Personnel429ErrorException`](../../doc/models/personnel-429-error-exception.md) |


# Get Personnel

Gets a single personnel by ID.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<PersonnelResponse>> getPersonnelAsync(
    final int personnelId)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `personnelId` | `int` | Template, Required | The id of the personnel to get.<br><br>**Constraints**: `>= 1` |

## Response Type

**200**: A single personnel matching the personnel ID.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`PersonnelResponse`](../../doc/models/personnel-response.md).

## Example Usage

```java
int personnelId = 128;

planApi.getPersonnelAsync(personnelId).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Personnel400ErrorException) {
        Personnel400ErrorException personnel400ErrorException = (Personnel400ErrorException) cause;
        personnel400ErrorException.printStackTrace();
    } else if (cause instanceof Personnel429ErrorException) {
        Personnel429ErrorException personnel429ErrorException = (Personnel429ErrorException) cause;
        personnel429ErrorException.printStackTrace();
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
  "personnelId": 5,
  "firstName": "Greenbyte",
  "lastName": "Support",
  "email": "support@greenbyte.com",
  "phone": "123-456",
  "mobile": "654-321",
  "organization": {
    "organizationId": 10,
    "name": "Power Offtakers Inc.",
    "email": "support@power-offtakers.example.com",
    "phone": "456-789"
  },
  "qualifications": [
    {
      "qualificationId": 85,
      "manufacturer": "GE",
      "qualificationType": "AP",
      "qualificationDescription": "Authorized Person"
    }
  ],
  "siteInductions": [
    {
      "siteInductionId": 43,
      "siteId": 1,
      "dateExpires": "2020-12-01"
    }
  ]
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Personnel400ErrorException`](../../doc/models/personnel-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 404 | The requested resource could not be found. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Personnel429ErrorException`](../../doc/models/personnel-429-error-exception.md) |


# List Organizations

Gets a list of organizations.

_🔐 This endpoint requires the **Plan** endpoint permission._

```java
CompletableFuture<ApiResponse<List<Organization>>> listOrganizationsAsync()
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Response Type

**200**: A list of organizations.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<Organization>`](../../doc/models/organization.md).

## Example Usage

```java
planApi.listOrganizationsAsync().thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Organizations400ErrorException) {
        Organizations400ErrorException organizations400ErrorException = (Organizations400ErrorException) cause;
        organizations400ErrorException.printStackTrace();
    } else if (cause instanceof Organizations429ErrorException) {
        Organizations429ErrorException organizations429ErrorException = (Organizations429ErrorException) cause;
        organizations429ErrorException.printStackTrace();
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
    "organizationId": 10,
    "name": "Power Offtakers Inc.",
    "email": "support@power-offtakers.example.com",
    "phone": "456-789"
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Organizations400ErrorException`](../../doc/models/organizations-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Organizations429ErrorException`](../../doc/models/organizations-429-error-exception.md) |


# List Hse Incidents

Gets a list of HSE incidents.

_🔐 This endpoint requires the **Plan** endpoint permission._

_This is a beta feature. Some details might change before it is released as a stable version._

```java
CompletableFuture<ApiResponse<List<HseIncidentsResponse>>> listHseIncidentsAsync(
    final LocalDateTime timestampStart,
    final LocalDateTime timestampEnd,
    final List<Integer> siteIds,
    final State state,
    final HseCategory category,
    final Boolean useUtc)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `timestampStart` | `LocalDateTime` | Query, Required | The beginning of the time interval to get data for (inclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The start timestamp **is** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `timestampEnd` | `LocalDateTime` | Query, Required | The end of the time interval to get data for (exclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The end timestamp is **not** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `siteIds` | `List<Integer>` | Query, Optional | Which sites to get HSE incidents for.<br><br>**Constraints**: `>= 1` |
| `state` | [`State`](../../doc/models/state.md) | Query, Optional | Retrieve HSE incidents with state: resolved or unresolved.<br>If not set, both resolved and unresolved HSE incidents are included. |
| `category` | [`HseCategory`](../../doc/models/hse-category.md) | Query, Optional | Retrieve HSE incidents with a specific category.<br>If not set, HSE incidents of all categories are included. |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A list of HSE incidents matching the filter parameters.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<HseIncidentsResponse>`](../../doc/models/hse-incidents-response.md).

## Example Usage

```java
LocalDateTime timestampStart = DateTimeHelper.fromRfc8601DateTime("01/01/2024 00:00:00");
LocalDateTime timestampEnd = DateTimeHelper.fromRfc8601DateTime("01/08/2024 00:00:00");
List<Integer> siteIds = Arrays.asList(
    1,
    2,
    3
);

Boolean useUtc = false;

planApi.listHseIncidentsAsync(timestampStart, timestampEnd, siteIds, null, null, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof HseIncidents400ErrorException) {
        HseIncidents400ErrorException hseIncidents400ErrorException = (HseIncidents400ErrorException) cause;
        hseIncidents400ErrorException.printStackTrace();
    } else if (cause instanceof HseIncidents429ErrorException) {
        HseIncidents429ErrorException hseIncidents429ErrorException = (HseIncidents429ErrorException) cause;
        hseIncidents429ErrorException.printStackTrace();
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
    "hseIncidentId": 10,
    "siteId": 5,
    "deviceId": 1,
    "timestamp": "2022-12-18T09:45:00",
    "hseCategory": "HazardObservation",
    "lostTimeInjury": false,
    "incidentDescription": "Broken ladder",
    "resolved": false,
    "resolvedTimestamp": null
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`HseIncidents400ErrorException`](../../doc/models/hse-incidents-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`HseIncidents429ErrorException`](../../doc/models/hse-incidents-429-error-exception.md) |


# Get Hse Incident

Get a single HSE incident by ID.

_🔐 This endpoint requires the **Plan** endpoint permission._

_This is a beta feature. Some details might change before it is released as a stable version._

```java
CompletableFuture<ApiResponse<HseIncidentsResponse1>> getHseIncidentAsync(
    final int hseIncidentId,
    final Boolean useUtc)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `hseIncidentId` | `int` | Template, Required | The id of the HSE incident to get.<br><br>**Constraints**: `>= 1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A single HSE incident.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`HseIncidentsResponse1`](../../doc/models/hse-incidents-response-1.md).

## Example Usage

```java
int hseIncidentId = 1;
Boolean useUtc = false;

planApi.getHseIncidentAsync(hseIncidentId, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof HseIncidents400ErrorException) {
        HseIncidents400ErrorException hseIncidents400ErrorException = (HseIncidents400ErrorException) cause;
        hseIncidents400ErrorException.printStackTrace();
    } else if (cause instanceof HseIncidents429ErrorException) {
        HseIncidents429ErrorException hseIncidents429ErrorException = (HseIncidents429ErrorException) cause;
        hseIncidents429ErrorException.printStackTrace();
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
  "hseIncidentId": 10,
  "siteId": 5,
  "deviceId": 1,
  "timestamp": "2022-12-18T09:45:00",
  "hseCategory": "HazardObservation",
  "lostTimeInjury": false,
  "incidentDescription": "Broken ladder",
  "resolved": false,
  "resolvedTimestamp": null
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`HseIncidents400ErrorException`](../../doc/models/hse-incidents-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 404 | The requested resource could not be found. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`HseIncidents429ErrorException`](../../doc/models/hse-incidents-429-error-exception.md) |


# List Worklog Items

Gets a list of worklog items.

_🔐 This endpoint requires the **Plan** endpoint permission._

_This is a beta feature. Some details might change before it is released as a stable version._

```java
CompletableFuture<ApiResponse<List<WorklogResponse>>> listWorklogItemsAsync(
    final LocalDateTime timestampStart,
    final LocalDateTime timestampEnd,
    final List<Integer> siteIds,
    final Boolean useUtc)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `timestampStart` | `LocalDateTime` | Query, Required | The beginning of the time interval to get data for (inclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The start timestamp **is** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `timestampEnd` | `LocalDateTime` | Query, Required | The end of the time interval to get data for (exclusive),<br>in [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)<br>**date-time** format:<br><br>* Timestamps ending with 'Z' are treated as UTC. Example: "2020-01-01T00:00:00Z"<br>* Time zone (UTC) offset timestamps ending with '+HH:mm'/"-HH:mm" are also supported. Example: "2020-01-01T02:00:00-02:00"<br>* Other timestamps are treated as being in the time zone configured in the Greenbyte Platform. Example: "2020-01-01T00:00:00"<br><br>The end timestamp is **not** included in the time interval: for<br>example, to select the full month of March 2020, set<br>`timestampStart` to "2020-03-01T00:00:00" and `timestampEnd` to<br>"2020-04-01T00:00:00".<br><br>Timestamps selected in the portal will by default be in UTC. |
| `siteIds` | `List<Integer>` | Query, Optional | What sites to get worklog items for.<br><br>**Constraints**: `>= 1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A list of worklog items matching the filter parameters.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`List<WorklogResponse>`](../../doc/models/worklog-response.md).

## Example Usage

```java
LocalDateTime timestampStart = DateTimeHelper.fromRfc8601DateTime("01/01/2024 00:00:00");
LocalDateTime timestampEnd = DateTimeHelper.fromRfc8601DateTime("01/08/2024 00:00:00");
List<Integer> siteIds = Arrays.asList(
    1,
    2,
    3
);

Boolean useUtc = false;

planApi.listWorklogItemsAsync(timestampStart, timestampEnd, siteIds, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Worklog400ErrorException) {
        Worklog400ErrorException worklog400ErrorException = (Worklog400ErrorException) cause;
        worklog400ErrorException.printStackTrace();
    } else if (cause instanceof Worklog429ErrorException) {
        Worklog429ErrorException worklog429ErrorException = (Worklog429ErrorException) cause;
        worklog429ErrorException.printStackTrace();
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
    "worklogItemId": 10,
    "timestamp": "2023-01-08T00:00:00",
    "siteId": 5,
    "hoursWorked": 2.5,
    "comment": "Inverter B Offline With Repeated Fault\n- Work Performed: INV B was cleaned\n"
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Worklog400ErrorException`](../../doc/models/worklog-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Worklog429ErrorException`](../../doc/models/worklog-429-error-exception.md) |


# Get Worklog Item

Get a single worklog item by ID.

_🔐 This endpoint requires the **Plan** endpoint permission._

_This is a beta feature. Some details might change before it is released as a stable version._

```java
CompletableFuture<ApiResponse<WorklogResponse1>> getWorklogItemAsync(
    final int worklogItemId,
    final Boolean useUtc)
```

## Authentication

This endpoint requires [ApiKeyHeaderAuth](../../doc/auth/custom-header-signature.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `worklogItemId` | `int` | Template, Required | The id of the worklog item to get.<br><br>**Constraints**: `>= 1` |
| `useUtc` | `Boolean` | Query, Optional | Set to true to get timestamps in UTC.<br><br>**Default**: `false` |

## Response Type

**200**: A single worklog item.

This method returns an [`ApiResponse`](../../doc/api-response.md) instance. The `getResult()` getter of this instance returns the response data which is of type [`WorklogResponse1`](../../doc/models/worklog-response-1.md).

## Example Usage

```java
int worklogItemId = 218;
Boolean useUtc = false;

planApi.getWorklogItemAsync(worklogItemId, useUtc).thenAccept(result -> {
    // TODO success callback handler
    System.out.println(result);
}).exceptionally(exception -> {
    Throwable cause = exception.getCause();

    if (cause instanceof Worklog400ErrorException) {
        Worklog400ErrorException worklog400ErrorException = (Worklog400ErrorException) cause;
        worklog400ErrorException.printStackTrace();
    } else if (cause instanceof Worklog429ErrorException) {
        Worklog429ErrorException worklog429ErrorException = (Worklog429ErrorException) cause;
        worklog429ErrorException.printStackTrace();
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
  "worklogItemId": 10,
  "timestamp": "2023-01-08T00:00:00",
  "siteId": 5,
  "hoursWorked": 2.5,
  "comment": "Inverter B Offline With Repeated Fault.\nWork Performed - INV B was cleaned\n"
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | The request cannot be fulfilled due to bad syntax. | [`Worklog400ErrorException`](../../doc/models/worklog-400-error-exception.md) |
| 401 | The request is missing a valid API key. | `ApiException` |
| 403 | One of the following:<br><br>* The API key does not authorize access to the requested endpoint because of a missing endpoint permission.<br>* The API key does not authorize access to the requested data. Devices, sites or data signals can be limited. | `ApiException` |
| 404 | The requested resource could not be found. | `ApiException` |
| 405 | The HTTP method is not allowed for the endpoint. | `ApiException` |
| 429 | The API key has been used in too many requests in a given amount<br>of time. The following headers will be set in the response:<br><br>* `X-Rate-Limit-Limit` – The rate limit period (for example<br>  "1m", "12h", or "1d").<br>* `X-Rate-Limit-Remaining` – The remaining number of requests<br>  for this period.<br>* `X-Rate-Limit-Reset` – The UTC timestamp string (in ISO 8601<br>  format) when the remaining number of requests resets.<br><br>The limit is currently 1,000 requests/minute per API key and IP<br>address. | [`Worklog429ErrorException`](../../doc/models/worklog-429-error-exception.md) |

