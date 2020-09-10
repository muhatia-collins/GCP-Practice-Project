lab: Google Cloud Fundamentals: Getting Started with Compute Engine

    Objectives:
In this lab, you will learn how to perform the following tasks:

-Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
-Create a Compute Engine virtual machine using the gcloud command-line interface.
-Connect between the two instances.

Steps:
1. Create a Compute Engine virtual machine <my-vm-1> using the Google Cloud Platform (GCP) Console.

In GCP console, on the top right toolbar, click the Open Cloud Shell button

type the following comand in cloud shell
gcloud compute instances create "my-vm-1"
--machine-type "n1-standard-1"
--image-project "debian-cloud"
--image "debian-9-stretch-v20190213"
--subnet "default" --tags http

to create firewall rules for your instance, exercute the following
gcloud compute firewall-rules create allow-http
--action=ALLOW
--destination=INGRESS
--rules=http:80
--target-tags=http

2. Create a Compute Engine virtual machine using the gcloud command-line interface.

set the default zone for your instance using the following command
  gcloud config set compute/zone us-central1-b

run this command to create a virtual machine instance <my-vm-2>
gcloud compute instances create "my-vm-2"
--machine-type "n1-standard-1"
--image-project "debian-cloud"
--image "debian-9-stretch-v20190213"
--subnet "default"

close the cloud shell by exercuting the folowing command
  exit

3. Connect between the two instances.

To open a command prompt on the my-vm-2 instance, click SSH in its row in the VM instances list

Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:

ping my-vm-1
Press Ctrl+C to abort the ping command

Use the ssh command to open a command prompt on my-vm-1:
ssh my-vm-1
enter yes if prompted to continue connecting to a host with unknown authenticity.

install the Nginx web server at the command prompt on my-vm-1
sudo apt-get install nginx-light -y

Use the nano text editor to add a custom message to the home page of the web server:
sudo nano /var/www/html/index.nginx-debian.html

Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:
Hi from YOUR_NAME
Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor

Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
curl http://localhost/
the response will be the HTML source of the web server's home page, including your line of custom text

type "exit" without quotes to exit the command prompt on my-vm-1

To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
curl http://my-vm-1/
to sure to a get a  HTML source response of the web server's home page, including your line of custom text.

In the GCP Navigation menu, click Compute Engine > VM instances.
Copy the External IP address for my-vm-1 and paste it into the address bar of a new browser tab. You will see your web server's home page, including your custom text.

Congratulations!

When you have completed your lab, click End Lab. Qwiklabs removes the resources you’ve used and cleans the account for you.