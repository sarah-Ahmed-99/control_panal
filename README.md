# control_panal
Steps to create a simple web interface to control a bot and display its latest movement using XAMPP and Visual Studio Code (VS Code)

## 1. Set up XAMPP and VS Code:
   - Install XAMPP on your system, which includes Apache, MySQL, PHP and other components needed for web development.
   - Install VS Code, a popular code editor, on your system.
## 2. Create a new project directory:
   - In the htdocs folder of XAMPP, create a new directory for your project:  ` control.`
## 3. Database setup:
   - Register XAMMP control panel and we can allow Apache and MySQL modules.
   - Within XAMMP, go to Admin to access the MySQL management interface.
   - Create a new database, on `Control`.
   - Create the `robot_movements` table within SQL:
     
     ```
     CREATE TABLE robot_movements (
     id INT AUTO_INCREMENT PRIMARY KEY,
     direction VARCHAR(255) NOT NULL
     );
## 4. Create the control page:
 - In VS Code, create a new file named` index11`.php in the `control `directory.
 - Add the following code to create a simple control interface:
   
    ```
   <!DOCTYPE html>
    <html>
    <head>
    <title>Robot Control</title>
    <style>
        .button-container {
            display: flex;
            justify-content: center;
            align-items: center;
            margin-top: 20px;
        }

        .button-container button {
            margin: 0 10px;
            width: 100px;
            height: 100px;
            font-size: 20px;
            background-color: #a0a0a0;
            border-radius: 50%;
        }
    </style>
    </head>
     <body>
    <h1>Robot Control</h1>
    <form method="post" action="control11.php">
        <div class="button-container">
            <button name="direction" value="forward">Forward</button>
        </div>
        <div class="button-container">
            <button name="direction" value="left">Left</button>
            <button name="direction" value="stop">Stop</button>
            <button name="direction" value="right">Right</button>
        </div>
        <div class="button-container">
            <button name="direction" value="backward">Backward</button>
        </div>
    </form>
    </body>
    </html>
## 5. Create the control script:
- In VS Code, create a new file named `control11.php` in the `control` directory.
- Add the following code to process movement orders and update the database:
  
    ```
      <?php
    $servername = "localhost";
    $username = "root";
    $password = "";
    $dbname = "control";

    $conn = new mysqli($servername, $username, $password, $dbname);
    if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
    }

    if (isset($_POST['direction'])) {
    $direction = $_POST['direction'];

    $sql = "INSERT INTO robot_movements (direction) VALUES ('$direction')";

    if ($conn->query($sql) === TRUE) {
        echo "Robot movement recorded successfully.";
    } else {
        echo "Error: " . $sql . "<br>" . $conn->error;
    }
    } else {
    echo "No 'direction' value submitted in the POST request.";
    }

    $conn->close();
    ?>;

 ## 6. Create the presentation page:
  - In VS Code, create a new file named `last value.php` in the `control` directory.
  - Add the following code to retrieve the last recorded movement direction from the database and display it:
    
      ```
     <!DOCTYPE html>
      <html>
     <head>
    <title>Last Robot Movement</title>
    <style>
        .movement-circle {
            width: 100px;
            height: 100px;
            background-color: #a0a0a0;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px;
            font-weight: bold;
            color: #333;
            margin: 50px auto;
            border:1px solid black;
        }
        .back-link {
            display: block;
            text-align: center;
            margin-top: 20px;
        }
        .back-button {
            display: block;
            background-color: #a0a0a0;
            color: #333;
            text-decoration: none;
            padding: 10px 20px;
            border-radius: 5px;
            margin: 20px auto;
            width: fit-content;
            font-size: 18px;
        }
    </style>
    </head>
    <body>
     <h1> last value</h1>
    <div class="movement-circle">
        <?php
        $servername = "localhost";
        $username = "root";
        $password = "";
        $dbname = "control";

        $conn = new mysqli($servername, $username, $password, $dbname);

        if ($conn->connect_error) {
            die("Connection failed: " . $conn->connect_error);
        }

        $sql = "SELECT direction FROM robot_movements ORDER BY id DESC LIMIT 1";
        $result = $conn->query($sql);

        if ($result->num_rows > 0) {
            $row = $result->fetch_assoc();
            $lastDirection = $row["direction"];
            echo $lastDirection;
        } else {
            echo "No data";
        }

        $conn->close();
        ?>
    </div>
    <a href="index11.php" class="back-button">Go Back</a>
    </body>
    </html>
 ### Web-based control interface:
 
![5780701861165254790_121](https://github.com/sarah-Ahmed-99/control_panal/assets/174282340/6267876a-0d25-4899-adf1-05f3121e3134)
