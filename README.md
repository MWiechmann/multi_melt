# multi_melt
A data wrangling tool to automatize complex series of pandas melt function calls (WIP - not functional yet!)

## What is this for?
I often have to work data-pipelines maintained by others that require files to enter in a specific format. 
The source data often starts with a suboptimal formatting and must be restructured to enter the data warehouse with a specific (somewhat esoteric) format.
This requires somewhat complex series of pandas.melt function calls. This tool is intended to automatize this process somewhat.

### Example datafile
A typical example source file would look like this:

| Uuid | Date	| Weight_tracking	| Country	| QFOODETAILS_foo1nm | QFOODETAILS_foo1br | QFOODETAILS_foo1cid | QFOODETAILS_foo1url | QFOODETAILS_foo1ch | VQ_foobarfoo1r | VQ_foobarfoo1s1	| VQ_foobarfoo1s2 | ... | VQ_foobarfoo1s10 | VQ_foobarfoo1f1 | VQ_foobarfoo1f2 | ... | VQ_foobarfoo1f20 | QFOODETAILS_foo2nm | QFOODETAILS_foo2br | QFOODETAILS_foo2cid | QFOODETAILS_foo2url | QFOODETAILS_foo2ch | VQ_foobarfoo2r | VQ_foobarfoo2s1 | VQ_foobarfoo2s2 | ... | QFOODETAILS_foo3nm | ... |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |  data |
