## Azure Virtual Machine

VM checklist

* **Start with the network**
* **Name the VM**
* **Decide the location for the VM**
* **Determine the size of the VM**
* **Understanding the pricing model**
* **Storage for the VM**
* **Select an operating system**



ls -la / to show the root of the disk
ps -l to show all the running processes
dmesg to list all the kernel messages
lsblk to list all the block devices - here you will see your drives

## Initialize data disks

* **Run the command with sudo and supply the disk you want to partition. We can use the following command to create a new primary partition:**
```
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```
* **we need to write a file system to the partition with the mkfs command.**
```
sudo mkfs -t ext4 /dev/sdc1
```
* **we need to mount the drive to the file system. Let's assume we will have a data folder. Let's create the mount point folder and mount the drive**

```
sudo mkdir /data && sudo mount /dev/sdc1 /data
```

## Create Mean Stack 

```

az vm create \
  --resource-group <rg-name> \
  --name MeanStack \
  --image Canonical:UbuntuServer:16.04-LTS:latest \
  --admin-username azureuser \
  --generate-ssh-keys

```

* **Open port 80 on the VM to allow incoming HTTP traffic to the web application**

```
az vm open-port \
  --port 80 \
  --resource-group <rg-name> \
  --name MeanStack
```

* **Create an SSH connection to your VM.**

```
ipaddress=$(az vm show \
  --name MeanStack \
  --resource-group <rg-name> \
  --show-details \
  --query [publicIps] \
  --output tsv)

  ssh azureuser@$ipaddress

  ```

  * **Install MongoDB**

  ```
  sudo apt-get install -y mongodb
  sudo systemctl status mongodb
  mongod --version
  ```

  * **Install NodeJS**

  ```
  curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
  sudo apt install nodejs
  nodejs -v
  ```

  * **Create a basic web application**

  ```
  cd ~
mkdir Books
touch Books/server.js
touch Books/package.json
mkdir Books/app
touch Books/app/model.js
touch Books/app/routes.js
mkdir Books/public
touch Books/public/script.js
touch Books/public/index.html
```
app/model.js

```
var mongoose = require('mongoose');
var dbHost = 'mongodb://localhost:27017/Books';
mongoose.connect(dbHost, { useNewUrlParser: true } );
mongoose.connection;
mongoose.set('debug', true);
var bookSchema = mongoose.Schema( {
    name: String,
    isbn: {type: String, index: true},
    author: String,
    pages: Number
});
var Book = mongoose.model('Book', bookSchema);
module.exports = Book;
```
Create Express Route (app/routes.js)

```
var path = require('path');
var Book = require('./model');
var routes = function(app) {
    app.get('/book', function(req, res) {
        Book.find({}, function(err, result) {
            if ( err ) throw err;
            res.json(result);
        });
    });
    app.post('/book', function(req, res) {
        var book = new Book( {
            name:req.body.name,
            isbn:req.body.isbn,
            author:req.body.author,
            pages:req.body.pages
        });
        book.save(function(err, result) {
            if ( err ) throw err;
            res.json( {
                message:"Successfully added book",
                book:result
            });
        });
    });
    app.delete("/book/:isbn", function(req, res) {
        Book.findOneAndRemove(req.query, function(err, result) {
            if ( err ) throw err;
            res.json( {
                message: "Successfully deleted the book",
                book: result
            });
        });
    });
    app.get('*', function(req, res) {
        res.sendFile(path.join(__dirname + '/public', 'index.html'));
    });
};
module.exports = routes;
```

Create the client-side JavaScript application(public/script.js)

```
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $http) {
    var getData = function() {
        return $http( {
            method: 'GET',
            url: '/book'
        }).then(function successCallback(response) {
            $scope.books = response.data;
        }, function errorCallback(response) {
            console.log('Error: ' + response);
        });
    };
    getData();
    $scope.del_book = function(book) {
        $http( {
            method: 'DELETE',
            url: '/book/:isbn',
            params: {'isbn': book.isbn}
        }).then(function successCallback(response) {
            console.log(response);
            return getData();
        }, function errorCallback(response) {
            console.log('Error: ' + response);
        });
    };
    $scope.add_book = function() {
        var body = '{ "name": "' + $scope.Name +
        '", "isbn": "' + $scope.Isbn +
        '", "author": "' + $scope.Author +
        '", "pages": "' + $scope.Pages + '" }';
        $http({
            method: 'POST',
            url: '/book',
            data: body
        }).then(function successCallback(response) {
            console.log(response);
            return getData();
        }, function errorCallback(response) {
            console.log('Error: ' + response);
        });
    };
});

```
Create the user interface(public/index.html)

```
<!doctype html>
<html ng-app="myApp" ng-controller="myCtrl">
<head>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.2/angular.min.js"></script>
    <script src="script.js"></script>
</head>
<body>
    <div>
    <table>
        <tr>
        <td>Name:</td>
        <td><input type="text" ng-model="Name"></td>
        </tr>
        <tr>
        <td>Isbn:</td>
        <td><input type="text" ng-model="Isbn"></td>
        </tr>
        <tr>
        <td>Author:</td>
        <td><input type="text" ng-model="Author"></td>
        </tr>
        <tr>
        <td>Pages:</td>
        <td><input type="number" ng-model="Pages"></td>
        </tr>
    </table>
    <button ng-click="add_book()">Add</button>
    </div>
    <hr>
    <div>
    <table>
        <tr>
        <th>Name</th>
        <th>Isbn</th>
        <th>Author</th>
        <th>Pages</th>
        </tr>
        <tr ng-repeat="book in books">
        <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
        <td>{{book.name}}</td>
        <td>{{book.isbn}}</td>
        <td>{{book.author}}</td>
        <td>{{book.pages}}</td>
        </tr>
    </table>
    </div>
</body>
</html>

```

Create the Express server to host the application(server.js)

```
var express = require('express');
var bodyParser = require('body-parser');
var app = express();
app.use(express.static(__dirname + '/public'));
app.use(bodyParser.json());
require('./app/routes')(app);
app.set('port', 80);
app.listen(app.get('port'), function() {
    console.log('Server up: http://localhost:' + app.get('port'));
});
```
package.json

```
{
  "name": "books",
  "description": "Sample web app that manages book information.",
  "license": "MIT",
  "repository": {
    "type": "git",
    "url": "https://github.com/MicrosoftDocs/mslearn-build-a-web-app-with-mean-on-a-linux-vm"
  },
  "main": "server.js",
  "dependencies": {
    "express": "~4.16",
    "mongoose": "~5.3",
    "body-parser": "~1.18"
  }
}
```

sudo apt install npm

npm install

sudo nodejs server.js