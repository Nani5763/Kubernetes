#                 ######Trivy######

* Trivy scans local and remote container images, supports multiple container engines, as well as archived  and extracted images. It works on raw filesystem and remote git repositories. With Trivy, you can scan whenever and wherever you need to.

* Trivy is a scanner of image to give the vulnerabilities.
* First Install Trivy
    * wget rpm -ivh https://github.com/aquasecurity/trivy/releases/download/v0.48.3/trivy_0.48.3_Linux-64bit.rpm
* To check the Trivy version
    * trivy --version
* To scan the Image means 
    * trivy image <Image Name>
* How to image was converted into json format
    * trivy image --format json -o <filename.json><imagename>
* If you want to see the jq format
    * jq.<filename.json> After json format we will use this.