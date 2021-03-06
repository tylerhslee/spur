# Overview
Research Title: New Product Diffusion  
School: New York University Leonard N. Stern School of Business  
Supervisor: Professor Masakazu Ishihara  

This research project was conducted under Stern Program for Undergraduate Research. All scripts listed in the repository have been written by myself. The purpose of the script is to run through the file system, then clean and aggregate the data into organized CSV files.

The entry point for the script is `src/main.py`. The script has only been tested and used in a UNIX environment.

## Installation
```bash
$ git clone https://github.com/tylerhslee/new_product_diffusion
$ cd new_product_diffusion/release/src
$ pip3 install -r requirements.txt
$ chmod +x main.py
$ ./main.py
```

## Data
Due to other complications, none of the actual data can be uploaded.
However, I will do my best to explain their structure and contents below.

### Consumer Data
The consumer data consists of 1023 different categories based on their `product category`, `year`, and `outlet`.

* `product category` includes 31 different kinds of products that are commonly found in grocery stores, drug stores, and mass stores.

* `year` starts from 2001 Jan. 01 to 2011 Dec. 31. Hence, there are 11 different categories.

* `outlet` includes grocery stores (GR), drug stores (DR), and mass stores (MA/MK). Any mass store data after 2007 have been marked as MK, but those names have been modified back to MA for convenience.

There are two types of data files. One is data collected from member stores, and the other is collected from member consumers. Unsurprisingly, the former contains a lot more data but the latter is necessary to access household summary data.

Each file name follows the format of either `'{category}\_{outlet}\_{first-week}\_{last-week}'` or `'{category}\_PANEL\_{outlet}\_{first-week}\_{last-week}.dat'` depending on the source. There is no store data for `MA`/`MK` (not sure why). All data files are written in human-readable csv format delimited by tabs.

Following is a sample (fake) data:


    IRI_KEY WEEK SY GE VEND  ITEM  UNITS DOLLARS  F    D PR

    000000 1114  0  0 00000   000     1     9.29 NONE 0 0
	
    111111 1114  0  1 11111 11111     4    37.16 NONE 0 0

    222222 1114  0  2 22222 22222     1     9.99 NONE 0 1

    333333 1114  0  3 33333 33333     1    16.49 NONE 0 0

    444444 1114  0  4 44444   444     2     4.98 NONE 0 0

    555555 1114  0  5 55555   555     2    18.58 NONE 0 0


### Product Data
Product Data are only categorized into different years and product categories. There are total of 93 different files.

* The range of the `year` is the same as the consumer data, except that for product data, they are grouped into *01-06*, *07*, and *08-11*.

* `product category` is the same as the consumer data.

Each file has a simple format of `'prod\_{product}.{file-extention}'`. File extention is *.xls* for any data in or before 2006 and *.xlsx* for any newer data.

Following is a sample (fake) data:

    PANID	WEEK	UNITS	OUTLET	DOLLARS	IRI_KEY	COLUPC

    0000000	1121	1	KK	4.27	0000000	00000000000

    1111111	1145	1	KK	5.47	1111111	11111111111

    2222222	1152	1	MA	10	222222	22222222222

    3333333	1139	1	MA	14.88	3333333	33333333333

    4444444	1139	1	MA	14.88	4444444	44444444444

### Directory Tree
The directory has the following structure:

    /
    ├── parsed stub files
    |   ├── prod_beer.xls  
    |   └── ...    
    ├── parsed stub files 2007
    |   ├── prod_beer.xlsx
    |   └── ...    
    ├── parsed stub files 2008-2011
    |   ├── prod11_beer.xlsx
    |   └── ...  
    ├── Year1
    |   └── External
    |       ├── beer
    |       |   ├── beer_drug_1114_1165
    |       |   ├── beer_groc_1114_1165
    |       |   ├── beer_PANEL_DR_1114_1165.dat
    |       |   ├── beer_PANEL_GR_1114_1165.dat
    |       |   └── beer_PANEL_MA_1114_1165.dat
    |       └── ...
    ├── ...
    ├── Year8
    |   ├── beer
    |   |   ├── beer_drug_1479_1530
    |   |   ├── beer_groc_1479_1530
    |   |   ├── beer_PANEL_DR_1479_1530.dat
    |   |   ├── beer_PANEL_GR_1479_1530.dat
    |   |   └── beer_PANEL_MK_1479_1530.dat
    |   └── ...
    └── ...   
