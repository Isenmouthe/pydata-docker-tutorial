# Setting up a Dev Environment

When working on a python project, a common way that people will manage their dependencies is running `pip freeze > requirements.txt` and coupling that with `virtualenv` to manage project level dependencies.

Often, when reproducing somebody else's analysis, it is not enough to run `pip install -r requirements.txt` in the repository.  

However, sometimes there are configurations that are specific system level dependencies that are not captured. As I go along with developing my code, I will install system-level dependencies as required by the package.  

To be able to replicate all the system level dependencies, you can see how Docker could easily be used! 

Now we move to the next stage, which is figuring out how to layer instructions, and put together a Dockerfile to set up a docker container with your exact specifications to replicate your results. 

In the past few weeks, we have observed the following issues: 
1. Somebody builds a tool in a different flavour of python with several package changes 
2. Having pandas 0.20 on one machine and pandas 0.21 on another can change how the metrics are calculated slightly
3. Struggling to manage `virtualenvs` for different packages, broken `virtualenvs`

The use case we will explore here, is setting up a python machine with all the tools required for a project, and then setting up a jupyter notebook server within to access all those resources: 

So, first navigate into the folder, where all the neccesary files are located and in the terminal run:
```console
docker build -t devenv .
```

In my case:
```console
C:\Users\...\pydata-docker-tutorial\02 - dev-env>docker build -t devenv .
```
Generated output:
```console
[+] Building 263.7s (13/13) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                   0.1s
 => => transferring dockerfile: 494B                                                                                                                   0.0s
 => [internal] load .dockerignore                                                                                                                      0.1s
 => => transferring context: 2B                                                                                                                        0.0s
 => [internal] load metadata for docker.io/library/python:3                                                                                            5.7s
 => [auth] library/python:pull token for registry-1.docker.io                                                                                          0.0s
 => [1/7] FROM docker.io/library/python:3@sha256:10fc14aa6ae69f69e4c953cffd9b0964843d8c163950491d2138af891377bc1d                                    149.8s
 => => resolve docker.io/library/python:3@sha256:10fc14aa6ae69f69e4c953cffd9b0964843d8c163950491d2138af891377bc1d                                      0.0s
 => => sha256:3f53d697b58165ec41a16cdc5f9e29a32ab2695688488862694be0155137446e 2.22kB / 2.22kB                                                         0.0s
 => => sha256:ee4e7a0f1c354d9996229a765d0785df2671252c1822ae111015d37dcf5f765b 8.52kB / 8.52kB                                                         0.0s
 => => sha256:a8ca11554fce00d9177da2d76307bdc06df7faeb84529755c648ac4886192ed1 55.04MB / 55.04MB                                                      75.8s
 => => sha256:10fc14aa6ae69f69e4c953cffd9b0964843d8c163950491d2138af891377bc1d 2.14kB / 2.14kB                                                         0.0s
 => => sha256:e4e46864aba2e62ba7c75965e4aa33ec856ee1b1074dda6b478101c577b63abd 5.16MB / 5.16MB                                                        10.0s
 => => sha256:c85a0be79bfba309d1f05dc40b447aa82b604593531fed1e7e12e4bef63483a5 10.88MB / 10.88MB                                                      18.4s
 => => sha256:195ea6a58ca87a18477965a6e6a8623112bde82c5b568a29c56ce4581b6e6695 54.59MB / 54.59MB                                                      76.4s
 => => sha256:157f16ed0a0c119e5015d22d95fd158bf9e85654611b870b79cca3987442948b 196.87MB / 196.87MB                                                   139.9s
 => => sha256:884b144bec286b456b1cd694ccd6adc07c3619b3b84069c4ec575fe213e94a7e 6.29MB / 6.29MB                                                        83.7s
 => => sha256:1c469643b609009ff435b3ba0e22f7acdad34837547c33ab301eeaa7993a6ef1 23.25MB / 23.25MB                                                      94.4s
 => => extracting sha256:a8ca11554fce00d9177da2d76307bdc06df7faeb84529755c648ac4886192ed1                                                              3.9s
 => => extracting sha256:e4e46864aba2e62ba7c75965e4aa33ec856ee1b1074dda6b478101c577b63abd                                                              0.5s
 => => extracting sha256:c85a0be79bfba309d1f05dc40b447aa82b604593531fed1e7e12e4bef63483a5                                                              0.7s
 => => extracting sha256:195ea6a58ca87a18477965a6e6a8623112bde82c5b568a29c56ce4581b6e6695                                                              4.7s
 => => sha256:4c0ac982aa8993dae4217bebcb9bd25cd97047488572ca84795be03483457208 232B / 232B                                                            84.1s
 => => sha256:049db2c7eb8a5bd3833cac2f58c6c72b481f1a0288a8b20527529c4970b52762 3.06MB / 3.06MB                                                        86.7s
 => => extracting sha256:157f16ed0a0c119e5015d22d95fd158bf9e85654611b870b79cca3987442948b                                                              7.3s
 => => extracting sha256:884b144bec286b456b1cd694ccd6adc07c3619b3b84069c4ec575fe213e94a7e                                                              0.3s
 => => extracting sha256:1c469643b609009ff435b3ba0e22f7acdad34837547c33ab301eeaa7993a6ef1                                                              0.8s
 => => extracting sha256:4c0ac982aa8993dae4217bebcb9bd25cd97047488572ca84795be03483457208                                                              0.0s
 => => extracting sha256:049db2c7eb8a5bd3833cac2f58c6c72b481f1a0288a8b20527529c4970b52762                                                              0.3s
 => [internal] load build context                                                                                                                      0.0s
 => => transferring context: 155B                                                                                                                      0.0s
 => [2/7] RUN apt-get update && apt-get install -y python3-pip                                                                                        18.3s
 => [3/7] COPY requirements.txt .                                                                                                                      0.1s
 => [4/7] RUN pip install -r requirements.txt                                                                                                         39.3s
 => [5/7] RUN pip3 install jupyter                                                                                                                    46.6s
 => [6/7] RUN useradd -ms /bin/bash demo                                                                                                               0.8s
 => [7/7] WORKDIR /home/demo                                                                                                                           0.1s
 => exporting to image                                                                                                                                 2.8s
 => => exporting layers                                                                                                                                2.8s
 => => writing image sha256:8f3938a3c7d629f9ee72d545cdcee9cabafbf5dfabaf7ff6c2763bc52996a7e8                                                           0.0s
 => => naming to docker.io/library/devenv                                                                                                              0.0s

Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
```

This should set up a jupyter notebook that you will be able to access with all the tools in the `requirements.txt` file installed. 

```console
docker run -p 8888:8888 devenv
```
If you face such error:
```console
C:\Users\...\pydata-docker-tutorial\02 - dev-env>docker run -p 8888:8888 devev
Unable to find image 'devev:latest' locally
docker: Error response from daemon: pull access denied for devev, repository does not exist or may require 'docker login': denied: requested access to the resource is denied.
See 'docker run --help'.
```
Try to login, using your dockerhub credentials
```console
docker login -u your_username
Password: your_password
```

Now access it from your machine, try `localhost:8888`. It will ask you to copy and paste the token you were given.



