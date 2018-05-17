# data-pack : data packages for Python

Data-pack is a library for querying and downloading data in Python.

## Specification

A data pack is a JSON file, stored at a publicly accessible and
*persistent* HTTP URL, of the following format:

```
{
  "description": "Description of the package",
  "version": 0.0,
  "spec": 0,
  "files": [
    {
      "name": "tipsy",
      "url": "https://api.figshare.com/v2/articles/4810153",
      "sha256": "7a9bdf7156262a5f7d8c3e5fd56d7de6466fa1b7f874d54d7419d6db64351427",
      "type": "png",
      "meta": {
          "arbitrary": "metadata",
          "another": "field"
       }
    },

    {
      "name": "chelsea",
      "url": "https://github.com/scikit-image/scikit-image/raw/master/skimage/data/chelsea.png",
      "url": "https://some.other/backup/url/chelsea.png",
      "sha256": "596aa1e7cb875eb79f437e310381d26b338a81c2da23439704a73c4651e8c4bb",
      "meta": {
        "note": "You probably don't want to store data on GitHub---ephemeral"
      }
    }
  ]
}
```

## Using data-pack

```python
import datapack as dp
data = dp.datapack('http://somewhere.files.com/example_images.json')
```

We download and access the datapack as follows:

```python
data.fetch()  # download and cache the entire datapack
data.list()  # list files in the datapack
image = data.load('chelsea')
```

If `data.load` is called without `data.fetch`, fetching is done implicitly.

## Installable datapacks

Python packages can also specify a `__datapack__` variable, pointing
to a data-package, which which case the package can be accessed as follows:

```python
dp = dp.datapack(my_package)  # get url from my_package.__datapack__
```
