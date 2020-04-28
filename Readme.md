# Purpose

The target of this document is to help configure EC2 instances so that it can run python scripts.

# Steps
Follow the following steps to complete the configuration-

### Spin an EC2 instance

* Login to your AWS console.
* Select  Amazon Linux AMI 2018.03.0 (HVM), SSD Volume Type.
* Make sure you download the .pem file.

### Access the EC2 instance
* Open terminal in your MacOS.
* Navigate to the path where you kept the pem file and change the access permission.
  ```bash
  chmod 400 /path/to/.pem/file
  ```
* Connect to the EC2 instance using ssh and public ip of the EC2.
  ```bash
  ssh -i /path/to/.pem/file ec2-user@ec2-xx-xxx-xxx-xxx.compute.amazonaws.com
  ```

### Install and configure the Python environment
* By default the linux instance will have Python2 installed.
* Install Python 3 by running the following script.
  ```bash
  sudo yum install python36
  ```
* Even after installing Python3.6, the version might still indicate to the older Python. To resolve this issue set an alternative path.
  ```bash
  sudo alternatives --set python /usr/bin/python3.6
  ```
* Check version to make sure the path is updated.
  ```bash
  python --version
  ```
* Once Python is installed you will need to install pip3.
  ```bash
  cd /tmp
  curl -O https://bootstrap.pypa.io/get-pip.py
  python3 get-pip.py --user
  ```
### Install required python packages
To run python scripts you will need to install various packages. In this scenario we will need to install boto3 package so that we can interact with various AWS services.
```bash
pip3 install boto3
```

### Configure boto3 to access AWS services
Once boto3 package is installed you need to configure the was credentials so that the program knows which AWS profile to interact with.
```bash
aws configure

AWS Access Key ID: xxxxxxxxxx
AWS Secret Access Key: xxxxxxxxx
Default region name: xx-xxxx-x
Default output format: json
```

### Copy file from local machine to ec2
Now you have an EC2 instance which is configured with Python and Boto3. To copy the python code from your local system to the EC2 instance, use the following script.
```bash
scp -i ~/path/to/.pem/file/ ~/path/of/file/to/copy ec2-user@ec2-xx-xxx-xxx-xxx.compute.amazonaws.com:/path/in/ec2
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
