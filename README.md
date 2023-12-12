<?php
$username=$_POST['txt'];
$email=$_POST['email'];
$password=$_POST['pswd'];
if(!empty($username) || !empty($email) || !empty($password)){
    $host = "localhost";
    $dbUsername = "root";
    $dbPassword = "9867782924@r;
    $dbname = "project";
    // creating connection;
    $conn = new mysqli($host, $dbUsername, $dbPassword, $dbname);
    if(mysqli_connect_error()){
        die('Connect Error ('.mysqli_connect_errno().') '.mysqli_connect_error());

    }
    else{
        $SELECT= "SELECT email from uservalues where email= ? Limit 1";
        $INSERT= "INSERT INTO uservalues(User_Name, email, pw) values(?, ?, ?)";
        //Preapare staement 
        $stmt= $conn-> prepare($SELECT);
        $stmt-> bind_param("s", $email );//bind the email paramter
        $stmt-> execute();
        $stmt-> bind_param("s", $email);
        $stmt-> store_result();
        $rnum= $stmt-> num_rows;
        if($rnum==0){
            $stmt->close();
            $stmt= $conn->prepare($INSERT);
            $stmt->bind_param("sss", $username,$email ,$password);
            $stmt->execute();
            echo 'Connected Successfully';





        }
        else{
            echo "someone alredy register using this id";
        }
        // close statement and connection
        $stmt -> close();
        $conn->close();
        

    }
 
}
else{
    echo "all filed is required";
    die();
}

?>
