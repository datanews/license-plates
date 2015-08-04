# NY personalized license plates

Data on New York personalized license plate applications received from the New York DMV in response to a July 2014 FOIL request.  Covers applications from 10/1/2010 to 9/26/2014.

[Learn about NY personalized plates](http://dmv.ny.gov/learn-about-personalized-plates)

## Contents

* `accepted-plates.csv`: CSV of plate applications that were accepted and issued, with order date and plate configuration.
* `rejected-plates.csv`: CSV of plate applications that were rejected by the department, with order date and plate configuration.

## Notes

* This data may contain explicit or offensive language.
* Plate configurations in `accepted-plates.csv` may have since been revoked by the DMV.
* Plate configurations in `rejected-plates.csv` were rejected by the department. It does not include plates that were reserved, banned by the Red Guide, or cancelled for administrative reasons.
* Some plate configurations may exist in multiple applications.
* A small number of rows may contain erroneous data because of Excel cell formatting in the original prepared files.

## Processing

The original files were in Microsoft Excel format.  They have been converted to CSV (comma-separated values) file for more broad use. The following commands were used to process:

```
in2csv "original/Copy of NYS DMV Personalized Plate Orders October 1 2010 through September 26 2014 (duplicates highlighted).xlsx" | sed -e '1s/Date Personalized Plate was Ordered/date/' -e '1s/Personalized Plate Configuration Requested/plate/' | csvcut -x | csvsort -c "date" > rejected-plates.csv > accepted-plates.csv && \
in2csv "original/Copy of NYS DMV Rejected Personalized Plate Orders October 1 2010 through September 26 2014 (response - 2014-6130).xlsx" | sed -e '1s/       Date Personalized Plate was Ordered/date/' -e '1s/        Personalized Plate Configuration Requested and Denied/plate/' | csvcut -x | csvsort -c "date" > rejected-plates.csv && \
csvstat accepted-plates.csv && csvstat rejected-plates.csv;
```
