# Deploy-a-React-Application-on-Ubuntu-VM-with-Nginx

This guide provides step-by-step instructions to deploy and run a This React application on an Ubuntu VM using Nginx, making it accessible from a public IP.

# 1. Install Node.js and npm
Since React requires Node.js and npm, install them first:

sudo apt update

<img width="742" height="208" alt="image" src="https://github.com/user-attachments/assets/18da25d7-abd1-4f72-a6c8-c2fe6a6e9ad4" />


sudo apt install -y nodejs npm

<img width="742" height="261" alt="image" src="https://github.com/user-attachments/assets/933e3564-33e7-4df8-ad46-4437abe6fe79" />

Verify the installation:

node -v

<img width="380" height="67" alt="image" src="https://github.com/user-attachments/assets/8255e95f-4e69-4c0a-90f2-413f13482438" />

npm -v

<img width="322" height="52" alt="image" src="https://github.com/user-attachments/assets/dd25961a-09d0-4d5a-a3a8-136d0788779a" />

# 2. Install Nginx

Update package lists and install Nginx:

sudo apt install -y nginx

<img width="596" height="191" alt="image" src="https://github.com/user-attachments/assets/da4c9e2b-ea27-486d-9c1d-9614ac023781" />


Start and enable Nginx:

sudo systemctl start nginx
sudo systemctl enable nginx

<img width="956" height="135" alt="image" src="https://github.com/user-attachments/assets/f9905ea6-f4b5-42fa-bd1b-d78d2b9b4ed6" />

Check Nginx status:

systemctl status nginx

<img width="957" height="217" alt="image" src="https://github.com/user-attachments/assets/b87b8abc-8cd9-4026-8ca4-97cb159c8612" />

As we can see, our nginx application is up and running

<img width="1206" height="318" alt="image" src="https://github.com/user-attachments/assets/87c895bf-b849-4949-8467-ffb6e7bf5a80" />


# 3. Clone the React Application from GitHub
Navigate to a temporary directory and clone the repository:

git clone https://github.com/pravinmishraaws/my-react-app.git
cd my-react-app

<img width="736" height="207" alt="image" src="https://github.com/user-attachments/assets/3116dc9f-dd10-4dd5-b579-f5443a5c3254" />

Open the App.js file

Navigate to your React app’s source folder:

<img width="917" height="86" alt="image" src="https://github.com/user-attachments/assets/3b90ee43-a928-425e-802d-4b41284eff92" />

cd my-react-app/src
Open the App.js file in a text editor using vi and Modify the content

<h2>Deployed by: <strong>Your Full Name</strong></h2>
<p>Date: <strong>DD/MM/YYYY</strong></p>
Update your details like: Your Full Name & Date

<img width="641" height="195" alt="image" src="https://github.com/user-attachments/assets/6562efb9-8138-464e-96d5-a3062e645af9" />


# 4. Install Dependencies and Build the React App
Install required dependencies:

npm install
Build the React application:

<img width="462" height="37" alt="image" src="https://github.com/user-attachments/assets/c877c33b-1e84-46f9-b3df-c986f733116f" />

npm run build
This will generate a build/ folder with production-ready static files.

<img width="763" height="231" alt="image" src="https://github.com/user-attachments/assets/78aaa936-e3a3-4409-8844-5e010ad83459" />

# 5. Deploy Build Files to Nginx Web Directory
Remove any existing files in the Nginx web directory:

sudo rm -rf /var/www/html/*
Copy the React build files to /var/www/html/:

sudo cp -r build/* /var/www/html/
Set proper permissions:

sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html

# 6. Configure Nginx for React
Nginx configuration file:

echo 'server {
    listen 80;
    server_name _;
    root /var/www/html;
    index index.html;
    
    location / {
        try_files $uri /index.html;
    }

    error_page 404 /index.html;
}' | sudo tee /etc/nginx/sites-available/default > /dev/null

Restart Nginx to apply the changes:

sudo systemctl restart nginx

# 7. Find Your Public IP and Access the Application
Retrieve the public IP of your Ubuntu VM:

Now, we can access the React application our public IP:

<img width="1323" height="553" alt="image" src="https://github.com/user-attachments/assets/27bf2755-0fa3-4c71-b1ce-a749844df1e7" />


Our React App is Now Live on Ubuntu with Nginx accessible from a public IP.

# NETWORKING & ACCESS CHECKS (PRODUCTION BASICS)

 **IPs and interfaces (helps confirm network is up)**:ip a

<img width="852" height="237" alt="image" src="https://github.com/user-attachments/assets/3605c5f8-857f-4355-af1c-d20809837191" />


Default route (proves you can reach the internet via gateway):
ip route
DNS resolution (proves name → IP works):
dig pravinmishra.com +short
(or)
host pravinmishra.com
Connectivity test (quick packet-level check):
ping -c 4 thecloudadvisory.com
Listening ports + owning process (what is actually exposed):
sudo ss -tulpen
Firewall status (basic security signal, even if not configured):
sudo ufw status
(if ufw is not installed: write “ufw not installed”)
Evidence note:
For output, highlight/mention:
Is nginx listening on 0.0.0.0:80?
Is SSH on 22?
Any unexpected open ports?
PHASE 2: SERVICE HEALTH + PROCESS VALIDATION (SYSTEMD STYLE)


Assignment 4: Deploy a Professional Website (Confidence Project)

LinkedIn Post (MANDATORY)
Write a short LinkedIn post about what you achieved this week. Include:
Your application URL
3–5 lines: what you deployed + what you learned
1 screenshot proof (app page showing your Full Name)
Paste LinkedIn Post URL here: ___________________________
Paste screenshot of LinkedIn post here:

