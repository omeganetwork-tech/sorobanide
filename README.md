# SorobanIDE
SorobanIDE: Visual Studio Code extension

# Draft: Architecture
## Domain
```mermaid
classDiagram
    class APIServer {
        -send()
        -receive()
    }

    class Transaction {
        Operation[] operations
    }

    class Operation
    
    class Command {
        build()
    }

    class CommandBuilder{
        build()
    }

    class CommandProcessor {
        execute()
    }
```

## Interactions
```mermaid
classDiagram
    class Event {
        -data
        +toString() string
    }
    Event <|-- NetworkEvent
    Event <|-- ChainEvent

    class Network 

    class APIServer {
        +Event events
        -sendTx(transaction)
        +execCommand(command, when, callback)
    }

    Server -- Network
    Server -- Event

    Server <|-- APIServer
    APIServer <|-- JSONRPC
    APIServer <|-- REST

    class APICommand
    APIServer *.. APICommand
```
**Server** belongs to a **Network** and emits **Events**.

**APIServer** is a **Server**.

APIServer interface is business-oriented: getTokenBalance(), depositToken(), withdrawToken(), getNetworkStatus(), etc.
