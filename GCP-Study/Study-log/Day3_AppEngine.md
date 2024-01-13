### [Source of this study material : GCP Fundamentals for Beginners by Janakiram MSV](https://www.udemy.com/course/google-cloud-platform-gcp-fundamentals-for-beginners/)


App Engine is Platform as a Service product that provides web app developers and enterprises with access to Google's scalable hosting.

App Engine makes deployment, maintenance, scalability easy so that you can focus on innovation.

App Engine is especially suitable for building scalable web application and mobile backends.

Google App Engine is free up to a certain amount of resource usage.


========================================================

Q13. Your company is looking to build an application to be deployed on App Engine.
Thousands of users access your website every day and the number of instances needs to scale based on the request rate.
A minimum of 4 unoccupied instances should be live at all times.
Which scaling configuration should you use?

A : Use Automatic Scaling and set min_idle_instances to 4.

Automatic Scaling creates instances based on request rate, response latencies, and
other application metrics.

You can specify thresholds for each of these metrics, as well as a minimum number of instances
to keep running at all times.

Using Automatic Scaling with min_idle_instances set to 4 allows for automatic scaling based on the request rate.

It ensures that there are always at least 4 instances running,
even during periods of low traffic. 

Additionally, as the request rate increases, additional instances will be automatically created
to handle the load, ensuring optimal performance and scalability.