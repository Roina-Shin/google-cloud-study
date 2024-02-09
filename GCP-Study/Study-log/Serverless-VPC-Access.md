### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Serverless VPC Access

- Let's say Cloud SQL is available with only internal IP address. As we saw in **Private Service Access** demo, Cloud SQL is part of Google owned VPC network.

- Suppose you want to connect one of your serverless products (e.g. Cloud Run, App Engine, Google Function, etc.) to the Cloud SQL instance.

- In that case, you can use **Serverless VPC Access**. 

- We can create a Cloud Function instance and try to fetch data from the Cloud SQL instance in this demo.


## Serverless VPC Access Demo

- So, go create a Cloud function. To do that, you need to enable the API first. While enabling the API, go to **Serverless VPC access** and click **Create connector**.


- **Serverless VPC Access** allows Cloud Functions, Cloud Run (fully managed) services and App Engine standard environment apps to access resources in a VPC network using the internal IP addresses of those resources. 


![create-connector](/GCP_pictures/Study-logs/serverless-vpc-access/create-connector.PNG "Create connector")


- Go back to creating the Cloud Functions. While creating the function, be sure to put it in the same region as the VPC connector resides in. Also in **Connections** section, choose the **VPC Connector** you created earlier.


![function-connections](/GCP_pictures/Study-logs/serverless-vpc-access/function-connections.PNG "Function Connections section")


- When configuring the function, choose Python and only change the **return** part so that we can veryfiy:


![function-config](/GCP_pictures/Study-logs/serverless-vpc-access/test-purpose.PNG "Test purposes")



- Once done, when you go to the URL of function, you will see that it works.


![function-works](/GCP_pictures/Study-logs/serverless-vpc-access/function-works.PNG "Function works")


- Now, we want this function to fetch data from our Cloud SQL. So we need to change the source code.


- Go edit your Cloud Functions and its source code. In main.py file, we will make modifications.


- So before even the Function starts, we will execute these:


![start-code-writing](/GCP_pictures/Study-logs/serverless-vpc-access/starting-code-writing.PNG "Start code writing")


- For the **connection name**, you can find it in the Cloud SQL instance overview page:


![cloud-sql-overview](/GCP_pictures/Study-logs/serverless-vpc-access/cloud-sql-overview.PNG "Cloud SQL Overview page")


- Edit the source code like below:


```
import pymysql

db_user = 'root'
db_password = 'demo123'
db_name = 'yejindb'
db_connection_name = 'my-vpn-router-project:us-east1:private-service-access-demo'
host = '10.76.64.3'

@functions_framework.http
def svpc_fun(request):
    """HTTP Cloud Function.
    Args:
        request (flask.Request): The request object.
        <https://flask.palletsprojects.com/en/1.1.x/api/#incoming-request-data>
    Returns:
        The response text, or any set of values that can be turned into a
        Response object using `make_response`
        <https://flask.palletsprojects.com/en/1.1.x/api/#flask.make_response>.
    """
    request_json = request.get_json()

    cnx = pymysql.connect(user=db_user,password=db_password,host=host, db=db_name)

    with cnx.cursor() as cursor:
        cursor.execute('Select * from Persons;')
        result = cursor.fetchall()
        last_name = result[0][1]
        first_name = result[0][2]
    cnx.close()

    return str(first_name + " " + last_name)
```


- And for Requirements.txt:


```
PyMySQL==0.9.3
```

- Also, be sure to edit the **entry point (function name)**.



- After several tries, I failed to get the right message from the Cloud Function URL:


![fail-message](/GCP_pictures/Study-logs/serverless-vpc-access/try-failure.PNG "Try failure")



- But the idea behind this is we created this **Serverless VPC Connector** to connect our Function to the Cloud SQL instance.

