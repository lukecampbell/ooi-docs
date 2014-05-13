# Coverage Model Users Guide

## Setting Values

Setting values is done through a dictionary, usually something like:

```python
data_dict = { 
  'time' : NumpyParameterData('time', time_array, time_array),
  'param0' : NumpyParameterData('param0', param0_array, time_array),
  'param1' : NumpyParameterData('param1', param0_array, time_array),
  'sparse0' : ConstantOverTime('sparse0', sparse_value, time_start=time0, time_end=time1)
}
coverage.set_parameter_values(data_dict)
```

Simple Enough, here's a convenience method:
  

```python
from coverage_model import NumpyParameterData

def _easy_dict(data_dict):
    if 'time' in data_dict:
        time_array = data_dict['time']
    else:
        elements = data_dict.values()[0]
        time_array = np.arange(len(elements))

    for k,v in data_dict.iteritems():
        data_dict[k] = NumpyParameterData(k, v, time_array)
    return data_dict
```

## Intervals for Sparse Values

You can use None's to specify open intervals


