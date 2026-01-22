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
Open the App.js file in a text editor:

nano App.js
(or use vi/vim if you prefer)

Modify the content

<h2>Deployed by: <strong>Your Full Name</strong></h2>
<p>Date: <strong>DD/MM/YYYY</strong></p>
Update your details like: Your Full Name & Date

4. Install Dependencies and Build the React App
Install required dependencies:

npm install
Build the React application:

npm run build
This will generate a build/ folder with production-ready static files.

5. Deploy Build Files to Nginx Web Directory
Remove any existing files in the Nginx web directory:

sudo rm -rf /var/www/html/*
Copy the React build files to /var/www/html/:

sudo cp -r build/* /var/www/html/
Set proper permissions:

sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
6. Configure Nginx for React
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
7. Find Your Public IP and Access the Application
Retrieve the public IP of your Ubuntu VM:

curl ifconfig.me
Now, students can access the React application in a browser using:

http://<your-public-ip>
For example, if the public IP is 203.0.113.25, visit:

http://203.0.113.25
8. Verify the Deployment
Ensure Nginx is correctly serving the React app:

curl <your-public-ip>
If successful, your React app is live!

Your React App is Now Live on Ubuntu with Nginx!
Now your React application is deployed on an Ubuntu VM with Nginx, accessible from a public IP.
