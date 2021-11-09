# multi_melt
A data wrangling tool to automatize complex series of pandas melt function calls (WIP - not functional yet!)

## What is this for?
I often have to work data-pipelines maintained by others that require files to enter in a specific format. 
The source data often starts with a suboptimal formatting in wide form and must be restructured to enter the data warehouse with a specific (somewhat esoteric) format in long form.
This requires a somewhat complex series of pandas.melt function calls. This tool is intended to automatize this process somewhat.

### Example datafile
A typical example source file would look like this:

| Uuid | Date | Weight_tracking | Country | QFOODETAILS_foo1nm | QFOODETAILS_foo1br | QFOODETAILS_foo1cid | QFOODETAILS_foo1url | QFOODETAILS_foo1ch | VQ_foobarfoo1r | VQ_foobarfoo1s1 | VQ_foobarfoo1s2 | VQ_foobarfoo1s3 | VQ_foobarfoo1s4 | VQ_foobarfoo1s5 | VQ_foobarfoo1s6 | VQ_foobarfoo1s7 | VQ_foobarfoo1s8 | VQ_foobarfoo1s9 | VQ_foobarfoo1s10 | VQ_foobarfoo1f1 | VQ_foobarfoo1f2 | VQ_foobarfoo1f3 | VQ_foobarfoo1f4 | VQ_foobarfoo1f5 | VQ_foobarfoo1f6 | VQ_foobarfoo1f7 | VQ_foobarfoo1f8 | VQ_foobarfoo1f9 | VQ_foobarfoo1f10 | VQ_foobarfoo1f11 | VQ_foobarfoo1f12 | VQ_foobarfoo1f13 | VQ_foobarfoo1f14 | VQ_foobarfoo1f15 | VQ_foobarfoo1f16 | VQ_foobarfoo1f17 | VQ_foobarfoo1f18 | VQ_foobarfoo1f19 | VQ_foobarfoo1f20 | QFOODETAILS_foo2nm | QFOODETAILS_foo2br | QFOODETAILS_foo2cid | QFOODETAILS_foo2url | QFOODETAILS_foo2ch | VQ_foobarfoo2r | VQ_foobarfoo2s1 | VQ_foobarfoo2s2 | VQ_foobarfoo2s3 | VQ_foobarfoo2s4 | VQ_foobarfoo2s5 | VQ_foobarfoo2s6 | VQ_foobarfoo2s7 | VQ_foobarfoo2s8 | VQ_foobarfoo2s9 | VQ_foobarfoo2s10 | VQ_foobarfoo2f1 | VQ_foobarfoo2f2 | VQ_foobarfoo2f3 | VQ_foobarfoo2f4 | VQ_foobarfoo2f5 | VQ_foobarfoo2f6 | VQ_foobarfoo2f7 | VQ_foobarfoo2f8 | VQ_foobarfoo2f9 | VQ_foobarfoo2f10 | VQ_foobarfoo2f11 | VQ_foobarfoo2f12 | VQ_foobarfoo2f13 | VQ_foobarfoo2f14 | VQ_foobarfoo2f15 | VQ_foobarfoo2f16 | VQ_foobarfoo2f17 | VQ_foobarfoo2f18 | VQ_foobarfoo2f19 | VQ_foobarfoo2f20 | ... | QFOODETAILS_foo15nm | QFOODETAILS_foo15br | QFOODETAILS_foo15cid | QFOODETAILS_foo15url | QFOODETAILS_foo15ch | VQ_foobarfoo15r | VQ_foobarfoo15s1 | VQ_foobarfoo15s2 | VQ_foobarfoo15s3 | VQ_foobarfoo15s4 | VQ_foobarfoo15s5 | VQ_foobarfoo15s6 | VQ_foobarfoo15s7 | VQ_foobarfoo15s8 | VQ_foobarfoo15s9 | VQ_foobarfoo15s10 | VQ_foobarfoo15f1 | VQ_foobarfoo15f2 | VQ_foobarfoo15f3 | VQ_foobarfoo15f4 | VQ_foobarfoo15f5 | VQ_foobarfoo15f6 | VQ_foobarfoo15f7 | VQ_foobarfoo15f8 | VQ_foobarfoo15f9 | VQ_foobarfoo15f10 | VQ_foobarfoo15f11 | VQ_foobarfoo15f12 | VQ_foobarfoo15f13 | VQ_foobarfoo15f14 | VQ_foobarfoo15f15 | VQ_foobarfoo15f16 | VQ_foobarfoo15f17 | VQ_foobarfoo15f18 | VQ_foobarfoo15f19 | VQ_foobarfoo15f20 | QFOODETAILSBARnm | QFOODETAILSBARbr | QFOODETAILSBARcid | QFOODETAILSBARurl | QFOODETAILSBARch | VQ_foobarbarfoosBARr | VQ_foobarbarfoosBARs1 | VQ_foobarbarfoosBARs2 | VQ_foobarbarfoosBARs3 | VQ_foobarbarfoosBARs4 | VQ_foobarbarfoosBARs5 | VQ_foobarbarfoosBARf1 | VQ_foobarbarfoosBARf2 | VQ_foobarbarfoosBARf3 | VQ_foobarbarfoosBARf4 | VQ_foobarbarfoosBARf5 | VQ_foobarbarfoosBARf6 | VQ_foobarbarfoosBARf7 | VQ_foobarbarfoosBARf8 | VQ_foobarbarfoosBARf9 | VQ_foobarbarfoosBARf10 | VQ_foobarbarfoosBARf11 | VQ_foobarbarfoosBARf12 | VQ_foobarbarfoosBARf13 | VQ_foobarbarfoosBARf14 | VQ_foobarbarfoosBARf15 | VQ_foobarbarfoosBARf16 | VQ_foobarbarfoosBARf17 | VQ_foobarbarfoosBARf18 | VQ_foobarbarfoosBARf19 | VQ_foobarbarfoosBARf20 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |--- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 6z36r8mzkgrsmat1 | 9/27/2021 | 0,809052632 | Süd | tukmiKqSod | NVfk | lYYU | kSED | TV | 1 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | RKPh | mKZj | AnTP | MMWU | TV | 1 | 1 | 1 | 0 | 1 | 1 | 1 | 1 | 0 | 1 | 1 |  |  |  |  |  |  |  |  | 1 | 1 |  |  |  |  |  |  |  |  |  | 1 | ... | |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | ozzb | ghxs | gxeu | tbbd | var | 1 | 1 | 0 | 0 | 1 | 0 |  |  |  |  |  |  | 1 | 1 | 1 |  |  |  |  |  |  |  |  |  |  | |
| thbqg2kdasv4vgw1 | 9/27/2021 | 0,7756 | Nord | tukmiKqSod | NVfk | lYYU | kSED | TV | 1 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | RKPh | mKZj | AnTP | MMWU | TV | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |  |  |  |  |  |  |  |  | 1 | 1 |  |  |  |  |  |  |  |  |  | 1 | ... | |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | ozzb | ghxs | gxeu | tbbd | var | 1 | 1 | 1 | 0 | 1 | 1 |  |  |  |  |  |  | 1 | 1 | 1 |  |  |  |  |  |  |  |  |  |  | |

This file then has to be restructured the following way:

| Uuid | Date | Weight_tracking | Country | QFOODETAILS_foo1nm | QFOODETAILS_foo1br | QFOODETAILS_foo1cid | QFOODETAILS_foo1url | QFOODETAILS_foo1ch | VQ_foobarfoo1r | VQ_foobarfoo1s1 | VQ_foobarfoo1s2 | VQ_foobarfoo1s3 | VQ_foobarfoo1s4 | VQ_foobarfoo1s5 | VQ_foobarfoo1s6 | VQ_foobarfoo1s7 | VQ_foobarfoo1s8 | VQ_foobarfoo1s9 | VQ_foobarfoo1s10 | VQ_foobarfoo1f1 | VQ_foobarfoo1f2 | VQ_foobarfoo1f3 | VQ_foobarfoo1f4 | VQ_foobarfoo1f5 | VQ_foobarfoo1f6 | VQ_foobarfoo1f7 | VQ_foobarfoo1f8 | VQ_foobarfoo1f9 | VQ_foobarfoo1f10 | VQ_foobarfoo1f11 | VQ_foobarfoo1f12 | VQ_foobarfoo1f13 | VQ_foobarfoo1f14 | VQ_foobarfoo1f15 | VQ_foobarfoo1f16 | VQ_foobarfoo1f17 | VQ_foobarfoo1f18 | VQ_foobarfoo1f19 | VQ_foobarfoo1f20 | VQ_foobarbarfoosBARs1 | VQ_foobarbarfoosBARs2 | VQ_foobarbarfoosBARs3 | VQ_foobarbarfoosBARs4 | VQ_foobarbarfoosBARs5 | VQ_foobarbarfoosBARf1 | VQ_foobarbarfoosBARf2 | VQ_foobarbarfoosBARf3 | VQ_foobarbarfoosBARf4 | VQ_foobarbarfoosBARf5 | VQ_foobarbarfoosBARf6 | VQ_foobarbarfoosBARf7 | VQ_foobarbarfoosBARf8 | VQ_foobarbarfoosBARf9 | VQ_foobarbarfoosBARf10 | VQ_foobarbarfoosBARf11 | VQ_foobarbarfoosBARf12 | VQ_foobarbarfoosBARf13 | VQ_foobarbarfoosBARf14 | VQ_foobarbarfoosBARf15 | VQ_foobarbarfoosBARf16 | VQ_foobarbarfoosBARf17 | VQ_foobarbarfoosBARf18 | VQ_foobarbarfoosBARf19 | VQ_foobarbarfoosBARf20 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 6z36r8mzkgrsmat1 | 9/27/2021 | 0,809052632 | Süd | tukmiKqSod | NVfk | lYYU | kSED | TV | 1 |
| 6z36r8mzkgrsmat1 | 9/27/2021 | 0,809052632 | Süd | RKPh | mKZj | AnTP | MMWU | TV | 1 | 1 | 1 | 0 | 1 | 1 | 1 | 1 | 0 | 1 | 1 |
| 6z36r8mzkgrsmat1 | 9/27/2021 | 0,809052632 | Süd | ozzb | ghxs | gxeu | tbbd | var | 1 | | | | | | | | | | |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | 1 | 1 | 0 | 0 | 1 | 0 |  |  |  |  |  |  | 1 | 1 | 1 |
| thbqg2kdasv4vgw1 | 9/27/2021 | 0,7756 | Nord | tukmiKqSod | NVfk | lYYU | kSED | TV | 1 |
| thbqg2kdasv4vgw1 | 9/27/2021 | 0,7756 | Nord | tukmiKqSod | NVfk | lYYU | kSED | TV | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| thbqg2kdasv4vgw1 | 9/27/2021 | 0,7756 | Nord | ozzb | ghxs | gxeu | tbbd | var | 1 | | | | | | | | | | |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | 1 | 1 | 1 | 0 | 1 | 1 |  |  |  |  |  |  | 1 | 1 | 1 |

Confusing, I know! Which is why I want to automatize this process.

What happens here is that the data is reshaped from wide to long, but in a somewhat complex way. There are a couple of fixed variable (Uuid, Date, Weight_tracking, Country), and two "groups" of variables that get reshaped. The first group are the variables from QFOODETAILS_foo1nm to VQ_foobarfoo15f20. The second group are the variables from QFOODETAILSBARnm to VQ_foobarbarfoosBARf20. Note that these variables do not simply follow the scheme _prefix + number_, but instead follow a scheme like _prefix + number + suffix_ (example: _VQ_foobarfoo + number + f1_).
