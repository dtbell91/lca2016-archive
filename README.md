This repo contains an archive of the linux.conf.au 2016 website and the commands/process used to download the flat version of the site.

Here are the commands used to download and clean up the content
```bash
wget --recursive --no-clobber --page-requisites --no-parent --domains lca2016.linux.org.au https://lca2016.linux.org.au --no-check-certificate --reject-regex "(.*)\/wiki/((.*)\?(.*)|Special\:.*)"
for file in $(find -name "*\?*"); do mv "$file" "${file%%\?*}"; done

```
