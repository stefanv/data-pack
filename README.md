# data-pack : data packages for Python

Data-pack is a library for querying and downloading data in Python.

The data-pack specification is given below.  Packages can be
distributed either directly (and queried via URL), or via an index.

## Specification: data-pack

A data pack is a JSON file, stored at a publicly accessible HTTP URL,
of the following format:

```
{
  "description": "Description of the package",
  "version": 0.0,
  "files": [
      {"name": "tipsy",
       "url": "https://api.figshare.com/v2/articles/4810153",
       "type": "png"},

      {"name": "chelsea",
       "url": "https://github.com/scikit-image/scikit-image/raw/master/skimage/data/chelsea.png"}
  ]
}
```

## Specification: index

An index is a JSON file, stored at a publicly accessible HTTP URL,
of the following format:

```
{
  "name": "neuroimage",
  "description": "Description of the neuroimaging archive",
  "datapacks": {
      "chelsea": "http://somewhere.org/data/chelsea.json",
      "sky": "http://somwhere.else.org/sky.json"
  }
}
```

## Using data-pack

```python
import datapack as dp
dp.add_index('neuroimage', 'http://www.index.org/datapack-index.json')
data = dp.datapack('neuroimage:chelsea')

data.fetch()  # download and cache the datapack
data.list()  # list files in the datapack
image = data.load('chelsea')
```
