# Foeget_Password-in-PHP

<center>
<form action="" method="post">
    <p style="color:red;">Recover password</p>
    <input type="text" name="email" >
    <input type="submit" name="submit" >

</form>

</center>

<?php 

    if(isset($_POST['submit'])){

        $to_email = $_POST['email'];

        $con = mysqli_connect('localhost','root','','student');
        $query = "SELECT *FROM std_info WHERE email='$to_email'";
        $result = mysqli_query($con,$query);
        $count = mysqli_num_rows($result);

        if($count>0){

            while($row = mysqli_fetch_assoc($result)){

                $rec_password = $row['password'];
                $subject = "Password Recovery .";
                $body = "Your pass is : $rec_password";
                $headers = "From: mehedihasan231199@gmail.com";

                if(mail($to_email,$subject,$body,$headers)){

                    echo "Your password successfully sent to ".$to_email;
                }else{
                    echo "Password recover failed .. ";
                }
            }


        }else{
            echo "Your email not matched";
        }

    }



?>
