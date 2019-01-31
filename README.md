<!DOCTYPE html>
<html>
<head>
	<title>Change Profile Picture</title>
</head>
<body>
<style type="text/css">
	.image
		{
			height: 260px;
			width: 200px;
			border: solid;	
		}
</style>	
<?php 
	if(isset($_POST['Upload']))
		{
			if(is_uploaded_file($_FILES['image']['tmp_name']))
				{
					$fn=$_FILES['image']['name'];
					$size=$_FILES['image']['size'];
					$type=$_FILES['image']['type'];
					$tpath=$_FILES['image']['tmp_name'];
					$error=$_FILES['image']['error'];
					$name=$_POST['name'];
					$mobile=$_POST['mobile'];
					$email=$_POST['email'];
						$str="abcdefghijklmnopqurstuvwxyz";
						$ext=substr(str_shuffle($str),5,15);
						$newname=$ext.$fn;
						if($type=='image/png' || $type=='image/jpg' || $type=='image/jpeg' || $type=='image/gif')
							{
								$status=move_uploaded_file($tpath,"Images/$newname");
									if($status==1)
									{
										echo "<pre>";
										echo "<h1>Profile Created Succesfully</h1>";
										echo "<h3>$name</h3>";
										echo "<h3>$mobile</h3>";
										echo "<h3>$email</h3>";
										echo "<img src='Images/$newname' class='image'>";
									}
									
							}
							else
								{
									echo "<h1>Please Select Valid Image Type</h1>";
								}
									
				}	
				else
					{
						echo "<h1>Choose Image To Upload On Profile</h1>";
					}
		}

?>
<form method="POST" action="#" enctype="multipart/form-data">
	<pre>
	<label>Your Name:</label>
	<input type="text" name="name"><br><br>
	<label>Your Mobile:</label>
	<input type="text" name="mobile"><br><br>
	<label>Your Email:</label>
	<input type="text" name="email"><br><br>
	<label>Choose Your Photo</label><br><br>
	<input type="file" name="image"><br><br>
	<input type="submit" name="Upload" value="Create Profile"><br>
</form>
</body>
</html>
