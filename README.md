# collecting pstacks on the main splunkd process
collecting pstacks on the main splunkd PID


1. install the collect-stacks.sh script onto the host
https://github.com/rephillips/debugging_splunk/blob/main/collect-stacks.sh

a.) cd /opt/splunk/bin
vi collect-stacks.sh


2. give the file executable permissions:

chmod +x collect-stacks.sh

3.) install elfutils (this step not required on splunk cloud ):

yum install elfutils

4.) create the output directory:

cd /tmp
mkdir splunk
the default output directory in the script is /tmp/splunk


5.) execute the script:
./collect-stacks.sh

the default script parameters are to collect a stack every .5 sec 1000 times. These defaults are sufficient.

7.) once the script finishes tar the directory created inside /tmp/splunk:
cd /tmp/splunk

tar -zcvf archive-name.tar.gz source-directory-name

note: it is normal to see .err for each .out file
move file to /tmp directory

8.) scp from cloud instance to local machine:

scp <indexer-host>:/tmp/<archive-name>.tar.gz .

9.) generate a diag once pstack collection is finished (this step not required on splunk cloud ):

$SPLUNK_HOME/bin

./splunk diag
