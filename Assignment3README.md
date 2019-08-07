# Using auto-builds and deploying the app

I used two services for auto-builds:
1. Travis-CI
2. Google Cloud Build

For the app deployment, I used Google Cloud Platform.

# Travis-CI

To use [Travis-CI](https://travis-ci.com/), I first installed it on my github repositories. After that, I used the [tutorials and documentation](https://docs.travis-ci.com/user/languages/python/) provided on the Travis-CI website as well as some outside research to build my .travis.yml file that is required for the build. 

**troubleshooting logs**
* I had trouble with my repo not showing up on Travis-CI. After a lot of time researching this problem I was unable to find the reason it wasn't showing up, so I ended up creating a new repository for my app which did show up.
* I got an error early on regarding the `script` command in the .travis.yaml file. I had to edit that to reflect the name of my main.py file. 

## Google Cloud Build

I utilized Google's [cloud build](https://cloud.google.com/cloud-build/?utm_source=google&utm_medium=cpc&utm_campaign=na-CA-all-en-dr-bkws-all-all-trial-b-dr-1007179&utm_content=text-ad-none-any-DEV_c-CRE_339578529269-ADGP_Hybrid+%7C+AW+SEM+%7C+BKWS+%7C+RLSA+%7C+CA+%7C+en+%7C+BMM+~+Tools+~+Cloud+Build+~+Google+Cloud+Build-KWID_43700042240939425-kwd-471794159726&utm_term=KW_%2Bgoogle%20%2Bcloud%20%2Bbuild-ST_%2BGoogle+%2BCloud+%2BBuild&gclid=EAIaIQobChMItq-oz6Lx4wIVTV8NCh0IIAHcEAAYASAAEgIXUfD_BwE) which required creating a cloudbuild.yaml file as well as a dockerfile. 
I first installed cloud build on my github repositories so that it would trigger a new build on every git push. Then  I read the documentation extensively as well as doing other research on stackexchange and github to learn how to put together a dockerfile as well as the proper steps required in the cloudbuild.yaml file. 

The cloudbuild.yaml file instructs Google Cloud Build exactly what steps to take in creating the build. My cloudbuild.yaml file simply instructs Google Cloud Build to run the dockerfile.

The dockerfile contains instructions on what commands to run in the cloud shell. My docker file contains instructions for Google Cloud Build to create a virtual environment, install the app requirements from the requirments.txt file, and run the app from the main.py file. A succesful build means that the file ran succesfully, and the app works. 

Please see comments in the cloudapp.yaml and dockerfile respectively for more details on their contents. 

**troubleshooting logs**
* I don't remember the exact errors I had to troublshoot, but this took a lot of trial and error, a lot of small edits to the yaml and dockerfiles, and a lot of research.
## Google App Deployment

Looking through [google's documentation](https://cloud.google.com/appengine/docs/standard/python3/config/appref) I found the information on how to structure the required app.yaml file for deployment. Once I added the file to the repository, I used Google Cloud Platform to create an App in the App Engine. There was a quick tutorial I went through to understand how to create the app on google's cloud platform and subsequently use google cloud shell to run it locally. Ultimately I used google cloud shell to deploy the app.

My app can be found at: [https://cisc3140-248419.appspot.com/index](https://cisc3140-248419.appspot.com/index)

This can be replicated as follows:
1. Create an app in Google Cloud Platform's App Engine
2. Launch Google's cloud shell. 
3. Input the following commands:
> $ git clone https://github.com/chalshaff12/cisc3140python2.git
> $ cd cisc3140python2
> $ virtualenv --python python3 ~/envs/venv
> $ source ~/envs/venv/bin/activate
> $ pip install -r requirements.txt
4. Make sure the app works locally by running the following command and using the web-preview button to open the app on your local host:
> $ flask run
5. To deploy the app, run the following command:
> $ gcloud app deploy

After the app is deployed, you will see the url that it is now hosted on.

**troubleshooting logs**
* I had trouble with python3 code triggering syntax errors. After learning that Google Cloud Platform runs on Python 2 I had to edit my code to remove string formats etc, to simple concats. 


