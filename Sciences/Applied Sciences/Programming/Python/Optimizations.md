
# Sorted Index in a DF
#optimizations #python #pandas #database #index

A problem case scenario: We have a reservations dataframe which contains the reservation creation date column `cr_date`, the check-in/out date columns: `ci_date`, and `co_date`, and a `#rooms` column. Required: we have certain target days stored in a list: `tds`, and for each target day, we want to find the number of occupied rooms for that day. For example, if `tds=['2023-01-01', '2023-01-02']`, and the dataframe looks like this:

| `cr_date` | `ci_date` | `co_date` | `#rooms` |
| ---- | ---- | ---- | ---- |
| 2022-06-01 | 2022-12-30 | 2023-01-02 | 2 |
| 2022-06-01 | 2022-12-31 | 2023-01-03 | 3 |
| 2022-06-02 | 2023-01-01 | 2023-01-04 | 1 |
| 2022-06-03 | 2023-01-02 | 2023-01-05 | 4 |
| 2022-06-03 | 2023-01-03 | 2023-01-06 | 2 |
such that:
- The first row indicates that 2 rooms are occupied from December 30, 2022 (inclusive), to January 2, 2023 (exclusive).
- The second row shows 3 rooms occupied from December 31, 2022 (inclusive), to January 3, 2023 (exclusive), and so on.

Then, we can see that the aggregated `#rooms` for `'2023-01-01', '2023-01-02'` are `2+3=5` and `3+1+4=8` respectively. Again, the `co_date` is exclusive, so we count until the day before it as an included target day.

Required: Perform the aggregation done above on all of `tds`.

## Solution Using Matrix (Slowest)

initial solution logic: code that will create a matrix dataframe such that the columns represent the values in `tds` and the index represents the unique values in `cr_date`, such that `cell_ij` represents the aggregated rooms which were reserved in the i<sup>th</sup> date to occupy these rooms on the j<sup>th</sup> target day. So for the previous example, said matrix will look like this:

|`cr_date`|`2023-01-01`|`2023-01-02`|
|---|---|---|
|2022-06-01|5|3|
|2022-06-02|1|1|
|2022-06-03|0|4|

Now, we'll use pandas' `melt` function to convert the matrix above to the following shape:

|`cr_date`|`Target Day`|`Total Reserved Rooms` |
|---|---|---|
|2022-06-01|2023-01-01|5|
|2022-06-01|2023-01-02|3|
|2022-06-02|2023-01-01|1|
|2022-06-02|2023-01-02|1|
|2022-06-03|2023-01-01|0|
|2022-06-03|2023-01-02|4|


## Solution Using Boolean Indexing

TODO: mention how the example above is solved using this logic:

```python
unique_hyears = df['rcr_hdate'].apply(lambda x: x.year).unique()
unique_hyears.sort()
target_gdates = pd.Series()
for hyear in unique_hyears:
    # hts and hte mean hijri target start and hijri target end
    # while "g" refers to gregorian
    hts_m, hts_d = SHARED_GLOBALS["TARGET_START_DAY_HIJRI"].month, SHARED_GLOBALS["TARGET_START_DAY_HIJRI"].day
    hte_m, hte_d = SHARED_GLOBALS["TARGET_END_DAY_HIJRI"].month, SHARED_GLOBALS["TARGET_END_DAY_HIJRI"].day
    is_diff_hyear = SHARED_GLOBALS["IS_DIFFERENT_YEAR"]
    hts = Hijri(hyear, hts_m, hts_d)
    hte = Hijri(hyear+is_diff_hyear, hte_m, hte_d)
    gts, gte = hijri_to_greg(hts), hijri_to_greg(hte)
    gt_range = pd.date_range(gts, gte, inclusive='left').to_series()
    target_gdates = target_gdates.append(gt_range)

daily_target_dates_melted_df = pd.DataFrame()
for gtd in target_gdates:
    gtd_res_df = df2[(df2['rci_gdate']<=gtd) & (df2['rco_gdate']>gtd)]
    gtd_res_df['target_gdate'] = gtd
    daily_target_dates_melted_df = daily_target_dates_melted_df.append(gtd_res_df)
daily_target_dates_melted_df.reset_index(inplace=True, drop=True)
daily_target_dates_melted_df
```

## Solution Using Lex-Sorted MultiIndex Slicing

Introductory note: By default, we should make sure a multiIndexed dataframe is lex-sorted. More details [here](https://tedboy.github.io/pandas/advanced/advanced3.html) and [here](https://stackoverflow.com/questions/54261500/how-to-avoid-sorting-when-indexing-pandas-multiindex). Caveat: lexicographical sorting is applied to string-like indices of your multiindex. Consequently, a number-like index will be numerically sorted, not lexicographically sorted (i.e., not like [this SO answer](https://stackoverflow.com/questions/45950646/what-is-lexicographical-order#:~:text=lexicographical%20order%20is%20alphabetical,2%20in%20%22alphabetical%22%20order.)).

TODO: explain the solution to the previously stated example using this code:

```python
# Create indexes on 'rci_gdate' and 'rco_gdate'
# note: "mi" means multi-index that will be lexsorted for easy slicing later on
mi_res_df = res_df.set_index(['rci_gdate', 'rco_gdate']).sort_index()

# Disable pandas UserWarning; as it says the multi-indexed df has duplicate values, 
# which doesn't matter to us, as we're just interested in getting all the reservation rows 
# where the current target day `gtd` is between the check-in and check-out (exclusive) dates
warnings.filterwarnings("ignore", category=UserWarning)

# Initialize an empty list to store the filtered DataFrames
filtered_dfs = []

# Iterate over each target date
for gtd in tqdm(target_gdates, total=len(target_gdates)):
    
    # Use index slicing for 'rci_gdate' and boolean masking for 'rco_gdate'
    # note: the .loc indexer is inclusive by default, so that's why
    # ":gtd" refers to "check-in less than or equal to gtd" and 
    # "gtd + pd.Timedelta(days=1):" refers to "greater than gtd"
    td_between_ci_co_slice_cond = pd.IndexSlice[:gtd, gtd + pd.Timedelta(days=1):]
    # reset_index() is to bring 'rci_gdate' and 'rco_gdate' back as columns
    gtd_res_df = mi_res_df.loc[td_between_ci_co_slice_cond, :].reset_index() 

    # Assign the target date as a column
    gtd_res_df['target_gdate'] = gtd
    # Append the result to the list of dfs
    filtered_dfs.append(gtd_res_df)

# Concatenate all the filtered dfs into one
dtd_df1 = pd.concat(filtered_dfs, ignore_index=True)

# Enable pandas UserWarning
warnings.filterwarnings("default", category=UserWarning)

```

