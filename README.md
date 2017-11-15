This repo contains an archive of the linux.conf.au 2016 website and the commands/process used to download the flat version of the site.

Here are the commands used to download and clean up the content
```bash
wget --recursive --no-clobber --page-requisites --no-parent --domains lca2016.linux.org.au https://lca2016.linux.org.au --no-check-certificate --reject-regex "(.*)\/wiki/((.*)\?(.*)|Special\:.*)"
for file in $(find -name "*\?*"); do mv "$file" "${file%%\?*}"; done
find * -type f -exec sed -iE 's/"https:\/\/lca2016\.linux\.org\.au/"/g' {} \;
find * -type f -exec sed -iE 's/"http:\/\/lca2016\.linux\.org\.au/"/g' {} \;
find * -type f -exec sed -iE 's/"https:\/\/linux\.conf\.au/"/g' {} \;
find * -type f -exec sed -iE 's/"http:\/\/linux\.conf\.au/"/g' {} \;
find * -type f -exec sed -iE 's/href=""/href="\/"/g' {} \;
find * -type f -exec sed -iE 's/https:\/\/linux\.conf\.au/https:\/\/lca2016\.linux\.org\.au/g' {} \;
find * -type f -exec sed -iE 's/http:\/\/linux\.conf\.au/https:\/\/lca2016\.linux\.org\.au/g' {} \;
```

Review the changes made (using `git diff`, for example) as some changes may not have been intended!

(if you find you suddenly have a bunch of files with names ending in various numbers of 'E' use this command to clear them out `find . -name '*E' -exec rm {} +`)
