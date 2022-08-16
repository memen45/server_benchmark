# server_benchmark
Minimal benchmark comparing some server languages / stacks 

Goal is to return `{"statuscode":200,"message":"Hello World!"}` as fast as possible.

## C++ 

### [Oatpp](https://oatpp.io/)
Follow the [starter project](https://oatpp.io/docs/start/project/) guide:
`git clone https://github.com/oatpp/oatpp-starter`
Then build and run.

### [Simple-Web-Server](https://gitlab.com/eidheim/Simple-Web-Server)
Follow the README.md in the repository to install dependencies
`git clone https://gitlab.com/eidheim/Simple-Web-Server`
Then follow the build steps, afterwards, enable -O2 optimisation:
```
cd build
cmake -DCMAKE_BUILD_TYPE=DEBUG -DCMAKE_C_FLAGS_DEBUG="-g -O2" -DCMAKE_CXX_FLAGS_DEBUG="-g -O2" ..
make VERBOSE=1
```

## JavaScript 
### [ExpressJS](https://github.com/expressjs/express)
Follow the guide under [examples](https://github.com/expressjs/express#examples):
```
git clone https://github.com/expressjs/express --depth 1
cd express
npm install
```

Now modify `examples/hello-word/index.js`

## PHP
Using Apache webserver with a simple vhost
```
<VirtualHost *:8000>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html/phptest

        <Directory "/">
          AllowOverride None
        </Directory>
        
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Add `Listen 8000` to `/etc/apache2/ports.conf` to enable port 8000
Add the file `/var/www/html/phptest/index.php`

## Testing
### Sequential requests
Each of the servers were tested using no concurrent requests: `ab -n 60000 -c 1 http://localhost:8000/`

Requests per second:
![image](https://user-images.githubusercontent.com/27782135/184961047-f17147a0-7b90-4f79-9001-0e007bc96a27.png)
Response time
![image](https://user-images.githubusercontent.com/27782135/184961557-eda57e01-bfd5-4144-8fb0-2ed6cbe4c224.png)

### Concurrent requests
Each of the servers were tested using 1000 concurrent requests: `ab -n 60000 -c 1000 http://localhost:8000/`

Requests per second
![image](https://user-images.githubusercontent.com/27782135/184962864-5c11678a-fcab-4968-8a9d-62b8cba7628e.png)

Response time
![image](https://user-images.githubusercontent.com/27782135/184962720-22022bf0-5d43-4b77-bc3d-ba28d56f7ceb.png)



