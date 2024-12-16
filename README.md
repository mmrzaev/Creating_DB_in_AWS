# Mirkomil
Creating AWS Web Application

Here is link to youtube video: https://youtu.be/SqgRhNK9wEo?si=AssiwpO86vJrKSIn

**Step 1: Create an EC2 Instance**
  1.Log in to your AWS Management Console.
  
  2.In the search bar, type EC2 and select Launch Instance.
  
  3.Choose an Ubuntu OS as the base image.
  
  3.Skip modifying the Instance Type.
  
  4.Create a Key Pair:
  Name the key pair (e.g., your own name for simplicity).
  Save the .pem file in a secure folder where you won’t accidentally delete it.



**Step 2: Configure Security Groups**

1.Allow inbound traffic on the necessary ports:
  *Port 80 (HTTP)
  
  *Port 22 (SSH)
  
  *Port 443 (HTTPS)
  
  *Port 5432 (PostgreSQL)
  
  *Port 8000 (Custom Flask Application)
  
2.You can edit the inbound rules during the instance creation or afterward by modifying the security group.



**Step 3: Create an RDS Database**

1.Go to RDS in the AWS Management Console.

2.Click Create Database and choose PostgreSQL (look for the elephant icon).

3.Assign a database name, Master Username, and Password.

4.Ensure the RDS instance is accessible from your EC2 instance by associating it with the same VPC and security group.

5.Click Create Database to finish the setup.


**Step 4: Connect to the EC2 Instance**

1.Use SSH to access your EC2 instance:

//ssh -i "path_to_your_key.pem" ubuntu@<EC2_Public_IP>//

2.Update the system and install necessary software.

//sudo apt update
sudo apt install python3 python3-pip postgresql-client -y//

**Step 5: Connect to the RDS Database**

1.Use the following command to connect to your PostgreSQL database from the EC2 instance:

//psql -h <RDS_End_Point> -U <RDS_User> -d <RDS_Database_Name>//

Replace <RDS_User> (default is postgres) and <RDS_Database_Name> with your actual values

2.Create a **timetable** table:

//CREATE TABLE timetable (
    id SERIAL PRIMARY KEY,
    course_name VARCHAR(100),
    level VARCHAR(20),
    day VARCHAR(20),
    time VARCHAR(20)
);//

3.Insert sample data into the timetable table:

//INSERT INTO timetable (course_name, level, day, time)
VALUES
    ('COSC 2610 1T', 'Undergraduate', 'Tuesday', '1:00 PM'),
    ('ANSO 1050 8T', 'Undergraduate', 'Tuesday', '11:30 AM'),
    ('SCIN 1030 1T', 'Undergraduate Webnet+', 'Wednesday', '2:00 PM'),
    ('COSC 1570 5T', 'Undergraduate', 'Thursday', '12:00 PM'),
    ('GLBC 1200 2S', 'Undergraduate', 'Friday', '11:30 AM');
//

It's example please choose your own courses :)

**Step 6: Set Up Your Flask Application**

1.Create a project folder and navigate into it:

//mkdir project_name
cd project_name//

**(in my case it's mirkomil)**

2.Create the Flask application file:

//touch app.py//

**(in my case it's also app.py but you can choose your own name)**

3.Install the required Python libraries:

//pip3 install --upgrade pip
pip3 install flask psycopg2-binary//

4.Set up a virtual environment:

//python3 -m venv venv
source venv/bin/activate//

**Step 7: Develop the Flask Application**

1.Add the necessary code to **app.py**(it maybe your own name) for your Flask application to interact with the **timetable** database and display the data in a web interface.

2.Place the HTML file (index.html) in your project directory for the website interface. (index.html it's just example. You can name it what ever you want :))

**Step 8: Test and Run Your Application**

1.Disable the firewall (if necessary) to ensure traffic can flow to your application:

//sudo ufw disable//

2.Navigate to your Flask application directory and run the application:

//cd ~/path_to_your_app/
python3 app.py//

3.Open a web browser and access your application by entering:

(http://<EC2_Public_IP>:8000)

Replace <EC2_Public_IP> with the public IP of your EC2 instance.

You should now see a simple table displaying the timetable data from your PostgreSQL database.

Common Issues and Resolutions

Outdated Python version: Reinstall or upgrade Python to the latest version.

Failed library installation: Retry installing the libraries after ensuring proper access to the EC2 instance.

File not found error: Double-check the directory path to your application before running the command.

This concludes the guide for setting up a simple AWS web application with Flask and PostgreSQL.

Also, if you are meeting someproblems, try to read suggestions of ubuntu if it's not working just google you problem :)

