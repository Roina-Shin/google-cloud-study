### [Source of this study material : Google Cloud Data Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-data-engineer-certification/)


## How to create a signed URL

- First, we should have a service account. Go to IAM and create a service account.


![create-sa](/GCP_pictures/Study-logs/signed-url/iam-sa.PNG "Create a service account")


- Click on 3 dots beside the service account and select **Manage Keys**.


- Then click **Add Key** and create one in JSON format.


![add-key-to-sa](/GCP_pictures/Study-logs/signed-url/add-key-to-sa.PNG "Add key to the service account")



- Once done, open your Cloud Shell.


![sa-key-created](/GCP_pictures/Study-logs/signed-url/sa-key-created.PNG "Service Account key created")


- Then go to the Storage Bucket and go inside the object details so that you get the URL like below:


![object-url](/GCP_pictures/Study-logs/signed-url/object-url.PNG "Object URL")



- This URL is not currently public. So if you try to access it in incognito browser, your access will be denied.


- But using this, you can create a signed URL. Go back to your Cloud Shell and upload your key file:


![upload-key](/GCP_pictures/Study-logs/signed-url/upload-key.PNG "Upload your key file")


- I changed the key file name into simpler one. Also check the content of the key file:


![key-check](/GCP_pictures/Study-logs/signed-url/key-check.PNG "Key check")


- Then install this python library **pyopenssl** which gsutil is going to internally use to generate the **signed URL**.


```
sudo pip3 install pyopenssl
```

- Also run the following commands to prevent error from occuring:


```
sudo apt-get install libssl-dev
```


```
sudo pip3 install --upgrade pip
```

- Finally run the first **pyopenssl* command again:


```
sudo pip3 install pyopenssl
```


- Now, we are going to generate our signed URL. Run the following command:


```
gsutil signurl -d 60s key.json gs://gatsby-flight-bucket/test/infile
```


![signurl-generation](/GCP_pictures/Study-logs/signed-url/signurl-generation.PNG "Signed url generation")


- But when you open the url your access will be denied. The reason lies in the service account permission.


![access-denied](/GCP_pictures/Study-logs/signed-url/access-denied.PNG "Access denied")


- Go to IAM and edit the service account's permissions so that it has 'Storage Object Admin' role:


![sa-permission](/GCP_pictures/Study-logs/signed-url/sa-permission.PNG "Service Account permissions")


- And if you run the signed url generation command again, you will successfully get an access to the file:


![access-successful-downloaded](/GCP_pictures/Study-logs/signed-url/access-success-downloaded.PNG "Access successful and downloaded the file")