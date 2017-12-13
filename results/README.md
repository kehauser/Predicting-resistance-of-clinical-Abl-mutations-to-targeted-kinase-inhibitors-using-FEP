# Experimental and computational datasets

## Data format

### `All_144_v173_all5ns.KeepLOD.dat`

FEP+ results, Experimental reference data

If file has LESS THAN 9 entries per line, then that value == name of inhibitor.
	e.g. axitinib

If file has more than one entry per line, here's what that data is:
```
	Mutation, IC50 (nM), DDG_exp (kcal/mol), DDG_FEP_run1, cc_err_FEP_run1, DDG_FEP_run2, cc_err_FEP_run2, DDG_FEP_run3, cc_err_FEP_run3
  e.g. M244V	690	-0.11	0.05	0.41	-0.20	0.41	0.08	0.41
```
		each entry on a line is tab-delimited  

	Here's how to read the data (python function):
```python
def read_inpfile(inpfile):
  ddg_run1,ddg_run2,ddg_run3,ddg_EXPT = [], [], [], []
  with open(inpfile) as input:
    for line in input:
      try:
        data = [ item.strip() for item in line.split() ]
        if len(data) < 9:  #vis. data for mutation is incomplete...
            continue
        else:
            ddg_run1.append(data[3]); ddg_run2.append(data[5]); ddg_run3.append(data[7])
      except:
        pass
  return ddg_run1, ddg_run2, ddg_run3
```
NOTE: If the IC50 (nM) value == 10000, then that data SHOULD NOT BE used for computing RMSE or MUE; it can be used for classification metrics (so long as the cutoff for classification is BELOW the DDG_exp value)

### `All_prime_144.dat`

Prime (MM-GBSA) results for computing impact of mutations on drug-binding.

File contains experimental DDG in the FIRST COLUMN, and the DDG for Prime is SECOND COLUMN.

If `DDG_exp == 5.08`, then EXCLUDE (this corresponds to T315I/dasatinib mutation that was above LOD of Ariad's assay) from quantitative metrics.

If `DDG_exp = 2.33`, then EXCLUDE (this corresponds to L248R/imatinib mutation that was above LOD of Ariad's assay) from quantitative metrics.

Can use these two mutations for classification metrics IF the value DDG is BELOW the cutoff.


### `all_Ki_y_IC50.dat`

Ki versus IC50 experimental data

FIRST COLUMN is IC50 data (Ariad)

SECOND COLUMN is Ki data (Davis et al.)

Note: many lines have one or no entries at all. That's just because of how the data was entered from the Excel datasheet in which ALL of the original data was organized into tables with ONE ROW for each possible mutations that are in the various datasets.


### `all_IC50.dat`

IC50 vs. IC50 data

Columns are permuted combinations of Ariad, Radaelli et al., and O'Hare et al.

Note. many lines have one or no entries at all for the reason described above for `all_Ki_y_IC50.dat`.
