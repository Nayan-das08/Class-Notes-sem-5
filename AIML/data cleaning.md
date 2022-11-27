>Chapter - [[_AIML]]

#Unlinked 
Aug 22, 2022
Topics - 

# Standardize values
## remove outliers
remove high and low values that affects the result of analysis
eg:

| temp | date |
| ---- | ---- |
| 35   | 18/6 |
| 35.6 | 19/6 | 
| 28.9 | 20/6 |
| -10.5 | 21/6 |
data which stands out from the rest
example - last row having temp -10.5


## scaled value is required
the data for an attribute must be in the common scale
eg: GPA and CGPA are two different scales of final grades 

## precision
for better presentation of data (4.5312 ~ 4.53)

## unit
ensure all observations under a variable have common unit
eg: MKS to CGS

## clean text
remove extra characters such as common prefix, postfix, multiple spaces

there are various cases that variable values may take - upper, lower, etc.

---
# format
follow a standard format

## fix invalid values
### convert incorrect datatypes
- eg: when numeric values are stored as strings, they need to be converted into strings, operations can not be done on the values of the variable
- common conversions
	- string to integer
	- string to date
	- number to string (pincode)

### correct values that go beyond range
if some of the values are beyond logical range (eg: temp < -276 degrees C), that must be corrected

### correct values that don't belong 
remove values that don't belong to a list, eg: in a dataset containing blood group of individual, E and F would be invalid and must be removed

### correct wrong structure - 
values that don't follow a defined structure, eg: a pin code of 12 digit would be invalid value and must be removed, phone no of 12 digits.

## validate internal rules
if there are internal rules such as date of delivery must be after date of order

---
# filtering data
- remove duplicate data
- remove identical rows
- filter rows
- filter by segment 
- filter by date period
- filter columns 
- aggregate data - group by required keys

---
# types of variables
categorical variables and numeric variables






>[!NOTE]
>when a signal is predicted in terms of time - Conti and discrete
>when a signal is predicted in terms of amplitude - Analog and digital
>finite number of states -> Analog, infinite -> digital




