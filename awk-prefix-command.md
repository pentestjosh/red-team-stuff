# Awk command to append "prefix" to each line of file 
````
awk '$0="prefix"$0' file > new_file
```
# Append http:// to a list of IPs
awk '$0="http://"$0' file > new_file


