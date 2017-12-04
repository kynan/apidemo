# apidemo

Following the steps to create the simple Orders demo

# Create API Blueprint in Apiary

1. go to apiary.io and logon using your credentials (you can create a new account for free if you don't have one)

2. Create a new API named Sample Orders (upper menu "Create New API")

3. Add the following markdown test

FORMAT: 1A
HOST: http://oc-144-21-66-168.compute.oraclecloud.com:3000/ordersdemo

# Orders

Simple get orders collection

## Orders Collection [/orders]

### Get Orders [GET]

+ Response 200 (application/json)

        [
            {
                "orderId": "order 1",
                "total_price": 50,
                "line_items": [
                    {
                        "lineItem": 1,
                        "productName": "Billy Bookshelf",
                        "quantity": 1,
                        "price": 50,
                        "currency": "EUR"
                    }
                ]
            }
        ]

4. Test the API mock by clicking on the "Get Orders" resource on the right-hand side on the screen, then click on Try > Call resource. Also take note of the URL used (which is the Mock URL, i.e. https://private-b3bf03-orders78.apiary-mock.com/orders)

5. Add API blueprint to GitHub repository by clicking on "Settings" menu item under "Link your GitHub repository"

6. Logon to Oracle API Platform CS (i.e. https://host/apiplatform) and create a new API as following:

    a. Click on "Create API"
    b. Add values as following: "Name": Orders Demo , "version": 1.0, "Description": Sample orders API
    c. Edit "API Request", add "v1/ordersdemo" as the "API Endpoint URL"
    e. Edit "Service Request", click "Enter a URL" then enter the Apiary Orders Demo mock URL
    f. Click on the "Deploy" icon (second top-down on the left), then click ""

# Create Sample Orders Microservice

1. Install NPM -follow instructions for your OS from https://nodejs.org/en/

2. Create package.json

npm init

Use as main file. server.js
Use following git repo: https://github.com/luisw19/node

3. Install Express as backend server

npm install --save express

4. Install body-parser to parse JSON payloads

npm install --save body-parser

5. Ensure all dependencies are installed in local “node_module” folder

npm install

6. Create server.js

touch server.js

6. Add the following code to test “Hello World”

var express     =   require("express");
var app         =   express();
var bodyParser  =   require("body-parser");
var router      =   express.Router();

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({"extended" : false}));

//Root resource with hello world
router.get("/",function(req,res){
    res.json({"response" : "Hello Birmingham UKOUG"});
});

app.use('/',router);

app.listen(3000);
console.log("Listening to PORT 3000");

7. Start the server

npm start

8. Stop the server (just control C) and let’s now add a “GET Orders” resource. Add the following block after Hellow World root

//orders resource
router.get("/orders",function(req,res){
    res.json(
        [{
          "orderId": "order 1",
          "total_price": 50,
          "line_items": [{
            "lineItem": 1,
            "productName": "Billy Bookshelf",
            "quantity": 1,
            "price": 50,
            "currency": "EUR"
          }]
        }]
      );
});
