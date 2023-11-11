# Assignment-4

**This assignment was performed based on the following procedures.**

First of all, I have imported all the necessary packages to use the functions.

Then, I have generated the credentials using SOURCE COOPERATIVE [<https://beta.source.coop/repositories/vida/google-microsoft-open-buildings/download/>] and created variables have the values that is corresponding to each of the credentials. *Remember the AWS_SESSION_TOKEN only works for five hours.*

The major credential are:

```         
aws_region 
Aws_Access_key_Id 
Aws_Secret_Access_Key 
Aws_Session_Token
```

I get the country ISO standard country code from the [<https://www.iso.org/obp/ui>]. which is **'HTI'**

Then, Create a client for Simple Storage Service (s3) access. For this you have to import _boto3_ package. The aformentioned credentials are used in this section to access the AWS bucket.

After that, I have used a function to automate the process of getting the keys for specific country, aws region using the given soucre cooperative credential.

The next process is to downloading the geoparquet file of Haiti,using *download_file()* function, which have the build footprints data originated by Microsoft and Google.

Again, one next function was wrote to read the geoparquet file that was downloaded in upper mentioned step. _read_geoparquet(file)_

_len(gp)_ function was used to count the build footprints originated by both sources.

_gp.crs_ function was used to check or print the coordinate reference system of the geoparquet data.

_gp=gp.to_crs(32618)_ was used to project the geographic coordinate. Haiti lies in _UTM Zone 18N_ which is denoted as _EPSG:32618_ in EPSG standard. 

_gp[g['bf_source]=='microsoft']_ and _gp[g['bf_source]=='google']_ was used to sliced the data according the defined categorical value. i.e. microsoft and google.

_.head()_ used to print the result in tabula view for both sliced data.

_plt.hist()_ is the function, under the _matplotlib_ package, used to plot histogram of the area of all building provided by mocrosoft as the source.

_all_intersect_bf=gp.sjoin(gp, predicate='intersects', how="inner").compute()_ is used to get the number of building footprints that intersects with each other regardless of sources.

_ggl_intersect_ggl=ggl_bf.sjoin(ggl_bf, predicate="intersects", how="inner").compute()_ is used to get the number of google building footprints intersect another google building footprints.

_ms_intersect_ms=ms_bf.sjoin(ms_bf, predicate='intersects', how="inner").compute()_ is used to get the number of microsoft building footprints intersect another microsoft building footprints.

_ggl_intersect_ms=ggl_bf.sjoin(ms_bf, predicate='intersects', how='inner').compute()_ is used to get the number of google building footprints intersecting with microsoft building footprints.





