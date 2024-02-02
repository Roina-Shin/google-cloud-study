## Using openSSL to encrypt and decrypt a custom key


When using GCP Cloud Shell, openSSL is pre-installed in the system so you don't need to worry about downloading it.

Just run the command to create your custom key.


### Encrypt your custom phrase

If you want to encrypt a certain phrase you like, use this command:

```
echo iwillmakeagoodresultinmygcpexam | openssl base64
```


![encypt-key](/GCP_pictures/Study-logs/open-ssl/encrypt-phrase.PNG "Encrypt your custom phrase")


### Decrypt your encryption key


To decrypt your newly created encryption key, enter this command:

```
echo aXdpbGxtYWtlYWdvb2RyZXN1bHRpbm15Z2NwZXhhbQo= | openssl base64 -d
```


![decrypt-key](/GCP_pictures/Study-logs/open-ssl/decrypt-key.PNG "Decrypt your custom key")



## Google Cloud Storage Bucket versioning


- Now, using the OpenSSL knowledge, we can create an infile (which stores custom phrase) and outfile (which stores encrypted key) and upload it to the storage bucket.

- Then, we can create another set of infile and outfile and upload them to the same bucket again. It will create a new version of the 2 files inside the storage bucket.


- First, create a custom phrase in infile and save it.

- Then run this command to convert the phraase in infile to an encrypted key in outfile:


```
openssl base64 -in infile -out outfile
```


![create-infile-and-outfile](/GCP_pictures/Study-logs/open-ssl/create-infile-and-outfile.PNG "Create an infile and outfile")


- Now, upload the 2 files into the Google storage bucket. Run the command:


```
gsutil cp * gs://gatsby-flight-bucket/test/
```


![move-files-to-bucket](/GCP_pictures/Study-logs/open-ssl/move-files-to-bucket.PNG "Move file to storage bucket")



- Once done, set the versioning 'on' to your bucket:


```
gsutil  versioning set on gs://gatsby-flight-bucket/
```

- Then, change your infile and run the command again to reflect the change in encrypted key in outfile as well:


```
openssl base64 -in infile -out outfile
```

- Also, upload the changed infile and outfile to the bucket again.


```
gsutil cp * gs://gatsby-flight-bucket/test/
```


![reupload-files0](/GCP_pictures/Study-logs/open-ssl/reupload-files.PNG "Reupload files")



- Finally, run this command to see if all the versions of the files have been recorded so far:


```
gsutil ls -a gs://gatsby-flight-bucket/test/
```


![gsutil-versioning-working](/GCP_pictures/Study-logs/open-ssl/gsutil-versioning-working.PNG "Versioning working on bucket!")