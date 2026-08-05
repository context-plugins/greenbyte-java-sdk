
# Tasks Response Assignee

## Class Name

`TasksResponseAssignee`

## Cases

| Type | Factory Method |
|  --- | --- |
| [`TaskAssigneeUser`](../../../doc/models/task-assignee-user.md) | TasksResponseAssignee.fromTaskAssigneeUser(TaskAssigneeUser taskAssigneeUser) |
| [`TaskAssigneePersonnel`](../../../doc/models/task-assignee-personnel.md) | TasksResponseAssignee.fromTaskAssigneePersonnel(TaskAssigneePersonnel taskAssigneePersonnel) |
| [`TaskAssigneeManufacturer`](../../../doc/models/task-assignee-manufacturer.md) | TasksResponseAssignee.fromTaskAssigneeManufacturer(TaskAssigneeManufacturer taskAssigneeManufacturer) |
| [`TaskAssigneeOther`](../../../doc/models/task-assignee-other.md) | TasksResponseAssignee.fromTaskAssigneeOther(TaskAssigneeOther taskAssigneeOther) |
| `Object` | TasksResponseAssignee.fromObject(Object object) |

## TaskAssigneeUser

### Initialization Code

#### Example

```java
TasksResponseAssignee.fromTaskAssigneeUser(
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
TasksResponseAssignee.fromTaskAssigneePersonnel(
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
TasksResponseAssignee.fromTaskAssigneeManufacturer(
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
TasksResponseAssignee.fromTaskAssigneeOther(
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
TasksResponseAssignee.fromObject(
        ApiHelper.deserialize("{\"key1\":\"val1\",\"key2\":\"val2\"}")
    )
```

