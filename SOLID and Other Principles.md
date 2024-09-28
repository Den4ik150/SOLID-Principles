# SOLID Principles in JavaScript

The SOLID principles provide guidelines for building clean, scalable, and maintainable code. Here's a breakdown of each principle with JavaScript examples:

# D

<details>
  
## 1. Single Responsibility Principle (SRP)
  
**Definition**: A class should have only one reason to change. It should only have one responsibility or function.

### Example:
```js
class Event {
  setTime(startTime, endTime) { /*...*/ }
  setTitle(title) { /*...*/ }
}

class Calendar {
  addEvent(event) { /*...*/ }
  removeEvent(event) { /*...*/ }
  getEventsBetween(startDate, endDate) { /*...*/ }
}

class CalendarExporter {
  exportToXML(filter) { /*...*/ }
  exportToJSON(filter) { /*...*/ }
}
```
- Explanation: Responsibilities are split among different classes (Event, Calendar, CalendarExporter) to ensure each has a single responsibility.
  
</details>
## 2. Open-Closed Principle (OCP)

  **Definition**: Software entities should be open for extension but closed for modification. We can add new functionality without changing existing code.

### Example:
  ```js
  class Event {
  renderNotification() {
    return `You have an event in ${this.calcMinutesUntil()} minutes!`;
  }
}

class ImportantEvent extends Event {
  renderNotification() {
    return `Urgent! ${super.renderNotification()}`;
  }
}
```

- Explanation: The ImportantEvent class extends the functionality of Event without modifying it, following the OCP.

## 3. Liskov Substitution Principle (LSP)

  **Definition**: Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.

  ### Example:

  ```js
class Event {
  renderNotification() { /*...*/ }
}

class ImportantEvent extends Event {
  renderNotification() { /*...*/ }
}

class Calendar {
  notifyUpcomingEvents() {
    this.events.forEach(event => {
      event.renderNotification();
    });
  }
}
```

-Explanation: The Calendar class can handle Event and ImportantEvent without needing to know the specific type.

## 4. Interface Segregation Principle (ISP)

  **Definition**: No client should be forced to depend on methods it does not use.

  ### Example:

  ```js
class Printable {
  print() { /*...*/ }
}

class Scannable {
  scan() { /*...*/ }
}

class Printer implements Printable {
  print() { /*...*/ }
}

class Scanner implements Scannable {
  scan() { /*...*/ }
}
```

-Explanation: By segregating interfaces, we ensure that classes only implement methods relevant to them.

## 5. Dependency Inversion Principle (DIP)

**Definition**: High-level modules should not depend on low-level modules. Both should depend on abstractions.

### Example:

```js
class NotificationService {
  send(notification) { /*...*/ }
}

class EmailService extends NotificationService {
  send(notification) { console.log("Sending email: ", notification); }
}

class Calendar {
  constructor(notificationService) {
    this.notificationService = notificationService;
  }
  notify(event) {
    this.notificationService.send(event.renderNotification());
  }
}
```

-Explanation: The Calendar class depends on an abstraction (NotificationService), making it flexible to work with any notification method (e.g., email, SMS).
