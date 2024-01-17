# Deploying Django Project on AlmaLinux


## 1. Unzip the Project
```bash
# Navigate to the directory where your zip file is located
cd /path/to/your/project

# Unzip the project
unzip project.zip

# Enter the project directory
cd project
```


## 2. Install Python 3.8 or Higher
```bash
# Install development tools
sudo yum groupinstall "Development Tools"

# Install required dependencies
sudo yum install openssl-devel bzip2-devel libffi-devel

# Download and compile Python
wget https://www.python.org/ftp/python/3.8.10/Python-3.8.10.tgz
tar xzf Python-3.8.10.tgz
cd Python-3.8.10
./configure --enable-optimizations
make
sudo make altinstall
```


## 3. Install MySQL Connector
```bash
# Install MySQL development libraries
sudo yum install mysql-devel

# Install MySQL Connector
pip3.8 install mysqlclient
```


## 4. Install Gunicorn
```bash
# Install Gunicorn
pip3.8 install gunicorn
```
## 5. Create database 
```bash
# Connect to database
mysql -u username

# put password

# create database 
create database onps_epay_django;
```

## 6. Django Project Configuration
```python
# settings.py

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'onps_epay_django', # created database name here
        'USER': 'username',
        'PASSWORD': 'password',
        'HOST': 'hostname',
        'PORT': '3306', # change port if not already 3306
    },
    'readonly_db': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'abdessalam_database_name',
        'USER': 'username',
        'PASSWORD': 'password',
        'HOST': 'hostname',
        'PORT': '3306', # change port if not already 3306
    }
}
```


## 7. Install Requirements and Deploy the Project
```bash
# Install project requirements
pip3.8 install -r requirements.txt

# Run Django migrations
python3.8 manage.py migrate

# Start Gunicorn in the background
gunicorn epaydashboard.wsgi:application --bind 0.0.0.0:8000 --daemon

# Check if Gunicorn is running
ps aux | grep gunicorn
```

