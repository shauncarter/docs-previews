Hello, this is just a test page.

1. Open Visual Studio Code.
1. Create a file with the extension `.swift`
1. Run the following code:

```swift
var gemCounter = 0

while gemCounter < 1 {
    moveForward()
    if !isBlockedRight {
        turnRight()
    }
    if isBlocked && isBlockedRight {
        turnLeft()
    }
    if isBlocked && isBlockedRight && isBlockedLeft {
        turnLeft()
    }
    if isBlocked && isBlockedRight && !isBlockedLeft {
        turnLeft()
    }
    if isOnGem {
        collectGem()
        gemCounter += 1
    }
}
```

1. Now, what was the name of the variable above?

=== "Snowflake"

    |Property|Description|
    |---|---|
    |Name|A human-readable name for the component.|
    |Warehouse|Select a Snowflake warehouse.|

=== "Redshift"

    |Property|Description|
    |---|---|
    |Name|A human-readable name for the component.|
    |Schema|Select a Redshift schema.|

=== "BigQuery"

    |Property|Description|
    |---|---|
    |Name|A human-readable name for the component.|
    |Dataset|Select a BigQuery dataset.|
