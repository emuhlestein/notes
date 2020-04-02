## JSON Server

JSON Server is a Node Module that you can use to create demo rest json webservice in less than a minute. All you need is a JSON file for sample data.

To install json server:  
    
    $npm install -g json-server
    

This start a simple web server:
    
    json-server db.json
    
db.json contains a json object of all the type or tables in the database.


$ json-server --watch db.json

By using this parameter we’re making sure that the server is started in watch mode which means that it watches for file changes and updates the exposed API accordingly.

A POST, PUT or PATCH request should include a Content-Type: application/json header to use the JSON in the request body. Otherwise it will result in a 200 OK but without changes being made to the data.

### Sample Table ###
A sample db.json database file:  

    {
        "employees": [
            {
                "id": 1,
                "first_name": "Sebastian",
                "last_name": "Eschweiler",
                "email": "sebastian@codingthesmartway.com"
            },
            {
                "id": 2,
                "first_name": "Steve",
                "last_name": "Palmer",
                "email": "steve@codingthesmartway.com"
            },
            {
                "id": 3,
                "first_name": "Ann",
                "last_name": "Smith",
                "email": "ann@codingthesmartway.com"
            }
       ] 
    }


npm install <package> This install the package into node_modules
  
npm install --save <package> This installs the package into node_modules and updates the package.json file, making this package a dependency for the project.
  
npm install --save-dev <package>  This installs the package and updates package.json to creates dev dependency.

Need to read about the npm left-pad problem.

yarn is like npm.


