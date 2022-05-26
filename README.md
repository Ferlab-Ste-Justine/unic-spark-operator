# unic-spark-operator
Univers informationnel custom spark operator

## Publish an image to Docker Hub
To publish an image, tag the master branch using the following convention :
```
<spark_version>_<image_version>
```

Where `<spark_version>` is :
`3.0.0`
or
`3.1.1`.

And `<image_version>` is a number starting from 0.

The image will be pushed to `ferlabcrsj/spark-operator` repo on Docker Hub.