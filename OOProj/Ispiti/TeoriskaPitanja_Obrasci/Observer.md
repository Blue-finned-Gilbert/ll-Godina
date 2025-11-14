Observer definicija :

Observer je projektni obrazac koji uvodi one-to-many zavisnost između objekata:
jedan objekat Subject/Publisher drži stanje, a više objekata Observer/Subscriber se „pretplate“ na njega.
Kad god se stanje subjekta promeni, on automatski obaveštava sve svoje posmatrače, koji zatim ažuriraju svoje stanje.

Observer generelni primer:
```mermaid
classDiagram
    class Publisher {
        -subscribers: Subscriber[]
        -mainState
        +subscribe(s: Subscriber)
        +unsubscribe(s: Subscriber)
        +notifySubscribers()
        +mainBusinessLogic()
    }
    
    class Client {
    }
    
    class Subscriber {
        <<interface>>
        +update(context)
    }
    
    class ConcreteSubscriber {
        +update(context)
    }
    
    %% Relacije
    Publisher o-- "*" Subscriber : subscribers
    Client --> Publisher : creates/uses
    Client --> ConcreteSubscriber : creates
    ConcreteSubscriber ..|> Subscriber : implements
```





Observer primer upotrebe obrasca:

```mermaid
classDiagram
    class BankAccount {
        -balance: double
        -observers: AccountObserver[]
        +deposit(amount: double): void
        +withdraw(amount: double): void
        +attach(o: AccountObserver): void
        +detach(o: AccountObserver): void
        +notifyObservers(): void
    }

    class AccountObserver {
        <<interface>>
        +update(account: BankAccount): void
    }

    class SmsNotifier {
        +update(account: BankAccount): void
    }

    class MobileAppDisplay {
        +update(account: BankAccount): void
    }

    class AccountingSystem {
        +update(account: BankAccount): void
    }

    BankAccount "1" --> "*" AccountObserver : notifies

    SmsNotifier ..|> AccountObserver
    MobileAppDisplay ..|> AccountObserver
    AccountingSystem ..|> AccountObserver

```
