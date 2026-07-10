# Todo Management

This application helps maintain daily todo lists and schedule tasks efficiently.

## Overview

Todo Management is a simple Java application to create, read, update, and delete todo items to help manage daily tasks in a scheduled manner.

## Features

- Add and remove todo items
- Mark items as complete
- List todos by status or date
- Simple file-based storage for persistence

## Requirements

- Java 11 or newer
- Maven (if provided build files) or a Java IDE

## Build & Run

1. Clone the repository:

   git clone https://github.com/bhagavan04/todo_management.git

2. Build (if using Maven):

   mvn clean package

3. Run the application (example):

   java -jar target/todo_management.jar

Adjust paths/commands according to how the project is organized.

## Efficient file handling

This project uses file-based storage for todos. To keep file I/O efficient and safe in Java, prefer these practices:

- Use buffered streams/readers (e.g., `BufferedReader`, `BufferedWriter`, `BufferedInputStream`, `BufferedOutputStream`) to reduce system calls.
- Use `try-with-resources` to ensure files are closed automatically and to avoid resource leaks:

```java
Path path = Paths.get("todos.txt");
try (BufferedReader br = Files.newBufferedReader(path, StandardCharsets.UTF_8)) {
    String line;
    while ((line = br.readLine()) != null) {
        // process line
    }
}
```

- Prefer NIO (java.nio.file.Files and Paths) for common operations — it's typically faster and more flexible than older IO APIs.
- When writing, minimize the number of write operations by accumulating content in a buffer or using `BufferedWriter`:

```java
try (BufferedWriter bw = Files.newBufferedWriter(path, StandardCharsets.UTF_8, StandardOpenOption.CREATE, StandardOpenOption.TRUNCATE_EXISTING)) {
    for (String todoLine : lines) {
        bw.write(todoLine);
        bw.newLine();
    }
}
```

- For larger datasets or concurrent access, consider switching to a lightweight database (e.g., SQLite) or add synchronization when multiple threads/processes may access the file.
- Avoid frequent small writes; batch changes when possible and write periodically or on graceful shutdown.

## Contributing

Contributions are welcome. Please open an issue or PR with improvements.

## License

Specify a license for the project (e.g., MIT) or add a LICENSE file.
