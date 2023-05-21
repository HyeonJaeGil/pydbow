

# pydbow
## python wrapped version of DBoW3 library


This is pybind repository of well-known Loop Closure Detection (LCD) library, DBoW3.
For details about the library itself, please refer to the original repository. [link here](https://github.com/rmsalinas/DBow3.git)


## Installation notes
Just like the original DBoW3 library, **OpenCV** is required.
Users can now build this extension module with **pip install**. 
There are no python module dependencies, but we recommend python 3.7+.
Using python virtual environment (e.g. anaconda3) is recommended.
```
# assume current path is project root (/path/to/pydbow)
pip install -e .
```
## How to use

### Vocabulary Creation

```python

import pydbow

# create from an empty instance
voc = pydbow.Vocabulary(4,3) # k, L

# training_features should be a list of binary descriptors
# each descriptor is 2d ndarray, where each row is a descriptors
# so the shape should be N,D
# N = number_of_descriptors_from_an_image
# D = dimension_of_descriptors with dtype as uint8
# note that D should be packbits (256 bits -> 32 dimensions)
training_features = [] # append binary descriptors here
voc.create(training_features)

# save vocabulary
voc.save("save/path/here")

# OR load vocabulary from a file
voc = pydbow.Vocabulary("path/to/file")
```

### Database add & query

```python

import pydbow

db = pydbow.Database(voc)

# add 2d ndarray binary descriptors to database
# its shape should be the same as the one from vocabulary creation
db.add(descriptors)

# parameters: descriptors, max_results, max_id
# returns: a list of tuple (index, score)
results = db.query(q_descriptors, 5, -1)
```


## Citing

If you use this software in an academic work, please cite:
```@online{DBoW3, author = {Rafael Muñoz-Salinas}, 
   title = {{DBoW3} DBoW3}, 
  year = 2017, 
  url = {https://github.com/rmsalinas/DBow3}, 
  urldate = {2017-02-17} 
 } 
```