Quality Control
---

### Parameter Generation

The `qc_applications` attribute in the data product resource causes the parameters to be created by data product management. For example:

```
data_product.qc_applications['TEMPWAT'] = ['qc_glblrng']
data_product.qc_applications['PRESWAT'] = ['qc_gradtst', 'qc_stuckvl']
```

Will cause data product management to generate three new parameters: `tempwat_glblrng_qc, preswat_gradtst_qc, preswat_stuckvl_qc`



### Upload File Format

```
global_range,reference designator,data product,units,author,min,max,,,
stuck_value,reference designator,data product,units,author,resolution,consecutive,,,
trend_test,reference designator,data product,units,author,length,poly_order,std,,
spike,reference designator,data product,units,author,accuracy,N,L,,
gradient_test,reference designator,data product,units,author,xunits,ddatdx,mindx,startdat,toldat
```

| testname      | reference designator | data product column | units column | author column | arg0       | arg1        | arg2  | arg3     | arg4   |
|---------------|----------------------|---------------------|--------------|---------------|------------|-------------|-------|----------|--------|
| global_range  | reference_designator | data product        | units        | author        | min        | max         |       |          |        |
| stuck_value   | reference_designator | data product        | units        | author        | resolution | consecutive |       |          |        |
| trend_test    | reference_designator | data product        | units        | author        | lenth      | poly_order  | std   |          |        |
| spike         | reference_designator | data product        | units        | author        | accuracy   | N           | L     |          |        |
| gradient_test | reference_designator | data product        | units        | author        | xunits     | ddadtx      | mindx | startdat | toldat |


Example:

```
# global_range,reference designator,data product,units,author,min,max,,,
# stuck_value,reference designator,data product,units,author,resolution,consecutive,,,
# trend_test,reference designator,data product,units,author,length,poly_order,std,,
# spike,reference designator,data product,units,author,accuracy,N,L,,
# gradient_test,reference designator,data product,units,author,xunits,ddatdx,mindx,startdat,toldat
global_range,CP01CNSM-MFD37-03-CTDBPD000,TEMPWAT,deg_C,Campbell,10.5,11,,,
stuck_value,CP01CNSM-MFD37-03-CTDBPD000,TEMPWAT,deg_C,Campbell,0.005,10,,,
spike_test,CP01CNSM-MFD37-03-CTDBPD000,TEMPWAT,deg_C,Campbell,0.0001,4,15,,
gradient_test,CP01CNSM-MFD37-03-CTDBPD000,TEMPWAT,dev_C,Campbell,s,[-50.0 50.0],10,,0.1
stuck_value,CP01CNSM-MFD37-03-CTDBPD000,PRESWAT,dbar,Campbell,0.005,10,,,
trend_test,CP01CNSM-MFD37-03-CTDBPD000,TEMPWAT,deg_C,Campbell,25,4,4.5,,

```


### Processing

![QC Processing Diagram](diagrams/QC%20Processing%20Flow.png)

There is one or more QC post processing processes running in the system. The QC Post Processor iterates over all site data products in the system, one at a time. If any of these site data products has a parameter that ends in `_qc` then it attempts to process QC for that data product.





