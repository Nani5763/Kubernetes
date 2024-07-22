################ HELM CHARTS ################

Interview they are asking did you work on Helm Charts?
A) Somecases may be yes, if you have a good knowledge you can say yes i have worked on helm charts. Otherwise i know helm charts but i have never work on helm charts but i know the process. Instead of "NO".

# Defination:-
1) Helm:- Helm helps you manage kubernetes applications-helm charts help you define, install and upgarde even the most complex kubernetes applications.
2) Charts:- Charts are easy to create ,version, share and publish- so start using helm and stop the copy-and-paste.

* How to install Helm charts

 -----helm install-----

https://github.com/helm/helm/releases

wget https://get.helm.sh/helm-v3.14.0-linux-amd64.tar.gz

tar -zxvf helm-v3.14.0-linux-amd64.tar.gz

mv linux-amd64/helm /usr/local/bin/helm

chmod 777 /usr/local/bin/helm  # give permissions 

helm version 






* Helm Chart is nothing but when ever you cam create the command
     
     * helm create <Sample_Name>

* If you can give this command. By default one project will create inside your folder structure. That Project sample application will be there.

* That sample application is like "nginx". Nginx application will run inside the "Project".

* To run the my project
  
   * helm install <First-Argument-Release-Name> <Second-Argument-Chart-Name>

* Example my Project name Helloworld means

   * helm install dev helloworld

# 1) Helm install:-
A) Helm is the command used to a install a helm chart

# 2) dev:- 
A) "dev" is the name you are giving to this particular release of the helm chart. This name can be anything you choose and is used to uniquely identify the helm release.

# 3) Helloworld:-
A) is the name of helm chart you are installing 

* How to see list of helm release list's by using
  
    * helm list -a

* We want to upgrade only the existing one instead of creating by using

    * helm upgarde dev helloworld