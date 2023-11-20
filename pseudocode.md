## 1.Use Case API

## 1.1 Function to add a Usecase

- Method: POST
- API End Point: `/api/usecase`

### add_usecase Function

### Description
This function handles the addition of a usecase by parsing JSON data from the event body, inserting the data into a PostgreSQL database, and returning a response.

### Function Definition

    Function add_usecase(event, context, callback):

    Parse the JSON data from the event body
    Initialize a new PostgreSQL client with connection details and Establish the connection
    
    Try:
        Check if the event body is empty
            Close the database connection
            Return the response with a 400 status code
            
        Else:
            Execute a query to insert event details into the "usecase" table

        Close the PostgreSQL connection
        Return the response with a 200 status code
        

    If an error occurs during the try block, execute the following block
    Catch (error):
        
        Close the PostgreSQL connection
        Return the response with a 400 status code
        

## 1.2 Function to update an existing Usecase based on id.

- Method: PUT
- API End Point: `/api/usecase/:id`

### update_usecase Function

### Description
This function updates a usecase in a PostgreSQL database based on the provided JSON data and usecase ID.

#### Function Definition
    
    Function update_usecase(event, context, callback):

    Extract usecase ID from path parameters
    Parse JSON data from the event body
    Set up a connection to a PostgreSQL database and Establish the database connection

    Try:

        Check if the usecase ID exists
            If (id exists):
                Execute a query to update the usecase details in the "usecase" table

                Check if the update was successful
                If (res.rowCount == 1):
                    Return success response
                    

    If an error occurs during the try block, execute the following block
    Catch (error):
        
        Close the PostgreSQL connection
        Return the response with a 400 status code
        

## 1.3 Function to delete an existing Usecase based on id.

- Method: DELETE
- API End Point: `/api/usecase/:id`

### delete_usecase Function

### Description
This function deletes a usecase in a PostgreSQL database based on the provided JSON data and usecase ID.

#### Function Definition

Function delete_usecase(event, context, callback):
    Extract usecase ID from path parameters

    Set up a connection to a PostgreSQL database and Establish the database connection


    Try:
        If (id exists):
            Execute a query to delete the usecase with the specified ID from the "usecase" table

            Check if the delete was successful
                Return success response

    If an error occurs during the try block, execute the following block
    Catch (error):
        Close the PostgreSQL connection
        Return the response with a 400 status code
        


## 1.4 Function to get an existing Usecase basedon id.

- Method: GET
- API End Point: `/api/usecase/:id`

### get_usecase Function

### Description
This function gets a usecase in a PostgreSQL database based on the provided JSON data and usecase ID.

### Function get_usecase(event, context, callback):

    Set up a connection to a PostgreSQL database and Establish the database connection

    Check if queryStringParameters exist in the event
    If (event.queryStringParameters exists):
        Assign queryStringParameters to the data object


    Try:
        Check if data object is empty
        If (JSON.stringify(data) is empty):
            Execute query to select all usecases from "usecase" table
        ElseIf (data has an 'id' field):
            Execute query to select usecase by ID from "usecase" table
        Else:
            Execute query to select usecases from "usecase" table based on filters

        Close the database connection
        Return success response

    Catch (error):

        Close the database connection
        Return response with a 400 status code