# PHP Backend Interview Questions and Answers

## Question 1: "What is PHP and what are its main features?"
**Answer:** PHP (Hypertext Preprocessor) is a widely-used open-source server-side scripting language designed for web development. Its main features include:
- **Cross-platform compatibility:** PHP runs on various platforms (Windows, Linux, macOS).
- **Database integration:** PHP supports multiple databases, including MySQL, PostgreSQL, and SQLite.
- **Ease of use:** PHP is easy to learn and has a simple syntax.
- **Rich set of built-in functions:** PHP provides numerous built-in functions for various tasks.
- **Community support:** Being open-source, PHP has a large community that contributes to its development and provides support.

## Question 2: "What are the differences between `include`, `require`, `include_once`, and `require_once`?"
**Answer:**
- **`include`:** Includes and evaluates the specified file. If the file is not found, a warning is issued, but the script continues execution.
- **`require`:** Similar to `include`, but if the file is not found, a fatal error occurs, and the script stops execution.
- **`include_once`:** Includes the file only once. If the file has already been included, it will not be included again, preventing redeclaration errors.
- **`require_once`:** Similar to `require`, but ensures the file is included only once.

### Example:
```php
// include.php
echo "This is included file.";

// main.php
include 'include.php'; // This will include the file
require 'include.php'; // This will include the file again without error

include_once 'include.php'; // This will not include again
require_once 'include.php'; // This will not include again
```

## Question 3: "What is the difference between GET and POST methods in PHP?"
**Answer:**

### GET method:
- Sends data appended to the URL as query strings.
- Limited data size (around 2048 characters).
- Data is visible in the URL, making it less secure.
- Suitable for retrieving data without side effects (idempotent).

### POST method:
- Sends data in the request body, not visible in the URL.
- No size limitations (limited by server settings).
- More secure for sensitive data (e.g., passwords).
- Suitable for submitting data that changes server state (non-idempotent).

### Example:
```php
// Using GET method
echo '<form method="GET" action="process.php">
        <input type="text" name="username">
        <input type="submit" value="Submit">
      </form>';

// Using POST method
echo '<form method="POST" action="process.php">
        <input type="text" name="username">
        <input type="submit" value="Submit">
      </form>';
```

## Question 4: "What are sessions and cookies in PHP?"
**Answer:**

### Sessions:
- Used to store user data on the server for the duration of a user's visit.
- Data is stored on the server, and a unique session ID is sent to the user's browser as a cookie.
- Sessions are useful for maintaining state across multiple pages (e.g., user authentication).

### Example:
```php
// Starting a session
session_start();
$_SESSION['username'] = 'JohnDoe';
echo $_SESSION['username']; // Outputs: JohnDoe
```

## Cookies
- **Definition:** Small pieces of data stored on the user's browser.
- **Purpose:** Can store user preferences and other information for a specified duration.
- **Transmission:** Cookies are sent with every HTTP request, which can increase bandwidth usage.

### Example:
```php
// Setting a cookie
setcookie("username", "JohnDoe", time() + (86400 * 30), "/"); // 86400 = 1 day

// Accessing a cookie
if(isset($_COOKIE['username'])) {
    echo $_COOKIE['username']; // Outputs: JohnDoe
}
```

## Question 5: "How do you connect to a MySQL database using PHP?"
**Answer:** You can connect to a MySQL database using the `mysqli` or `PDO` extension. Here’s an example using `mysqli`:

### Example:
```php
$servername = "localhost";
$username = "username";
$password = "password";
$dbname = "database_name";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully";
```
## Question 6: "What is the purpose of the `mysqli_real_escape_string()` function?"
**Answer:** The `mysqli_real_escape_string()` function is used to escape special characters in a string for use in an SQL statement. This helps prevent SQL injection attacks by ensuring that user input is treated as data rather than executable code. It adds backslashes before characters like quotes, which could otherwise terminate the SQL command prematurely.

### Example:
```php
$user_input = "O'Reilly";
$safe_input = $conn->real_escape_string($user_input);
$sql = "SELECT * FROM users WHERE last_name = '$safe_input'";
```

## Question 7: "What are prepared statements and why are they used?"
**Answer:** Prepared statements are a feature of database interaction that allows you to execute the same SQL statement multiple times with different parameters. They are used to:
- Improve performance by pre-compiling the SQL statement.
- Enhance security by preventing SQL injection attacks, as user input is treated as data rather than executable code.

### Example using `mysqli`:
```php
$stmt = $conn->prepare("SELECT * FROM users WHERE email = ?");
$stmt->bind_param("s", $email);
$email = "user@example.com";
$stmt->execute();
$result = $stmt->get_result();
```

## Question 8: "Explain the MVC architecture in PHP."
**Answer:** MVC (Model-View-Controller) is a design pattern used in PHP frameworks to separate application logic:
- **Model:** Represents the data and business logic. It interacts with the database and handles data manipulation.
- **View:** Represents the user interface. It displays data to the user and sends user input to the controller.
- **Controller:** Acts as an intermediary between the model and view. It processes user input, interacts with the model, and updates the view accordingly.

### Example Structure:
/app /models UserModel.php /views userView.php /controllers UserController.php


## Question 9: "What is Composer and how is it used in PHP?"
**Answer:** Composer is a dependency manager for PHP that allows developers to manage libraries and packages in their projects. It simplifies the process of installing, updating, and autoloading dependencies. You can define your project dependencies in a `composer.json` file and run `composer install` to install them.

### Example of `composer.json`:
```json
{
    "require": {
        "monolog/monolog": "^2.0"
    }
}
```

### To install dependencies, run:
```bash
composer install
```

## Question 10: "How do you handle errors and exceptions in PHP?"
**Answer:** In PHP, errors can be handled using:
- **Error handling functions:** Functions like `error_reporting()`, `set_error_handler()`, and `trigger_error()` can be used to manage errors.
- **Exception handling:** Use `try`, `catch`, and `finally` blocks to handle exceptions. This allows you to catch errors and execute alternative code without stopping the script.

### Example:
```php
try {
    // Code that may throw an exception
    throw new Exception("An error occurred!");
} catch (Exception $e) {
    echo 'Caught exception: ',  $e->getMessage(), "\n";
} finally {
    // Code that will always execute
    echo "Execution finished.";
}
```
