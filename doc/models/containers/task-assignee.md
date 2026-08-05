
# Task Assignee

## Class Name

`TaskAssignee`

## Cases

| Type | Factory Method |
|  --- | --- |
| [`TaskAssigneeUser`](../../../doc/models/task-assignee-user.md) | TaskAssignee.fromTaskAssigneeUser(TaskAssigneeUser taskAssigneeUser) |
| [`TaskAssigneePersonnel`](../../../doc/models/task-assignee-personnel.md) | TaskAssignee.fromTaskAssigneePersonnel(TaskAssigneePersonnel taskAssigneePersonnel) |
| [`TaskAssigneeManufacturer`](../../../doc/models/task-assignee-manufacturer.md) | TaskAssignee.fromTaskAssigneeManufacturer(TaskAssigneeManufacturer taskAssigneeManufacturer) |
| [`TaskAssigneeOther`](../../../doc/models/task-assignee-other.md) | TaskAssignee.fromTaskAssigneeOther(TaskAssigneeOther taskAssigneeOther) |
| `Object` | TaskAssignee.fromObject(Object object) |

## TaskAssigneeUser

### Initialization Code

#### Example

```java
TaskAssignee.fromTaskAssigneeUser(
        new TaskAssigneeUser.Builder(
            "firstName2",
            "lastName6",
            TaskAssigneeType.USER
        )
        .build()
    )
```

## TaskAssigneePersonnel

### Initialization Code

#### Example

```java
TaskAssignee.fromTaskAssigneePersonnel(
        new TaskAssigneePersonnel.Builder(
            TaskAssigneeType.USER
        )
        .build()
    )
```

## TaskAssigneeManufacturer

### Initialization Code

#### Example

```java
TaskAssignee.fromTaskAssigneeManufacturer(
        new TaskAssigneeManufacturer.Builder(
            TaskAssigneeType.USER
        )
        .build()
    )
```

## TaskAssigneeOther

### Initialization Code

#### Example

```java
TaskAssignee.fromTaskAssigneeOther(
        new TaskAssigneeOther.Builder(
            TaskAssigneeType.USER,
            "text0"
        )
        .build()
    )
```

## Object

### Initialization Code

#### Example

```java
TaskAssignee.fromObject(
        ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}")
    )
```

