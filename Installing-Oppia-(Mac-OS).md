**Note:** If you just want to create and share explorations, you may be able to use the hosted server at https://www.oppia.org (in which case you don't need to install anything).

*These installation instructions were last tested on 3 Dec 2018. For more information on issues that may occasionally arise with the installation process, please see the [[Troubleshooting|Troubleshooting]] page. Thanks to Varun Tandon for updating these instructions!*

**Note:** Be careful about trying to install Oppia if you have the Python [Anaconda platform](https://www.anaconda.com/) installed. We've received a bunch of reports that installation is tricky in that environment (there are lots of small things that get in the way), and that the solution is to use the standard python installation (via e.g. homebrew) instead.

**Before starting these instructions, you should complete the [[Installing Oppia page|Installing-Oppia]].**

## Note: Mac with M1 chips ##

1. [Install](https://stackoverflow.com/a/64883440) Rosetta 2

2. Inside Rosetta perform the Downloading and prerequisites steps (**Note:** If `sudo easy_install pyyaml` does not work try using `pip3 install pyyaml`).

3. Open the Rosetta terminal and run `python -m scripts.start`

## Prerequisites ##

Oppia relies on a number of programs and third-party libraries. Many of these libraries are downloaded automatically for you when you first run the `start.py` script provided with Oppia. However, there are some things that you will need to do beforehand:

1. Ensure that you have [Python 2.7](http://www.python.org/download/releases/2.7/) installed (Note: you can check this by running `python --version`). If Python 2.7 is not installed, download and run the latest Python 2.7 installer from https://www.python.org/downloads/mac-osx/. Make sure you download an installer for Python 2 and not Python 3!


1. Check if you have git installed:

   ```console
   $ git --version
   git version 2.24.3 (Apple Git-128)
   ```

   If you get a `command not found` error, then you need to install git. Download [git](http://git-scm.com/download/mac), then run the package and follow instructions. This allows you to store the source in version control.

1. Set up a virtual environment (virtualenv) for your Oppia dependencies. This ensures that conflicting versions of Python, pip, or any Python modules on your machine do not result in installation issues.

    In the `opensource/` folder (**note**: this is the **parent directory** of oppia/) run:

    ```
    pip2 install virtualenv
    python2 -m virtualenv env
    ```

    This creates a Python 2 virtual environment named "env" in your `opensource/` directory. Now, anytime you need to work with the Oppia code base, you should activate the virtualenv in `opensource/` by running

    ```
    source env/bin/activate
    ```

    If this is successful, the usual `YOURMACBOOK-NAME:directory$` at the start of the terminal line will be replaced with `(env) YOURMACBOOK-NAME:directory$`

    The following steps of installation and running the development server should all be done within this virtual environment to ensure compatibility.

    **Troubleshooting**: If, after running the `pip2 install virtualenv` command, you encounter a **'pip2 not found error'**, then do the following ([reference](https://pip.pypa.io/en/stable/installing/)):

    * Run the following command in the terminal: `curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py`. This command downloads the get-pip.py file.

    * In the same folder where you ran the above command, run: `python get-pip.py`.

    * If, after running the above command you get a warning about the directory not being added to PATH, you can add the suggested directory to the PATH by running: `sudo nano /etc/paths` and adding the suggested path at the bottom of the /etc/paths file (e.g. /Users/{{SYSTEM USERNAME}}/Library/Python/2.7/bin).

    **Note**: If you get errors while setting up virtual environment and running a development server works fine without a virtual environment (there are no conflicts with versions of python, pip or other python modules), you can safely skip the virtual environment setup. Also, if you use another tool to manage your Python environments like pipenv or pyenv, those should work too.

1. After activating the virtual environment, install setuptools (which is needed to install coverage, which checks test coverage for the Python code) and pyyaml (which is needed to parse YAML files).

   ```console
   pip install setuptools pyyaml
   ```

## Running Oppia on a development server ##

1. In a terminal, navigate to `oppia/` and run:

   ```console
   python -m scripts.start
   ```

   <details>
   <summary>Example output</summary>
   ```text
   Checking if node.js is installed in /opensource/oppia/../oppia_tools
   Installing Node.js
   Checking if yarn is installed in /opensource/oppia/../oppia_tools
   Removing package-lock.json
   Installing yarn

   WARNING: Please note that Oppia uses Yarn to manage node packages

   do *NOT* use npm. For more information on how to use yarn,

   visit https://yarnpkg.com/en/docs/usage.

   Environment setup completed.
   Checking whether google-cloud-sdk is installed in /opensource/oppia_tools/google-cloud-sdk-335.0.0/google-cloud-sdk
   Downloading Google Cloud SDK (this may take a little while)...
   Download complete. Installing Google Cloud SDK...


   Your current Cloud SDK version is: 335.0.0
   Installing components from version: 335.0.0

   ┌────────────────────────────────────────────────────────────────────────┐
   │                  These components will be installed.                   │
   ├────────────────────────────────────────────────┬────────────┬──────────┤
   │                      Name                      │  Version   │   Size   │
   ├────────────────────────────────────────────────┼────────────┼──────────┤
   │ Cloud Datastore Emulator                       │      2.1.0 │ 18.4 MiB │
   │ gRPC Python library                            │     1.20.0 │  1.9 MiB │
   │ gcloud Beta Commands                           │ 2019.05.17 │  < 1 MiB │
   │ gcloud app Python Extensions                   │     1.9.91 │  6.1 MiB │
   │ gcloud app Python Extensions (Extra Libraries) │     1.9.90 │ 27.1 MiB │
   │ gcloud cli dependencies                        │ 2020.06.12 │  < 1 MiB │
   └────────────────────────────────────────────────┴────────────┴──────────┘

   For the latest full release notes, please visit:
     https://cloud.google.com/sdk/release_notes

   ╔════════════════════════════════════════════════════════════╗
   ╠═ Creating update staging area                             ═╣
   ╠════════════════════════════════════════════════════════════╣
   ╠═ Installing: Cloud Datastore Emulator                     ═╣
   ╠════════════════════════════════════════════════════════════╣
   ╠═ Installing: gRPC Python library                          ═╣
   ╠════════════════════════════════════════════════════════════╣
   ╠═ Installing: gRPC Python library                          ═╣
   ╠════════════════════════════════════════════════════════════╣
   ╠═ Installing: gcloud Beta Commands                         ═╣
   ╠════════════════════════════════════════════════════════════╣
   ╠═ Installing: gcloud app Python Extensions                 ═╣
   ╠════════════════════════════════════════════════════════════╣
   ╠═ Installing: gcloud app Python Extensions (Extra Libra... ═╣
   ╠════════════════════════════════════════════════════════════╣
   ╠═ Installing: gcloud cli dependencies                      ═╣
   ╠════════════════════════════════════════════════════════════╣
   ╠═ Creating backup and activating new installation          ═╣
   ╚════════════════════════════════════════════════════════════╝

   Performing post processing steps...done.

   Update done!

   Checking if coverage is installed in /opensource/oppia/../oppia_tools
   Installing coverage
   Checking if pip is installed on the local machine
   Collecting coverage==5.3
     Using cached coverage-5.3-cp27-cp27m-macosx_10_13_intel.whl (210 kB)
   Installing collected packages: coverage
   Successfully installed coverage-5.3

   Checking if pylint is installed in /opensource/oppia/../oppia_tools
   Installing pylint
   Checking if pip is installed on the local machine
   Collecting pylint==1.9.5
     Using cached pylint-1.9.5-py2.py3-none-any.whl (696 kB)
   Collecting configparser; python_version == "2.7"
     Using cached configparser-4.0.2-py2.py3-none-any.whl (22 kB)
   Collecting six
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Collecting isort>=4.2.5
     Using cached isort-4.3.21-py2.py3-none-any.whl (42 kB)
   Collecting mccabe
     Using cached mccabe-0.6.1-py2.py3-none-any.whl (8.6 kB)
   Collecting backports.functools-lru-cache; python_version == "2.7"
     Using cached backports.functools_lru_cache-1.6.4-py2.py3-none-any.whl (5.9 kB)
   Collecting singledispatch; python_version < "3.4"
     Downloading singledispatch-3.6.2-py2.py3-none-any.whl (8.2 kB)
   Collecting astroid<2.0,>=1.6
     Using cached astroid-1.6.6-py2.py3-none-any.whl (305 kB)
   Collecting futures; python_version < "3.2"
     Using cached futures-3.3.0-py2-none-any.whl (16 kB)
   Processing /Users/user/Library/Caches/pip/wheels/b1/c2/ed/d62208260edbd3fa7156545c00ef966f45f2063d0a84f8208a/wrapt-1.12.1-cp27-cp27m-macosx_10_15_x86_64.whl
   Collecting lazy-object-proxy
     Using cached lazy_object_proxy-1.6.0-cp27-cp27m-macosx_10_14_x86_64.whl (21 kB)
   Collecting enum34>=1.1.3; python_version < "3.4"
     Using cached enum34-1.1.10-py2-none-any.whl (11 kB)
   Installing collected packages: configparser, six, backports.functools-lru-cache, futures, isort, mccabe, singledispatch, wrapt, lazy-object-proxy, enum34, astroid, pylint
   Successfully installed astroid-1.6.6 backports.functools-lru-cache-1.6.4 configparser-4.0.2 enum34-1.1.10 futures-3.3.0 isort-4.3.21 lazy-object-proxy-1.6.0 mccabe-0.6.1 pylint-1.9.5 singledispatch-3.6.2 six-1.16.0 wrapt-1.12.1

   Checking if Pillow is installed in /opensource/oppia/../oppia_tools
   Installing Pillow
   Checking if pip is installed on the local machine
   Collecting Pillow==6.2.2
     Using cached Pillow-6.2.2-cp27-cp27m-macosx_10_6_intel.whl (3.9 MB)
   Installing collected packages: Pillow
   Successfully installed Pillow-6.2.2

   Checking if pylint-quotes is installed in /opensource/oppia/../oppia_tools
   Installing pylint-quotes
   Checking if pip is installed on the local machine
   Collecting pylint-quotes==0.1.8
     Using cached pylint_quotes-0.1.8-py2.py3-none-any.whl (6.3 kB)
   Collecting pylint
     Using cached pylint-1.9.5-py2.py3-none-any.whl (696 kB)
   Collecting configparser; python_version == "2.7"
     Using cached configparser-4.0.2-py2.py3-none-any.whl (22 kB)
   Collecting six
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Collecting isort>=4.2.5
     Using cached isort-4.3.21-py2.py3-none-any.whl (42 kB)
   Collecting mccabe
     Using cached mccabe-0.6.1-py2.py3-none-any.whl (8.6 kB)
   Collecting backports.functools-lru-cache; python_version == "2.7"
     Using cached backports.functools_lru_cache-1.6.4-py2.py3-none-any.whl (5.9 kB)
   Collecting singledispatch; python_version < "3.4"
     Using cached singledispatch-3.6.2-py2.py3-none-any.whl (8.2 kB)
   Collecting astroid<2.0,>=1.6
     Using cached astroid-1.6.6-py2.py3-none-any.whl (305 kB)
   Collecting futures; python_version < "3.2"
     Using cached futures-3.3.0-py2-none-any.whl (16 kB)
   Processing /Users/user/Library/Caches/pip/wheels/b1/c2/ed/d62208260edbd3fa7156545c00ef966f45f2063d0a84f8208a/wrapt-1.12.1-cp27-cp27m-macosx_10_15_x86_64.whl
   Collecting lazy-object-proxy
     Using cached lazy_object_proxy-1.6.0-cp27-cp27m-macosx_10_14_x86_64.whl (21 kB)
   Collecting enum34>=1.1.3; python_version < "3.4"
     Using cached enum34-1.1.10-py2-none-any.whl (11 kB)
   Installing collected packages: configparser, six, backports.functools-lru-cache, futures, isort, mccabe, singledispatch, wrapt, lazy-object-proxy, enum34, astroid, pylint, pylint-quotes
   Successfully installed astroid-1.6.6 backports.functools-lru-cache-1.6.4 configparser-4.0.2 enum34-1.1.10 futures-3.3.0 isort-4.3.21 lazy-object-proxy-1.6.0 mccabe-0.6.1 pylint-1.9.5 pylint-quotes-0.1.8 singledispatch-3.6.2 six-1.16.0 wrapt-1.12.1

   Checking if webtest is installed in /opensource/oppia/../oppia_tools
   Installing webtest
   Checking if pip is installed on the local machine
   Collecting webtest==2.0.35
     Using cached WebTest-2.0.35-py2.py3-none-any.whl (32 kB)
   Collecting waitress>=0.8.5
     Using cached waitress-1.4.4-py2.py3-none-any.whl (58 kB)
   Collecting six
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Collecting WebOb>=1.2
     Using cached WebOb-1.8.7-py2.py3-none-any.whl (114 kB)
   Collecting beautifulsoup4
     Using cached beautifulsoup4-4.9.3-py2-none-any.whl (115 kB)
   Collecting soupsieve<2.0,>1.2; python_version < "3.0"
     Using cached soupsieve-1.9.6-py2.py3-none-any.whl (33 kB)
   Collecting backports.functools-lru-cache; python_version < "3"
     Using cached backports.functools_lru_cache-1.6.4-py2.py3-none-any.whl (5.9 kB)
   Installing collected packages: waitress, six, WebOb, backports.functools-lru-cache, soupsieve, beautifulsoup4, webtest
   Successfully installed WebOb-1.8.7 backports.functools-lru-cache-1.6.4 beautifulsoup4-4.9.3 six-1.16.0 soupsieve-1.9.6 waitress-1.4.4 webtest-2.0.35

   Checking if isort is installed in /opensource/oppia/../oppia_tools
   Installing isort
   Checking if pip is installed on the local machine
   Collecting isort==4.3.21
     Using cached isort-4.3.21-py2.py3-none-any.whl (42 kB)
   Collecting backports.functools-lru-cache; python_version < "3.2"
     Using cached backports.functools_lru_cache-1.6.4-py2.py3-none-any.whl (5.9 kB)
   Collecting futures; python_version < "3.2"
     Using cached futures-3.3.0-py2-none-any.whl (16 kB)
   Installing collected packages: backports.functools-lru-cache, futures, isort
   Successfully installed backports.functools-lru-cache-1.6.4 futures-3.3.0 isort-4.3.21

   Checking if pycodestyle is installed in /opensource/oppia/../oppia_tools
   Installing pycodestyle
   Checking if pip is installed on the local machine
   Collecting pycodestyle==2.6.0
     Using cached pycodestyle-2.6.0-py2.py3-none-any.whl (41 kB)
   Installing collected packages: pycodestyle
   Successfully installed pycodestyle-2.6.0

   Checking if esprima is installed in /opensource/oppia/../oppia_tools
   Installing esprima
   Checking if pip is installed on the local machine
   Processing /Users/user/Library/Caches/pip/wheels/63/aa/c8/3fbb4a3f263a33d0f89439d173d2b835426e4399a99f0c8e14/esprima-4.0.1-cp27-none-any.whl
   Installing collected packages: esprima
   Successfully installed esprima-4.0.1

   Checking if PyGithub is installed in /opensource/oppia/../oppia_tools
   Installing PyGithub
   Checking if pip is installed on the local machine
   Processing /Users/user/Library/Caches/pip/wheels/d5/81/71/87cc3f90fd363100cb788f462292f9a9e1e568b40e43d96944/PyGithub-1.45-cp27-none-any.whl
   Collecting requests>=2.14.0
     Downloading requests-2.26.0-py2.py3-none-any.whl (62 kB)
   Collecting pyjwt
     Using cached PyJWT-1.7.1-py2.py3-none-any.whl (18 kB)
   Collecting six
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Collecting deprecated
     Using cached Deprecated-1.2.12-py2.py3-none-any.whl (9.5 kB)
   Collecting urllib3<1.27,>=1.21.1
     Downloading urllib3-1.26.6-py2.py3-none-any.whl (138 kB)
   Collecting certifi>=2017.4.17
     Downloading certifi-2021.5.30-py2.py3-none-any.whl (145 kB)
   Collecting idna<3,>=2.5; python_version < "3"
     Using cached idna-2.10-py2.py3-none-any.whl (58 kB)
   Collecting chardet<5,>=3.0.2; python_version < "3"
     Using cached chardet-4.0.0-py2.py3-none-any.whl (178 kB)
   Processing /Users/user/Library/Caches/pip/wheels/b1/c2/ed/d62208260edbd3fa7156545c00ef966f45f2063d0a84f8208a/wrapt-1.12.1-cp27-cp27m-macosx_10_15_x86_64.whl
   Installing collected packages: urllib3, certifi, idna, chardet, requests, pyjwt, six, wrapt, deprecated, PyGithub
   Successfully installed PyGithub-1.45 certifi-2021.5.30 chardet-4.0.0 deprecated-1.2.12 idna-2.10 pyjwt-1.7.1 requests-2.26.0 six-1.16.0 urllib3-1.26.6 wrapt-1.12.1

   Checking if protobuf is installed in /opensource/oppia/../oppia_tools
   Installing protobuf
   Checking if pip is installed on the local machine
   Collecting protobuf==3.13.0
     Using cached protobuf-3.13.0-cp27-cp27m-macosx_10_9_x86_64.whl (1.3 MB)
   Collecting setuptools
     Using cached setuptools-44.1.1-py2.py3-none-any.whl (583 kB)
   Collecting six>=1.9
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Installing collected packages: setuptools, six, protobuf
   Successfully installed protobuf-3.13.0 setuptools-44.1.1 six-1.16.0

   Checking if psutil is installed in /opensource/oppia/../oppia_tools
   Installing psutil
   Checking if pip is installed on the local machine
   Processing /Users/user/Library/Caches/pip/wheels/42/32/da/8b12fd6b138c733efd03cfde6c6c8191a32842f9e82aa45fbf/psutil-5.7.3-cp27-cp27m-macosx_10_15_x86_64.whl
   Installing collected packages: psutil
   Successfully installed psutil-5.7.3

   Checking if pip-tools is installed in /opensource/oppia/../oppia_tools
   Installing pip-tools
   Checking if pip is installed on the local machine
   Collecting pip-tools==5.4.0
     Using cached pip_tools-5.4.0-py2.py3-none-any.whl (45 kB)
   Collecting click>=7
     Using cached click-7.1.2-py2.py3-none-any.whl (82 kB)
   Collecting pip>=20.1
     Using cached pip-20.3.4-py2.py3-none-any.whl (1.5 MB)
   Collecting six
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Installing collected packages: click, pip, six, pip-tools
   Successfully installed click-7.1.2 pip-20.3.4 pip-tools-5.4.0 six-1.16.0

   Checking if setuptools is installed in /opensource/oppia/../oppia_tools
   Installing setuptools
   Checking if pip is installed on the local machine
   Collecting setuptools==36.6.0
     Using cached setuptools-36.6.0-py2.py3-none-any.whl (481 kB)
   Installing collected packages: setuptools
   Successfully installed setuptools-36.6.0

   Checking if enum34 is installed.
   Checking if pip is installed on the local machine
   Collecting enum34==1.1.10
     Using cached enum34-1.1.10-py2-none-any.whl (11 kB)
   Installing collected packages: enum34
   Successfully installed enum34-1.1.10

   Checking if protobuf is installed.
   Checking if pip is installed on the local machine
   Collecting protobuf==3.13.0
     Using cached protobuf-3.13.0-cp27-cp27m-macosx_10_9_x86_64.whl (1.3 MB)
   Requirement already satisfied: setuptools in /Users/user/.pyenv/versions/2.7.16/envs/oppia-tmp/lib/python2.7/site-packages (from protobuf==3.13.0) (44.1.1)
   Collecting six>=1.9
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Installing collected packages: six, protobuf
   Successfully installed protobuf-3.13.0 six-1.16.0

   Installing third-party JS libraries and zip files.
   Checking if pip is installed on the local machine
   Regenerating "requirements.txt" file...
   #
   # This file is autogenerated by pip-compile
   # To update, run:
   #
   #    pip-compile
   #
   apache-beam[gcp]==2.24.0  # via -r requirements.in
   avro==1.9.2               # via apache-beam
   backports.functools-lru-cache==1.6.1  # via -r requirements.in, soupsieve
   beautifulsoup4==4.9.1     # via -r requirements.in
   bleach==3.3.0             # via -r requirements.in
   cachecontrol==0.12.6      # via firebase-admin
   cachetools==3.1.1         # via apache-beam, google-auth
   callbacks==0.3.0          # via -r requirements.in
   certifi==2020.6.20        # via elasticsearch, requests
   chardet==3.0.4            # via requests
   contextlib2==0.6.0.post1  # via -r requirements.in
   crcmod==1.7               # via apache-beam, google-resumable-media
   dill==0.3.1.1             # via apache-beam
   docopt==0.6.2             # via hdfs
   elasticsearch==7.10.0     # via -r requirements.in
   enum34==1.1.10            # via google-cloud-bigquery, google-cloud-dlp, google-cloud-language, google-cloud-pubsub, google-cloud-tasks, google-cloud-vision, grpcio, pyarrow
   fastavro==0.23.6          # via apache-beam
   fasteners==0.16           # via google-apitools
   git+git://github.com/oppia/firebase-admin-python@8d6deee889733d09ef5327d78c09e4d7b17785ac#egg=firebase-admin  # via -r requirements.in
   funcsigs==1.0.2           # via apache-beam, mock
   future==0.18.2            # via -r requirements.in, apache-beam
   futures==3.3.0            # via apache-beam, google-api-core, grpcio, pyarrow
   google-api-core[grpc,grpcgcp]==1.22.4  # via firebase-admin, google-api-python-client, google-cloud-bigquery, google-cloud-bigtable, google-cloud-core, google-cloud-datastore, google-cloud-dlp, google-cloud-firestore, google-cloud-language, google-cloud-pubsub, google-cloud-spanner, google-cloud-tasks, google-cloud-translate, google-cloud-videointelligence, google-cloud-vision
   google-api-python-client==1.12.8  # via firebase-admin
   google-apitools==0.5.31   # via apache-beam
   google-auth-httplib2==0.0.4  # via google-api-python-client
   google-auth==1.22.1       # via apache-beam, google-api-core, google-api-python-client, google-auth-httplib2, google-cloud-storage
   google-cloud-bigquery==1.28.0  # via apache-beam
   google-cloud-bigtable==1.7.0  # via apache-beam
   google-cloud-core==1.5.0  # via apache-beam, google-cloud-bigquery, google-cloud-bigtable, google-cloud-datastore, google-cloud-firestore, google-cloud-spanner, google-cloud-storage, google-cloud-translate
   google-cloud-datastore==1.15.3  # via apache-beam
   google-cloud-dlp==1.0.0   # via apache-beam
   google-cloud-firestore==1.9.0  # via firebase-admin
   google-cloud-language==1.3.0  # via apache-beam
   google-cloud-pubsub==1.7.0  # via apache-beam
   google-cloud-spanner==1.19.1  # via apache-beam
   google-cloud-storage==1.35.0  # via firebase-admin
   google-cloud-tasks==1.5.0  # via -r requirements.in
   google-cloud-translate==2.0.1  # via -r requirements.in
   google-cloud-videointelligence==1.16.1  # via apache-beam
   google-cloud-vision==1.0.0  # via apache-beam
   google-resumable-media==1.2.0  # via google-cloud-bigquery, google-cloud-storage
   googleapis-common-protos[grpc]==1.52.0  # via -r requirements.in, google-api-core, grpc-google-iam-v1
   googleappenginecloudstorageclient==1.9.22.1  # via -r requirements.in, googleappenginemapreduce, googleappenginepipeline
   googleappenginemapreduce==1.9.22.0  # via -r requirements.in
   googleappenginepipeline==1.9.22.1  # via -r requirements.in, googleappenginemapreduce
   graphy==1.0.0             # via -r requirements.in, googleappenginemapreduce
   grpc-google-iam-v1==0.12.3  # via google-cloud-bigtable, google-cloud-pubsub, google-cloud-spanner, google-cloud-tasks
   grpcio-gcp==0.2.2         # via apache-beam, google-api-core
   grpcio==1.32.0            # via apache-beam, google-api-core, googleapis-common-protos, grpc-google-iam-v1, grpcio-gcp
   hdfs==2.5.8               # via apache-beam
   html5lib==1.0.1           # via -r requirements.in
   httplib2==0.17.4          # via apache-beam, google-api-python-client, google-apitools, google-auth-httplib2, oauth2client
   idna==2.10                # via requests
   mock==2.0.0               # via apache-beam, googleappenginemapreduce
   monotonic==1.5            # via fasteners
   mox==0.5.3                # via googleappenginemapreduce
   msgpack==1.0.2            # via cachecontrol
   mutagen==1.43.0           # via -r requirements.in
   numpy==1.16.6             # via apache-beam, pyarrow
   oauth2client==3.0.0       # via apache-beam, google-apitools
   packaging==20.4           # via -r requirements.in, bleach
   pbr==5.5.1                # via mock
   protobuf==3.13.0          # via apache-beam, google-api-core, googleapis-common-protos
   pyarrow==0.16.0           # via apache-beam
   pyasn1-modules==0.2.8     # via google-auth, oauth2client
   pyasn1==0.4.8             # via oauth2client, pyasn1-modules, rsa
   pydot==1.4.1              # via apache-beam
   pylatexenc==2.6           # via -r requirements.in
   pymongo==3.11.3           # via apache-beam
   pyparsing==2.4.7          # via packaging, pydot
   python-dateutil==2.8.1    # via apache-beam
   pytz==2020.1              # via apache-beam, fastavro, google-api-core, google-cloud-firestore
   pyvcf==0.6.8              # via apache-beam
   redis==3.5.3              # via -r requirements.in
   requests-mock==1.5.2      # via -r requirements.in
   requests-toolbelt==0.9.1  # via -r requirements.in
   requests==2.24.0          # via -r requirements.in, apache-beam, cachecontrol, google-api-core, google-cloud-storage, hdfs, requests-mock, requests-toolbelt
   rsa==4.5                  # via google-auth, oauth2client
   simplejson==3.17.0        # via -r requirements.in, googleappenginemapreduce
   six==1.15.0               # via -r requirements.in, bleach, fasteners, firebase-admin, google-api-core, google-api-python-client, google-apitools, google-auth, google-auth-httplib2, google-cloud-bigquery, google-cloud-core, google-resumable-media, grpcio, hdfs, html5lib, mock, oauth2client, packaging, protobuf, pyarrow, python-dateutil, requests-mock, webapp2
   soupsieve==1.9.5          # via -r requirements.in, beautifulsoup4
   typing-extensions==3.7.4.3  # via apache-beam
   typing==3.7.4.3           # via apache-beam, typing-extensions
   uritemplate==3.0.1        # via google-api-python-client
   urllib3==1.25.11          # via elasticsearch, requests
   webapp2==3.0.0b1          # via -r requirements.in
   webencodings==0.5.1       # via -r requirements.in, bleach, html5lib
   webob==1.8.6              # via webapp2

   # The following packages are considered to be unsafe in a requirements file:
   # setuptools
   Checking if pip is installed on the local machine
   Collecting apache-beam[gcp]==2.24.0
     Using cached apache_beam-2.24.0-cp27-cp27m-macosx_10_9_x86_64.whl (3.6 MB)
   Processing /Users/user/Library/Caches/pip/wheels/28/a0/fc/a3d4892b81eedc9e027323c08e9890bee1ec2d35edd1c1ac96/avro-1.9.2-py2-none-any.whl
   Collecting backports.functools-lru-cache==1.6.1
     Using cached backports.functools_lru_cache-1.6.1-py2.py3-none-any.whl (5.7 kB)
   Collecting beautifulsoup4==4.9.1
     Using cached beautifulsoup4-4.9.1-py2-none-any.whl (111 kB)
   Collecting bleach==3.3.0
     Using cached bleach-3.3.0-py2.py3-none-any.whl (283 kB)
   Collecting cachecontrol==0.12.6
     Using cached CacheControl-0.12.6-py2.py3-none-any.whl (19 kB)
   Collecting cachetools==3.1.1
     Using cached cachetools-3.1.1-py2.py3-none-any.whl (11 kB)
   Collecting callbacks==0.3.0
     Using cached callbacks-0.3.0-py2-none-any.whl (5.7 kB)
   Collecting certifi==2020.6.20
     Using cached certifi-2020.6.20-py2.py3-none-any.whl (156 kB)
   Collecting chardet==3.0.4
     Using cached chardet-3.0.4-py2.py3-none-any.whl (133 kB)
   Collecting contextlib2==0.6.0.post1
     Using cached contextlib2-0.6.0.post1-py2.py3-none-any.whl (9.8 kB)
   Processing /Users/user/Library/Caches/pip/wheels/06/c2/19/2d00b8cea7d9ac6e19d286b0c41cf7a9eb39f64bd21ed43194/crcmod-1.7-cp27-cp27m-macosx_10_15_x86_64.whl
   Processing /Users/user/Library/Caches/pip/wheels/54/6e/1d/172ed90bc541c925faff97e03c7a110b8ce876ab13e10b0c77/dill-0.3.1.1-py2-none-any.whl
   Processing /Users/user/Library/Caches/pip/wheels/1c/d7/2d/aefbee2bf20e0ed968d4ab943e03451db0f14c52b5f624fc7e/docopt-0.6.2-py2.py3-none-any.whl
   Collecting elasticsearch==7.10.0
     Using cached elasticsearch-7.10.0-py2.py3-none-any.whl (321 kB)
   Collecting enum34==1.1.10
     Using cached enum34-1.1.10-py2-none-any.whl (11 kB)
   Collecting fastavro==0.23.6
     Using cached fastavro-0.23.6-cp27-cp27m-macosx_10_14_x86_64.whl (397 kB)
   Collecting fasteners==0.16
     Using cached fasteners-0.16-py2.py3-none-any.whl (28 kB)
   Collecting firebase-admin
     Using cached firebase_admin-3.2.1-py2.py3-none-any.whl
   Collecting funcsigs==1.0.2
     Using cached funcsigs-1.0.2-py2.py3-none-any.whl (17 kB)
   Processing /Users/user/Library/Caches/pip/wheels/8b/99/a0/81daf51dcd359a9377b110a8a886b3895921802d2fc1b2397e/future-0.18.2-cp27-none-any.whl
   Collecting futures==3.3.0
     Using cached futures-3.3.0-py2-none-any.whl (16 kB)
   Collecting google-api-core[grpc,grpcgcp]==1.22.4
     Using cached google_api_core-1.22.4-py2.py3-none-any.whl (91 kB)
   Collecting google-api-python-client==1.12.8
     Using cached google_api_python_client-1.12.8-py2.py3-none-any.whl (61 kB)
   Collecting google-apitools==0.5.31
     Using cached google_apitools-0.5.31-py2-none-any.whl (135 kB)
   Collecting google-auth-httplib2==0.0.4
     Using cached google_auth_httplib2-0.0.4-py2.py3-none-any.whl (9.1 kB)
   Collecting google-auth==1.22.1
     Using cached google_auth-1.22.1-py2.py3-none-any.whl (114 kB)
   Collecting google-cloud-bigquery==1.28.0
     Using cached google_cloud_bigquery-1.28.0-py2.py3-none-any.whl (187 kB)
   Collecting google-cloud-bigtable==1.7.0
     Using cached google_cloud_bigtable-1.7.0-py2.py3-none-any.whl (267 kB)
   Collecting google-cloud-core==1.5.0
     Using cached google_cloud_core-1.5.0-py2.py3-none-any.whl (27 kB)
   Collecting google-cloud-datastore==1.15.3
     Using cached google_cloud_datastore-1.15.3-py2.py3-none-any.whl (134 kB)
   Collecting google-cloud-dlp==1.0.0
     Using cached google_cloud_dlp-1.0.0-py2.py3-none-any.whl (169 kB)
   Collecting google-cloud-firestore==1.9.0
     Using cached google_cloud_firestore-1.9.0-py2.py3-none-any.whl (344 kB)
   Collecting google-cloud-language==1.3.0
     Using cached google_cloud_language-1.3.0-py2.py3-none-any.whl (83 kB)
   Collecting google-cloud-pubsub==1.7.0
     Using cached google_cloud_pubsub-1.7.0-py2.py3-none-any.whl (144 kB)
   Collecting google-cloud-spanner==1.19.1
     Using cached google_cloud_spanner-1.19.1-py2.py3-none-any.whl (255 kB)
   Collecting google-cloud-storage==1.35.0
     Using cached google_cloud_storage-1.35.0-py2.py3-none-any.whl (96 kB)
   Collecting google-cloud-tasks==1.5.0
     Using cached google_cloud_tasks-1.5.0-py2.py3-none-any.whl (215 kB)
   Collecting google-cloud-translate==2.0.1
     Using cached google_cloud_translate-2.0.1-py2.py3-none-any.whl (90 kB)
   Collecting google-cloud-videointelligence==1.16.1
     Using cached google_cloud_videointelligence-1.16.1-py2.py3-none-any.whl (183 kB)
   Collecting google-cloud-vision==1.0.0
     Using cached google_cloud_vision-1.0.0-py2.py3-none-any.whl (435 kB)
   Collecting google-resumable-media==1.2.0
     Using cached google_resumable_media-1.2.0-py2.py3-none-any.whl (75 kB)
   Collecting googleapis-common-protos[grpc]==1.52.0
     Using cached googleapis_common_protos-1.52.0-py2.py3-none-any.whl (100 kB)
   Processing /Users/user/Library/Caches/pip/wheels/e5/2f/b3/6bdb2fd3f05228d7ad93f1f130e6b203c5f5a34263f8a7dee4/GoogleAppEngineCloudStorageClient-1.9.22.1-cp27-none-any.whl
   Processing /Users/user/Library/Caches/pip/wheels/15/ae/f0/f04a8648aae57361d2a896a377edce3de662153a9e09f40f80/GoogleAppEngineMapReduce-1.9.22.0-cp27-none-any.whl
   Processing /Users/user/Library/Caches/pip/wheels/36/d4/62/694d6b99f70c77ac1e5b0d898e85c4135e494c8a4ac08023a4/GoogleAppEnginePipeline-1.9.22.1-cp27-none-any.whl
   Processing /Users/user/Library/Caches/pip/wheels/d4/17/c7/b5a20f1b0e44336c2e3080e4444a6234b320800453f0c513ef/Graphy-1.0.0-cp27-none-any.whl
   Processing /Users/user/Library/Caches/pip/wheels/de/3a/83/77a1e18e1a8757186df834b86ce6800120ac9c79cd8ca4091b/grpc_google_iam_v1-0.12.3-cp27-none-any.whl
   Collecting grpcio-gcp==0.2.2
     Using cached grpcio_gcp-0.2.2-py2.py3-none-any.whl (9.4 kB)
   Collecting grpcio==1.32.0
     Using cached grpcio-1.32.0-cp27-cp27m-macosx_10_9_x86_64.whl (3.3 MB)
   Processing /Users/user/Library/Caches/pip/wheels/3a/18/11/31dfb768f5d55108760cdd028ad7026173f7c0e847cb71fe4b/hdfs-2.5.8-py2-none-any.whl
   Collecting html5lib==1.0.1
     Using cached html5lib-1.0.1-py2.py3-none-any.whl (117 kB)
   Processing /Users/user/Library/Caches/pip/wheels/ce/98/d0/7cbebe9de22c986e85e2561069d25c9752b43523240f803199/httplib2-0.17.4-py2-none-any.whl
   Collecting idna==2.10
     Using cached idna-2.10-py2.py3-none-any.whl (58 kB)
   Collecting mock==2.0.0
     Using cached mock-2.0.0-py2.py3-none-any.whl (56 kB)
   Collecting monotonic==1.5
     Using cached monotonic-1.5-py2.py3-none-any.whl (5.3 kB)
   Processing /Users/user/Library/Caches/pip/wheels/33/cd/ad/ecda0a1c076b959cf62237eebe1d736ae81b048b22bbc64e6d/mox-0.5.3-cp27-none-any.whl
   Processing /Users/user/Library/Caches/pip/wheels/9a/c1/2f/dee60aba1e3df6f5a6edd694e62bf14f3537158cf1b63cc39d/msgpack-1.0.2-py2-none-any.whl
   Collecting mutagen==1.43.0
     Using cached mutagen-1.43.0-py2.py3-none-any.whl (212 kB)
   Collecting numpy==1.16.6
     Using cached numpy-1.16.6-cp27-cp27m-macosx_10_9_x86_64.whl (13.9 MB)
   Processing /Users/user/Library/Caches/pip/wheels/b3/ca/7f/39e3e6758df2c1bfc56e12e3a7cb4693a7da0a63f0c9791f14/oauth2client-3.0.0-py2-none-any.whl
   Collecting packaging==20.4
     Using cached packaging-20.4-py2.py3-none-any.whl (37 kB)
   Collecting pbr==5.5.1
     Using cached pbr-5.5.1-py2.py3-none-any.whl (106 kB)
   Collecting protobuf==3.13.0
     Using cached protobuf-3.13.0-cp27-cp27m-macosx_10_9_x86_64.whl (1.3 MB)
   Collecting pyarrow==0.16.0
     Using cached pyarrow-0.16.0-cp27-cp27m-macosx_10_9_intel.whl (21.7 MB)
   Collecting pyasn1-modules==0.2.8
     Using cached pyasn1_modules-0.2.8-py2.py3-none-any.whl (155 kB)
   Collecting pyasn1==0.4.8
     Using cached pyasn1-0.4.8-py2.py3-none-any.whl (77 kB)
   Collecting pydot==1.4.1
     Using cached pydot-1.4.1-py2.py3-none-any.whl (19 kB)
   Processing /Users/user/Library/Caches/pip/wheels/bc/bc/42/3dac088caf1b6a70d45100e79144b555f3db7cfb4f7be426b2/pylatexenc-2.6-cp27-none-any.whl
   Collecting pymongo==3.11.3
     Using cached pymongo-3.11.3-cp27-cp27m-macosx_10_14_intel.whl (375 kB)
   Collecting pyparsing==2.4.7
     Using cached pyparsing-2.4.7-py2.py3-none-any.whl (67 kB)
   Collecting python-dateutil==2.8.1
     Using cached python_dateutil-2.8.1-py2.py3-none-any.whl (227 kB)
   Collecting pytz==2020.1
     Using cached pytz-2020.1-py2.py3-none-any.whl (510 kB)
   Processing /Users/user/Library/Caches/pip/wheels/b8/43/84/5248fa58c81c6f2a9b1e4f1f8b12573f79a75f492c7a1b0e5a/PyVCF-0.6.8-py2-none-any.whl
   Collecting redis==3.5.3
     Using cached redis-3.5.3-py2.py3-none-any.whl (72 kB)
   Collecting requests-mock==1.5.2
     Using cached requests_mock-1.5.2-py2.py3-none-any.whl (22 kB)
   Collecting requests-toolbelt==0.9.1
     Using cached requests_toolbelt-0.9.1-py2.py3-none-any.whl (54 kB)
   Collecting requests==2.24.0
     Using cached requests-2.24.0-py2.py3-none-any.whl (61 kB)
   Collecting rsa==4.5
     Using cached rsa-4.5-py2.py3-none-any.whl (36 kB)
   Collecting simplejson==3.17.0
     Using cached simplejson-3.17.0-cp27-cp27m-macosx_10_13_x86_64.whl (74 kB)
   Collecting six==1.15.0
     Using cached six-1.15.0-py2.py3-none-any.whl (10 kB)
   Collecting soupsieve==1.9.5
     Using cached soupsieve-1.9.5-py2.py3-none-any.whl (33 kB)
   Collecting typing-extensions==3.7.4.3
     Using cached typing_extensions-3.7.4.3-py2-none-any.whl (9.3 kB)
   Collecting typing==3.7.4.3
     Using cached typing-3.7.4.3-py2-none-any.whl (26 kB)
   Collecting uritemplate==3.0.1
     Using cached uritemplate-3.0.1-py2.py3-none-any.whl (15 kB)
   Collecting urllib3==1.25.11
     Using cached urllib3-1.25.11-py2.py3-none-any.whl (127 kB)
   Processing /Users/user/Library/Caches/pip/wheels/db/46/a3/ffe5500cc4dd3fc1e5de0485287a4d484f15f3e2293fe4c994/webapp2-3.0.0b1-cp27-none-any.whl
   Collecting webencodings==0.5.1
     Using cached webencodings-0.5.1-py2.py3-none-any.whl (11 kB)
   Collecting webob==1.8.6
     Using cached WebOb-1.8.6-py2.py3-none-any.whl (114 kB)
   Installing collected packages: apache-beam, avro, backports.functools-lru-cache, beautifulsoup4, bleach, cachecontrol, cachetools, callbacks, certifi, chardet, contextlib2, crcmod, dill, docopt, elasticsearch, enum34, fastavro, fasteners, firebase-admin, funcsigs, future, futures, google-api-core, google-api-python-client, google-apitools, google-auth-httplib2, google-auth, google-cloud-bigquery, google-cloud-bigtable, google-cloud-core, google-cloud-datastore, google-cloud-dlp, google-cloud-firestore, google-cloud-language, google-cloud-pubsub, google-cloud-spanner, google-cloud-storage, google-cloud-tasks, google-cloud-translate, google-cloud-videointelligence, google-cloud-vision, google-resumable-media, googleapis-common-protos, googleappenginecloudstorageclient, googleappenginemapreduce, googleappenginepipeline, graphy, grpc-google-iam-v1, grpcio-gcp, grpcio, hdfs, html5lib, httplib2, idna, mock, monotonic, mox, msgpack, mutagen, numpy, oauth2client, packaging, pbr, protobuf, pyarrow, pyasn1-modules, pyasn1, pydot, pylatexenc, pymongo, pyparsing, python-dateutil, pytz, pyvcf, redis, requests-mock, requests-toolbelt, requests, rsa, simplejson, six, soupsieve, typing-extensions, typing, uritemplate, urllib3, webapp2, webencodings, webob
   Successfully installed apache-beam-2.24.0 avro-1.9.2 backports.functools-lru-cache-1.6.1 beautifulsoup4-4.9.1 bleach-3.3.0 cachecontrol-0.12.6 cachetools-3.1.1 callbacks-0.3.0 certifi-2020.6.20 chardet-3.0.4 contextlib2-0.6.0.post1 crcmod-1.7 dill-0.3.1.1 docopt-0.6.2 elasticsearch-7.10.0 enum34-1.1.10 fastavro-0.23.6 fasteners-0.16 firebase-admin-3.2.1 funcsigs-1.0.2 future-0.18.2 futures-3.3.0 google-api-core-1.22.4 google-api-python-client-1.12.8 google-apitools-0.5.31 google-auth-1.22.1 google-auth-httplib2-0.0.4 google-cloud-bigquery-1.28.0 google-cloud-bigtable-1.7.0 google-cloud-core-1.5.0 google-cloud-datastore-1.15.3 google-cloud-dlp-1.0.0 google-cloud-firestore-1.9.0 google-cloud-language-1.3.0 google-cloud-pubsub-1.7.0 google-cloud-spanner-1.19.1 google-cloud-storage-1.35.0 google-cloud-tasks-1.5.0 google-cloud-translate-2.0.1 google-cloud-videointelligence-1.16.1 google-cloud-vision-1.0.0 google-resumable-media-1.2.0 googleapis-common-protos-1.52.0 googleappenginecloudstorageclient-1.9.22.1 googleappenginemapreduce-1.9.22.0 googleappenginepipeline-1.9.22.1 graphy-1.0.0 grpc-google-iam-v1-0.12.3 grpcio-1.32.0 grpcio-gcp-0.2.2 hdfs-2.5.8 html5lib-1.0.1 httplib2-0.17.4 idna-2.10 mock-2.0.0 monotonic-1.5 mox-0.5.3 msgpack-1.0.2 mutagen-1.43.0 numpy-1.16.6 oauth2client-3.0.0 packaging-20.4 pbr-5.5.1 protobuf-3.13.0 pyarrow-0.16.0 pyasn1-0.4.8 pyasn1-modules-0.2.8 pydot-1.4.1 pylatexenc-2.6 pymongo-3.11.3 pyparsing-2.4.7 python-dateutil-2.8.1 pytz-2020.1 pyvcf-0.6.8 redis-3.5.3 requests-2.24.0 requests-mock-1.5.2 requests-toolbelt-0.9.1 rsa-4.5 simplejson-3.17.0 six-1.15.0 soupsieve-1.9.5 typing-3.7.4.3 typing-extensions-3.7.4.3 uritemplate-3.0.1 urllib3-1.25.11 webapp2-3.0.0b1 webencodings-0.5.1 webob-1.8.6

   Downloading file yuicompressor-2.4.8.jar to ../oppia_tools/yuicompressor-2.4.8 ...
   Download of yuicompressor-2.4.8.jar succeeded.
   Downloading and unzipping file MathJax-2.7.5 to ./third_party/static ...
   Download of MathJax-2.7.5 succeeded.
   Downloading and unzipping file ng-joyride-b117e019582433995393f81e2006a6bc36ca1cf2 to ./third_party/static ...
   Download of ng-joyride-b117e019582433995393f81e2006a6bc36ca1cf2 succeeded.
   Downloading and unzipping file bower-material-1.1.19 to ./third_party/static ...
   Download of bower-material-1.1.19 succeeded.
   Downloading and unzipping file angular-ui-tree-master to ./third_party/static ...
   Download of angular-ui-tree-master succeeded.
   Downloading and unzipping file fontawesome-free-5.9.0-web to ./third_party/static ...
   Download of fontawesome-free-5.9.0-web succeeded.
   Downloading file angular-translate-loader-static-files.min.js to ./third_party/static/bower-angular-translate-loader-static-files-2.18.1 ...
   Download of angular-translate-loader-static-files.min.js succeeded.
   Downloading and unzipping file guppy-7509f31c3f6e1205763d605ab41098cf6ac9d738 to ./third_party/static ...
   Download of guppy-7509f31c3f6e1205763d605ab41098cf6ac9d738 succeeded.
   Downloading file angular.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular.js succeeded.
   Downloading file angular.min.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular.min.js succeeded.
   Downloading file angular.min.js.map to ./third_party/static/angularjs-1.8.2 ...
   Download of angular.min.js.map succeeded.
   Downloading file angular-animate.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-animate.js succeeded.
   Downloading file angular-animate.min.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-animate.min.js succeeded.
   Downloading file angular-animate.min.js.map to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-animate.min.js.map succeeded.
   Downloading file angular-resource.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-resource.js succeeded.
   Downloading file angular-resource.min.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-resource.min.js succeeded.
   Downloading file angular-resource.min.js.map to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-resource.min.js.map succeeded.
   Downloading file angular-route.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-route.js succeeded.
   Downloading file angular-route.min.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-route.min.js succeeded.
   Downloading file angular-route.min.js.map to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-route.min.js.map succeeded.
   Downloading file angular-sanitize.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-sanitize.js succeeded.
   Downloading file angular-sanitize.min.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-sanitize.min.js succeeded.
   Downloading file angular-sanitize.min.js.map to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-sanitize.min.js.map succeeded.
   Downloading file angular-aria.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-aria.js succeeded.
   Downloading file angular-aria.min.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-aria.min.js succeeded.
   Downloading file angular-aria.min.js.map to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-aria.min.js.map succeeded.
   Downloading file angular-touch.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-touch.js succeeded.
   Downloading file angular-touch.min.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-touch.min.js succeeded.
   Downloading file angular-touch.min.js.map to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-touch.min.js.map succeeded.
   Downloading file ui-bootstrap-tpls-2.5.0.js to ./third_party/static/ui-bootstrap-2.5.0 ...
   Download of ui-bootstrap-tpls-2.5.0.js succeeded.
   Downloading file ui-bootstrap-tpls-2.5.0.min.js to ./third_party/static/ui-bootstrap-2.5.0 ...
   Download of ui-bootstrap-tpls-2.5.0.min.js succeeded.
   Downloading and unzipping file jquery-ui-touch-punch-improved-0.3.1 to ./third_party/static ...
   Download of jquery-ui-touch-punch-improved-0.3.1 succeeded.
   Downloading file diff_match_patch.js to ./third_party/static/diff-match-patch-1.0.0 ...
   Download of diff_match_patch.js succeeded.
   Downloading file angular-translate-loader-partial.min.js to ./third_party/static/bower-angular-translate-loader-partial-2.18.1 ...
   Download of angular-translate-loader-partial.min.js succeeded.
   Downloading file angular-simple-logger.min.js to ./third_party/static/angular-simple-logger-0.1.7 ...
   Download of angular-simple-logger.min.js succeeded.
   Downloading and unzipping file MIDI.js-c26ebb9baaf0abc060c8a13254dad283c6ee7304 to ./third_party/static ...
   Download of MIDI.js-c26ebb9baaf0abc060c8a13254dad283c6ee7304 succeeded.
   Downloading file jquery-ui.min.js to ./third_party/static/jqueryui-1.12.1 ...
   Download of jquery-ui.min.js succeeded.
   Downloading and unzipping file ui-codemirror-5d04fa5c991f915e4578be5f1175e22d94696633 to ./third_party/static ...
   Download of ui-codemirror-5d04fa5c991f915e4578be5f1175e22d94696633 succeeded.
   Downloading and unzipping file angular-toastr-1.7.0 to ./third_party/static ...
   Download of angular-toastr-1.7.0 succeeded.
   Downloading file angular-translate-interpolation-messageformat.min.js to ./third_party/static/bower-angular-translate-interpolation-messageformat-2.18.1 ...
   Download of angular-translate-interpolation-messageformat.min.js succeeded.
   Downloading and unzipping file angular-drag-and-drop-lists-2.1.0 to ./third_party/static ...
   Download of angular-drag-and-drop-lists-2.1.0 succeeded.
   Downloading and unzipping file messageformat-2.0.5 to ./third_party/static ...
   Download of messageformat-2.0.5 succeeded.
   Downloading and unzipping file popper-core-1.15.0 to ./third_party/static ...
   Download of popper-core-1.15.0 succeeded.
   Downloading and unzipping file BootstrapCK4-Skin-1.0.0 to ./third_party/static ...
   Download of BootstrapCK4-Skin-1.0.0 succeeded.
   Downloading file angular-translate-storage-cookie.min.js to ./third_party/static/bower-angular-translate-storage-cookie-2.18.1 ...
   Download of angular-translate-storage-cookie.min.js succeeded.
   Downloading file angular.headroom.min.js to ./third_party/static/headroom-js-0.9.4 ...
   Download of angular.headroom.min.js succeeded.
   Downloading file headroom.min.js to ./third_party/static/headroom-js-0.9.4 ...
   Download of headroom.min.js succeeded.
   Downloading file angular-translate.min.js to ./third_party/static/bower-angular-translate-2.18.1 ...
   Download of angular-translate.min.js succeeded.
   Downloading file ui-leaflet.min.no-header.js to ./third_party/static/angular-ui-leaflet-1.0.3 ...
   Download of ui-leaflet.min.no-header.js succeeded.
   Downloading and unzipping file CodeMirror-5.17.0 to ./third_party/static ...
   Download of CodeMirror-5.17.0 succeeded.
   Downloading file jquery.js to ./third_party/static/jquery-3.5.1 ...
   Download of jquery.js succeeded.
   Downloading file jquery.min.js to ./third_party/static/jquery-3.5.1 ...
   Download of jquery.min.js succeeded.
   Downloading file jquery.min.js.map to ./third_party/static/jquery-3.5.1 ...
   Download of jquery.min.js.map succeeded.
   Downloading and unzipping file ngAudio-1.7.4 to ./third_party/static ...
   Download of ngAudio-1.7.4 succeeded.
   Downloading and unzipping file ckeditor4-releases-4.12.1 to ./third_party/static ...
   Download of ckeditor4-releases-4.12.1 succeeded.
   Downloading file angular-mocks.js to ./third_party/static/angularjs-1.8.2 ...
   Download of angular-mocks.js succeeded.
   Downloading and unzipping file bootstrap-4.3.1-dist to ./third_party/static ...
   Download of bootstrap-4.3.1-dist succeeded.
   Downloading file leaflet.js to ./third_party/static/leaflet-1.4.0 ...
   Download of leaflet.js succeeded.
   Downloading file leaflet.css to ./third_party/static/leaflet-1.4.0 ...
   Download of leaflet.css succeeded.
   Downloading and unzipping file skulpt-dist-1.1.0 to ./third_party/static ...
   Download of skulpt-dist-1.1.0 succeeded.
   Downloading and unzipping file lamejs-1.2.0 to ./third_party/static ...
   Download of lamejs-1.2.0 succeeded.
   Downloading and unzipping file select2-4.0.3 to ./third_party/static ...
   Download of select2-4.0.3 succeeded.
   Downloading and unzipping file oppia-ml-proto-0.0.0 to ./third_party ...
   Download of oppia-ml-proto-0.0.0 succeeded.
   Installing redis-cli...
   Downloading and untarring file redis-6.0.10 to ../oppia_tools ...
   Download of redis-6.0.10 succeeded.
   cd src && /Library/Developer/CommandLineTools/usr/bin/make all
       CC Makefile.dep
   rm -rf redis-server redis-sentinel redis-cli redis-benchmark redis-check-rdb redis-check-aof *.o *.gcda *.gcno *.gcov redis.info lcov-html Makefile.dep dict-benchmark
   rm -f adlist.d quicklist.d ae.d anet.d dict.d server.d sds.d zmalloc.d lzf_c.d lzf_d.d pqsort.d zipmap.d sha1.d ziplist.d release.d networking.d util.d object.d db.d replication.d rdb.d t_string.d t_list.d t_set.d t_zset.d t_hash.d config.d aof.d pubsub.d multi.d debug.d sort.d intset.d syncio.d cluster.d crc16.d endianconv.d slowlog.d scripting.d bio.d rio.d rand.d memtest.d crcspeed.d crc64.d bitops.d sentinel.d notify.d setproctitle.d blocked.d hyperloglog.d latency.d sparkline.d redis-check-rdb.d redis-check-aof.d geo.d lazyfree.d module.d evict.d expire.d geohash.d geohash_helper.d childinfo.d defrag.d siphash.d rax.d t_stream.d listpack.d localtime.d lolwut.d lolwut5.d lolwut6.d acl.d gopher.d tracking.d connection.d tls.d sha256.d timeout.d setcpuaffinity.d anet.d adlist.d dict.d redis-cli.d zmalloc.d release.d ae.d crcspeed.d crc64.d siphash.d crc16.d ae.d anet.d redis-benchmark.d adlist.d dict.d zmalloc.d siphash.d
   (cd ../deps && /Library/Developer/CommandLineTools/usr/bin/make distclean)
   (cd hiredis && /Library/Developer/CommandLineTools/usr/bin/make clean) > /dev/null || true
   (cd linenoise && /Library/Developer/CommandLineTools/usr/bin/make clean) > /dev/null || true
   (cd lua && /Library/Developer/CommandLineTools/usr/bin/make clean) > /dev/null || true
   (cd jemalloc && [ -f Makefile ] && /Library/Developer/CommandLineTools/usr/bin/make distclean) > /dev/null || true
   (rm -f .make-*)
   (rm -f .make-*)
   echo STD=-std=c11 -pedantic -DREDIS_STATIC='' >> .make-settings
   echo WARN=-Wall -W -Wno-missing-field-initializers >> .make-settings
   echo OPT=-O2 >> .make-settings
   echo MALLOC=libc >> .make-settings
   echo BUILD_TLS= >> .make-settings
   echo USE_SYSTEMD= >> .make-settings
   echo CFLAGS= >> .make-settings
   echo LDFLAGS= >> .make-settings
   echo REDIS_CFLAGS= >> .make-settings
   echo REDIS_LDFLAGS= >> .make-settings
   echo PREV_FINAL_CFLAGS=-std=c11 -pedantic -DREDIS_STATIC='' -Wall -W -Wno-missing-field-initializers -O2 -g -ggdb   -I../deps/hiredis -I../deps/linenoise -I../deps/lua/src >> .make-settings
   echo PREV_FINAL_LDFLAGS=  -g -ggdb >> .make-settings
   (cd ../deps && /Library/Developer/CommandLineTools/usr/bin/make hiredis linenoise lua)
   (cd hiredis && /Library/Developer/CommandLineTools/usr/bin/make clean) > /dev/null || true
   (cd linenoise && /Library/Developer/CommandLineTools/usr/bin/make clean) > /dev/null || true
   (cd lua && /Library/Developer/CommandLineTools/usr/bin/make clean) > /dev/null || true
   (cd jemalloc && [ -f Makefile ] && /Library/Developer/CommandLineTools/usr/bin/make distclean) > /dev/null || true
   (rm -f .make-*)
   (echo "" > .make-ldflags)
   (echo "" > .make-cflags)
   MAKE hiredis
   cd hiredis && /Library/Developer/CommandLineTools/usr/bin/make static
   cc -std=c99 -pedantic -c -O3 -fPIC  -I/usr/local/opt/openssl/include -Wall -W -Wstrict-prototypes -Wwrite-strings -Wno-missing-field-initializers -g -ggdb net.c
   cc -std=c99 -pedantic -c -O3 -fPIC  -I/usr/local/opt/openssl/include -Wall -W -Wstrict-prototypes -Wwrite-strings -Wno-missing-field-initializers -g -ggdb hiredis.c
   cc -std=c99 -pedantic -c -O3 -fPIC  -I/usr/local/opt/openssl/include -Wall -W -Wstrict-prototypes -Wwrite-strings -Wno-missing-field-initializers -g -ggdb sds.c
   cc -std=c99 -pedantic -c -O3 -fPIC  -I/usr/local/opt/openssl/include -Wall -W -Wstrict-prototypes -Wwrite-strings -Wno-missing-field-initializers -g -ggdb async.c
   cc -std=c99 -pedantic -c -O3 -fPIC  -I/usr/local/opt/openssl/include -Wall -W -Wstrict-prototypes -Wwrite-strings -Wno-missing-field-initializers -g -ggdb read.c
   cc -std=c99 -pedantic -c -O3 -fPIC  -I/usr/local/opt/openssl/include -Wall -W -Wstrict-prototypes -Wwrite-strings -Wno-missing-field-initializers -g -ggdb sockcompat.c
   ar rcs libhiredis.a net.o hiredis.o sds.o async.o read.o sockcompat.o
   /Library/Developer/CommandLineTools/usr/bin/ranlib: file: libhiredis.a(sockcompat.o) has no symbols
   MAKE linenoise
   cd linenoise && /Library/Developer/CommandLineTools/usr/bin/make
   cc  -Wall -Os -g  -c linenoise.c
   MAKE lua
   cd lua/src && /Library/Developer/CommandLineTools/usr/bin/make all CFLAGS="-O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC='' " MYLDFLAGS="" AR="ar rcu"
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lapi.o lapi.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lcode.o lcode.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ldebug.o ldebug.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ldo.o ldo.c
   ldo.c:496:7: warning: unused variable 'c' [-Wunused-variable]
     int c = luaZ_lookahead(p->z);
         ^
   1 warning generated.
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ldump.o ldump.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lfunc.o lfunc.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lgc.o lgc.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o llex.o llex.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lmem.o lmem.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lobject.o lobject.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lopcodes.o lopcodes.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lparser.o lparser.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lstate.o lstate.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lstring.o lstring.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ltable.o ltable.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ltm.o ltm.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lundump.o lundump.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lvm.o lvm.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lzio.o lzio.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o strbuf.o strbuf.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o fpconv.o fpconv.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lauxlib.o lauxlib.c
   lauxlib.c:577:61: warning: while loop has empty body [-Wempty-body]
      while ((c = getc(lf.f)) != EOF && c != LUA_SIGNATURE[0]) ;
                                                               ^
   lauxlib.c:577:61: note: put the semicolon on a separate line to silence this warning
   1 warning generated.
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lbaselib.o lbaselib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ldblib.o ldblib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o liolib.o liolib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lmathlib.o lmathlib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o loslib.o loslib.c
   loslib.c:60:3: warning: 'tmpnam' is deprecated: This function is provided for compatibility reasons only. Due to security concerns inherent in the design of tmpnam(3), it is highly recommended that you
         use mkstemp(3) instead. [-Wdeprecated-declarations]
     lua_tmpnam(buff, err);
     ^
   ./luaconf.h:657:33: note: expanded from macro 'lua_tmpnam'
   #define lua_tmpnam(b,e)         { e = (tmpnam(b) == NULL); }
                                          ^
   /Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include/stdio.h:186:1: note: 'tmpnam' has been explicitly marked deprecated here
   __deprecated_msg("This function is provided for compatibility reasons only.  Due to security concerns inherent in the design of tmpnam(3), it is highly recommended that you use mkstemp(3) instead.")
   ^
   /Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include/sys/cdefs.h:200:48: note: expanded from macro '__deprecated_msg'
           #define __deprecated_msg(_msg) __attribute__((__deprecated__(_msg)))
                                                         ^
   1 warning generated.
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ltablib.o ltablib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lstrlib.o lstrlib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o loadlib.o loadlib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o linit.o linit.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua_cjson.o lua_cjson.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua_struct.o lua_struct.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua_cmsgpack.o lua_cmsgpack.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua_bit.o lua_bit.c
   ar rcu liblua.a lapi.o lcode.o ldebug.o ldo.o ldump.o lfunc.o lgc.o llex.o lmem.o lobject.o lopcodes.o lparser.o lstate.o lstring.o ltable.o ltm.o lundump.o lvm.o lzio.o strbuf.o fpconv.o lauxlib.o lbaselib.o ldblib.o liolib.o lmathlib.o loslib.o ltablib.o lstrlib.o loadlib.o linit.o lua_cjson.o lua_struct.o lua_cmsgpack.o lua_bit.o	# DLL needs all object files
   ranlib liblua.a
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua.o lua.c
   cc -o lua  lua.o liblua.a -lm
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o luac.o luac.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o print.o print.c
   cc -o luac  luac.o print.o liblua.a -lm
       CC adlist.o
       CC quicklist.o
       CC ae.o
       CC anet.o
       CC dict.o
       CC server.o
       CC sds.o
       CC zmalloc.o
       CC lzf_c.o
       CC lzf_d.o
       CC pqsort.o
       CC zipmap.o
       CC sha1.o
       CC ziplist.o
       CC release.o
       CC networking.o
       CC util.o
       CC object.o
       CC db.o
       CC replication.o
       CC rdb.o
       CC t_string.o
       CC t_list.o
       CC t_set.o
       CC t_zset.o
       CC t_hash.o
       CC config.o
       CC aof.o
       CC pubsub.o
       CC multi.o
       CC debug.o
       CC sort.o
       CC intset.o
       CC syncio.o
       CC cluster.o
       CC crc16.o
       CC endianconv.o
       CC slowlog.o
       CC scripting.o
       CC bio.o
       CC rio.o
       CC rand.o
       CC memtest.o
       CC crcspeed.o
       CC crc64.o
       CC bitops.o
       CC sentinel.o
       CC notify.o
       CC setproctitle.o
       CC blocked.o
       CC hyperloglog.o
       CC latency.o
       CC sparkline.o
       CC redis-check-rdb.o
       CC redis-check-aof.o
       CC geo.o
       CC lazyfree.o
       CC module.o
       CC evict.o
       CC expire.o
       CC geohash.o
       CC geohash_helper.o
       CC childinfo.o
       CC defrag.o
       CC siphash.o
       CC rax.o
       CC t_stream.o
       CC listpack.o
       CC localtime.o
       CC lolwut.o
       CC lolwut5.o
       CC lolwut6.o
       CC acl.o
       CC gopher.o
       CC tracking.o
       CC connection.o
       CC tls.o
       CC sha256.o
       CC timeout.o
       CC setcpuaffinity.o
       LINK redis-server
       INSTALL redis-sentinel
       CC redis-cli.o
       LINK redis-cli
       CC redis-benchmark.o
       LINK redis-benchmark
       INSTALL redis-check-rdb
       INSTALL redis-check-aof

   Hint: It's a good idea to run 'make test' ;)

   Redis-cli installed successfully.
   Installing ElasticSearch...
   Downloading and untarring file elasticsearch-7.10.1 to ../oppia_tools ...
   Download of elasticsearch-7.10.1 succeeded.
   ElasticSearch installed successfully.
   Copying Google Cloud SDK modules to third_party/python_libs...
   Checking that all google library modules contain __init__.py files...
   yarn install v1.22.10
   [1/4] 🔍  Resolving packages...
   [2/4] 🚚  Fetching packages...
   warning Pattern ["@definitelytyped/typescript-versions@latest"] is trying to unpack in the same destination "/Users/user/Library/Caches/Yarn/v6/npm-@definitelytyped-typescript-versions-0.0.80-f4216d3cc81d61555a681b15c965fbbcd70ddc91-integrity/node_modules/@definitelytyped/typescript-versions" as pattern ["@definitelytyped/typescript-versions@^0.0.80","@definitelytyped/typescript-versions@^0.0.80","@definitelytyped/typescript-versions@^0.0.80"]. This could result in non-deterministic behavior, skipping.
   [3/4] 🔗  Linking dependencies...
   warning " > @asymmetrik/ngx-leaflet@8.1.0" has unmet peer dependency "tslib@2".
   warning " > @ng-bootstrap/ng-bootstrap@8.0.4" has unmet peer dependency "@angular/localize@^10.0.0".
   warning " > bootstrap@4.6.0" has unmet peer dependency "popper.js@^1.16.1".
   warning "firebase-admin > @firebase/database > @firebase/auth-interop-types@0.1.5" has unmet peer dependency "@firebase/app-types@0.x".
   [4/4] 🔨  Building fresh packages...
   ✨  Done in 782.82s.
   Installing buf and protoc binary.
   Compiling protobuf files.

   Installing pre-commit hook for git
   Created symlink in .git/hooks directory
   Making pre-commit hook file executable ...
   pre-commit hook file is now executable!
   Installing pre-push hook for git
   Created symlink in .git/hooks directory
   Making pre-push hook file executable ...
   pre-push hook file is now executable!
   Building third party libs at third_party/generated/
   Starting new Redis Server: /opensource/oppia/../oppia_tools/redis-cli-6.0.10/src/redis-server redis.conf
   Starting new ElasticSearch Server: /opensource/oppia/../oppia_tools/elasticsearch-7.10.1/bin/elasticsearch -q
   Starting new Firebase Emulator: /opensource/oppia/node_modules/firebase-tools/lib/bin/firebase.js emulators:start --only auth --project dev-project-id --config .firebase.json --export-on-exit /opensource/oppia/../firebase_emulator_cache
   ⚠  emulators: You are not currently authenticated so some features may not work correctly. Please run firebase login to authenticate the CLI.
   i  emulators: Starting emulators: auth
   ⚠  emulators: It seems that you are running multiple instances of the emulator suite for project dev-project-id. This may result in unexpected behavior.
   ⚠  ui: Emulator UI unable to start on port 4000, starting on 4001 instead.
   i  ui: Emulator UI logging to ui-debug.log

   ┌─────────────────────────────────────────────────────────────┐
   │ ✔  All emulators ready! It is now safe to connect your app. │
   │ i  View Emulator UI at http://localhost:4001                │
   └─────────────────────────────────────────────────────────────┘

   ┌────────────────┬────────────────┬────────────────────────────┐
   │ Emulator       │ Host:Port      │ View in Emulator UI        │
   ├────────────────┼────────────────┼────────────────────────────┤
   │ Authentication │ localhost:9099 │ http://localhost:4001/auth │
   └────────────────┴────────────────┴────────────────────────────┘
     Emulator Hub running at localhost:4400
     Other reserved ports: 4500

   Issues? Report them at https://github.com/firebase/firebase-tools/issues and attach the *-debug.log files.

   Starting new Webpack Compiler: /opensource/oppia/../oppia_tools/node-14.15.0/bin/node /opensource/oppia/node_modules/webpack/bin/webpack.js --config webpack.dev.config.ts --color --watch --progress
   10% building 0/0 modules 0 active
   webpack is watching the files…

   Hash: e6d5bec1376a7fe0428b
   Version: webpack 4.46.0
   Time: 68495ms
   Built at: 07/17/2021 5:40:56 PM
   Starting new GAE Development Server: /Users/user/.pyenv/versions/oppia-tmp/bin/python /opensource/oppia_tools/google-cloud-sdk-335.0.0/google-cloud-sdk/platform/google_appengine/dev_appserver.py --host 0.0.0.0 --port 8181 --admin_host 0.0.0.0 --admin_port 8000 --clear_datastore true --enable_console false --enable_host_checking true --automatic_restart true --skip_sdk_update_check true --log_level info --dev_appserver_log_level info app_dev.yaml
                                                                                                                     Asset      Size                                                                                                         Chunks             Chunk Names
                                                                                                  about-page.mainpage.html  5.15 KiB                                                                                                                 [emitted]
                                                                                                           about.bundle.js  63.4 KiB                                                                                                          about  [emitted]  about
   about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js   6.4 MiB  about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277  [emitted]  about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277
   about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js  16.8 KiB  about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240  [emitted]  about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240
                                                                                                  admin-page.mainpage.html  3.53 KiB                                                                                                                 [emitted]
                                                                                                           admin.bundle.js   198 KiB                                                                                                          admin  [emitted]  admin
                                                                                              classroom-page.mainpage.html  5.21 KiB                                                                                                                 [emitted]
                                                                                                       classroom.bundle.js  26.5 KiB                                                                                                      classroom  [emitted]  classroom
                             classroom~exploration_player~practice_session~review_test~skill_editor~topic_editor.bundle.js  20.8 KiB                            classroom~exploration_player~practice_session~review_test~skill_editor~topic_editor  [emitted]  classroom~exploration_player~practice_session~review_test~skill_editor~topic_editor
                                                                                               classroom~library.bundle.js  36.6 KiB                                                                                              classroom~library  [emitted]  classroom~library
                                                                                      collection-editor-page.mainpage.html  5.36 KiB                                                                                                                 [emitted]
                                                                                      collection-player-page.mainpage.html  7.13 KiB                                                                                                                 [emitted]
                                                                                               collection_editor.bundle.js   125 KiB                                                                                              collection_editor  [emitted]  collection_editor
   collection_editor~contributor_dashboard~exploration_editor~preferences~skill_editor~topic_editor~top~29bde881.bundle.js  78.9 KiB  collection_editor~contributor_dashboard~exploration_editor~preferences~skill_editor~topic_editor~top~29bde881  [emitted]  collection_editor~contributor_dashboard~exploration_editor~preferences~skill_editor~topic_editor~top~29bde881
                            collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js   137 KiB                           collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor  [emitted]  collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor
                                                                                               collection_player.bundle.js    80 KiB                                                                                              collection_player  [emitted]  collection_player
                                                                                                  console_errors.bundle.js  28.5 KiB                                                                                                 console_errors  [emitted]  console_errors
                                                                                                       console_errors.html  4.86 KiB                                                                                                                 [emitted]
                                                                                                contact-page.mainpage.html  4.89 KiB                                                                                                                 [emitted]
                                                                                                         contact.bundle.js  35.5 KiB                                                                                                        contact  [emitted]  contact
                                                                                  contributor-dashboard-page.mainpage.html  6.65 KiB                                                                                                                 [emitted]
                                                                                           contributor_dashboard.bundle.js   238 KiB                                                                                          contributor_dashboard  [emitted]  contributor_dashboard
   contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js   334 KiB  contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33  [emitted]  contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33
         contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js   525 KiB        contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor  [emitted]  contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor
               contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js   181 KiB              contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor  [emitted]  contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor
   contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js   260 KiB  contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53  [emitted]  contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53
                                              contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js  1.15 MiB                                             contributor_dashboard~exploration_editor~skill_editor~topic_editor  [emitted]  contributor_dashboard~exploration_editor~skill_editor~topic_editor
                                                                 contributor_dashboard~skill_editor~topic_editor.bundle.js  36.6 KiB                                                                contributor_dashboard~skill_editor~topic_editor  [emitted]  contributor_dashboard~skill_editor~topic_editor
                                     contributor_dashboard~skill_editor~topic_editor~topics_and_skills_dashboard.bundle.js  37.1 KiB                                    contributor_dashboard~skill_editor~topic_editor~topics_and_skills_dashboard  [emitted]  contributor_dashboard~skill_editor~topic_editor~topics_and_skills_dashboard
                                                                                      creator-dashboard-page.mainpage.html  5.86 KiB                                                                                                                 [emitted]
                                                                                               creator_dashboard.bundle.js   106 KiB                                                                                              creator_dashboard  [emitted]  creator_dashboard
                                                                                         delete-account-page.mainpage.html  4.93 KiB                                                                                                                 [emitted]
                                                                                                  delete_account.bundle.js  37.6 KiB                                                                                                 delete_account  [emitted]  delete_account
                                                                                                 donate-page.mainpage.html  4.89 KiB                                                                                                                 [emitted]
                                                                                                          donate.bundle.js  42.5 KiB                                                                                                         donate  [emitted]  donate
                                                                                        email-dashboard-page.mainpage.html  5.04 KiB                                                                                                                 [emitted]
                                                                                      email-dashboard-result.mainpage.html  4.95 KiB                                                                                                                 [emitted]
                                                                                                 email_dashboard.bundle.js  39.6 KiB                                                                                                email_dashboard  [emitted]  email_dashboard
                                                                                          email_dashboard_result.bundle.js  39.3 KiB                                                                                         email_dashboard_result  [emitted]  email_dashboard_result
                                                                                               error-iframed.mainpage.html  6.04 KiB                                                                                                                 [emitted]
                                                                                              error-page-400.mainpage.html  4.59 KiB                                                                                                                 [emitted]
                                                                                              error-page-401.mainpage.html  4.59 KiB                                                                                                                 [emitted]
                                                                                              error-page-404.mainpage.html  4.59 KiB                                                                                                                 [emitted]
                                                                                              error-page-500.mainpage.html  4.59 KiB                                                                                                                 [emitted]
                                                                                                           error.bundle.js  36.7 KiB                                                                                                          error  [emitted]  error
                                                                                     exploration-editor-page.mainpage.html  13.4 KiB                                                                                                                 [emitted]
                                                                                     exploration-player-page.mainpage.html  8.11 KiB                                                                                                                 [emitted]
                                                                                              exploration_editor.bundle.js  69.5 KiB                                                                                             exploration_editor  [emitted]  exploration_editor
                                                                           exploration_editor~exploration_player.bundle.js  1.17 MiB                                                                          exploration_editor~exploration_player  [emitted]  exploration_editor~exploration_player
                                 exploration_editor~exploration_player~practice_session~review_test~skill_editor.bundle.js  18.5 KiB                                exploration_editor~exploration_player~practice_session~review_test~skill_editor  [emitted]  exploration_editor~exploration_player~practice_session~review_test~skill_editor
                                                                                              exploration_player.bundle.js  38.3 KiB                                                                                             exploration_player  [emitted]  exploration_player
                                                    exploration_player~practice_session~review_test~skill_editor.bundle.js  57.5 KiB                                                   exploration_player~practice_session~review_test~skill_editor  [emitted]  exploration_player~practice_session~review_test~skill_editor
                                                                                            get-started-page.mainpage.html  7.46 KiB                                                                                                                 [emitted]
                                                                                                     get_started.bundle.js  28.7 KiB                                                                                                    get_started  [emitted]  get_started
                                                                                                         landing.bundle.js  51.1 KiB                                                                                                        landing  [emitted]  landing
                                                                                      learner-dashboard-page.mainpage.html  5.53 KiB                                                                                                                 [emitted]
                                                                                               learner_dashboard.bundle.js   124 KiB                                                                                              learner_dashboard  [emitted]  learner_dashboard
                                                                                                library-page.mainpage.html  5.53 KiB                                                                                                                 [emitted]
                                                                                                         library.bundle.js  78.1 KiB                                                                                                        library  [emitted]  library
                                                                                                  login-page.mainpage.html  5.02 KiB                                                                                                                 [emitted]
                                                                                                           login.bundle.js  33.1 KiB                                                                                                          login  [emitted]  login
                                                                                                 logout-page.mainpage.html  4.91 KiB                                                                                                                 [emitted]
                                                                                                          logout.bundle.js  34.4 KiB                                                                                                         logout  [emitted]  logout
                                                                                            maintenance-page.mainpage.html  3.55 KiB                                                                                                                 [emitted]
                                                                                                     maintenance.bundle.js  36.6 KiB                                                                                                    maintenance  [emitted]  maintenance
                                                                                              moderator-page.mainpage.html  4.95 KiB                                                                                                                 [emitted]
                                                                                                       moderator.bundle.js  44.3 KiB                                                                                                      moderator  [emitted]  moderator
                                                                                notifications-dashboard-page.mainpage.html  4.89 KiB                                                                                                                 [emitted]
                                                                                         notifications_dashboard.bundle.js  40.8 KiB                                                                                        notifications_dashboard  [emitted]  notifications_dashboard
                                                                               pending-account-deletion-page.mainpage.html  5.15 KiB                                                                                                                 [emitted]
                                                                                        pending_account_deletion.bundle.js  34.8 KiB                                                                                       pending_account_deletion  [emitted]  pending_account_deletion
                                                                                                        playbook.bundle.js  39.6 KiB                                                                                                       playbook  [emitted]  playbook
                                                                                                    playbook.mainpage.html  4.77 KiB                                                                                                                 [emitted]
                                                                                       practice-session-page.mainpage.html  6.09 KiB                                                                                                                 [emitted]
                                                                                                practice_session.bundle.js  30.2 KiB                                                                                               practice_session  [emitted]  practice_session
                                                                       practice_session~review_test~skill_editor.bundle.js    75 KiB                                                                      practice_session~review_test~skill_editor  [emitted]  practice_session~review_test~skill_editor
                                                                                            preferences-page.mainpage.html  5.27 KiB                                                                                                                 [emitted]
                                                                                                     preferences.bundle.js  54.9 KiB                                                                                                    preferences  [emitted]  preferences
                                                                                                privacy-page.mainpage.html  4.86 KiB                                                                                                                 [emitted]
                                                                                                         privacy.bundle.js  52.4 KiB                                                                                                        privacy  [emitted]  privacy
                                                                                                profile-page.mainpage.html  11.7 KiB                                                                                                                 [emitted]
                                                                                                         profile.bundle.js  58.5 KiB                                                                                                        profile  [emitted]  profile
                                                                                            review-test-page.mainpage.html     6 KiB                                                                                                                 [emitted]
                                                                                                     review_test.bundle.js  29.3 KiB                                                                                                    review_test  [emitted]  review_test
                                                                                                         runtime.bundle.js  6.12 KiB                                                                                                        runtime  [emitted]  runtime
                                                                                                 signup-page.mainpage.html  4.86 KiB                                                                                                                 [emitted]
                                                                                                          signup.bundle.js  49.5 KiB                                                                                                         signup  [emitted]  signup
                                                                                           skill-editor-page.mainpage.html   7.5 KiB                                                                                                                 [emitted]
                                                                                                    skill_editor.bundle.js   148 KiB                                                                                                   skill_editor  [emitted]  skill_editor
                                                                                       skill_editor~topic_editor.bundle.js  82.7 KiB                                                                                      skill_editor~topic_editor  [emitted]  skill_editor~topic_editor
                                                                                                 splash-page.mainpage.html  5.26 KiB                                                                                                                 [emitted]
                                                                                                          splash.bundle.js  64.4 KiB                                                                                                         splash  [emitted]  splash
                                                                                       stewards-landing-page.mainpage.html  4.65 KiB                                                                                                                 [emitted]
                                                                                                        stewards.bundle.js  68.8 KiB                                                                                                       stewards  [emitted]  stewards
                                                                                           story-editor-page.mainpage.html  5.69 KiB                                                                                                                 [emitted]
                                                                                           story-viewer-page.mainpage.html    12 KiB                                                                                                                 [emitted]
                                                                                                    story_editor.bundle.js   163 KiB                                                                                                   story_editor  [emitted]  story_editor
                                                           story_editor~topic_editor~topics_and_skills_dashboard.bundle.js  20.3 KiB                                                          story_editor~topic_editor~topics_and_skills_dashboard  [emitted]  story_editor~topic_editor~topics_and_skills_dashboard
                                                                                                    story_viewer.bundle.js    69 KiB                                                                                                   story_viewer  [emitted]  story_viewer
                                                                                        subtopic-viewer-page.mainpage.html  5.22 KiB                                                                                                                 [emitted]
                                                                                                 subtopic_viewer.bundle.js  51.7 KiB                                                                                                subtopic_viewer  [emitted]  subtopic_viewer
                                                                                                  teach-page.mainpage.html  4.73 KiB                                                                                                                 [emitted]
                                                                                                           teach.bundle.js  74.1 KiB                                                                                                          teach  [emitted]  teach
                                                                                                  terms-page.mainpage.html  4.95 KiB                                                                                                                 [emitted]
                                                                                                           terms.bundle.js  46.6 KiB                                                                                                          terms  [emitted]  terms
                                                                                                 thanks-page.mainpage.html  4.78 KiB                                                                                                                 [emitted]
                                                                                                          thanks.bundle.js  35.6 KiB                                                                                                         thanks  [emitted]  thanks
                                                                                           topic-editor-page.mainpage.html  7.32 KiB                                                                                                                 [emitted]
                                                                                          topic-landing-page.mainpage.html  4.71 KiB                                                                                                                 [emitted]
                                                                                           topic-viewer-page.mainpage.html  5.16 KiB                                                                                                                 [emitted]
                                                                                                    topic_editor.bundle.js   200 KiB                                                                                                   topic_editor  [emitted]  topic_editor
                                                                                       topic_editor~topic_viewer.bundle.js  29.7 KiB                                                                                      topic_editor~topic_viewer  [emitted]  topic_editor~topic_viewer
                                                                                                    topic_viewer.bundle.js  57.7 KiB                                                                                                   topic_viewer  [emitted]  topic_viewer
                                                                            topics-and-skills-dashboard-page.mainpage.html  5.63 KiB                                                                                                                 [emitted]
                                                                                     topics_and_skills_dashboard.bundle.js   191 KiB                                                                                    topics_and_skills_dashboard  [emitted]  topics_and_skills_dashboard
   vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js  13.9 MiB  vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6  [emitted]  vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6
   vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js  35.4 KiB  vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070  [emitted]  vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070
       vendors~contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js  1.01 MiB      vendors~contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor  [emitted]  vendors~contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor
                                      vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js  1.41 MiB                                     vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor  [emitted]  vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor
                                                                                                 vendors~library.bundle.js  19.8 KiB                                                                                                vendors~library  [emitted]  vendors~library
                                                                                                   vendors~login.bundle.js   418 KiB                                                                                                  vendors~login  [emitted]  vendors~login
                                                                                             vendors~preferences.bundle.js   133 KiB                                                                                            vendors~preferences  [emitted]  vendors~preferences
                                                                             vendors~topics_and_skills_dashboard.bundle.js  24.2 KiB                                                                            vendors~topics_and_skills_dashboard  [emitted]  vendors~topics_and_skills_dashboard
   Entrypoint about = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js about.bundle.js
   Entrypoint admin = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js admin.bundle.js
   Entrypoint classroom = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js classroom~exploration_player~practice_session~review_test~skill_editor~topic_editor.bundle.js classroom~library.bundle.js classroom.bundle.js
   Entrypoint collection_editor = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js collection_editor~contributor_dashboard~exploration_editor~preferences~skill_editor~topic_editor~top~29bde881.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js collection_editor.bundle.js
   Entrypoint collection_player = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js collection_player.bundle.js
   Entrypoint contact = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js contact.bundle.js
   Entrypoint console_errors = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js console_errors.bundle.js
   Entrypoint creator_dashboard = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js vendors~contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js creator_dashboard.bundle.js
   Entrypoint contributor_dashboard = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js vendors~contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js collection_editor~contributor_dashboard~exploration_editor~preferences~skill_editor~topic_editor~top~29bde881.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js contributor_dashboard~skill_editor~topic_editor~topics_and_skills_dashboard.bundle.js contributor_dashboard~skill_editor~topic_editor.bundle.js contributor_dashboard.bundle.js
   Entrypoint delete_account = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js delete_account.bundle.js
   Entrypoint donate = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js donate.bundle.js
   Entrypoint email_dashboard = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js email_dashboard.bundle.js
   Entrypoint email_dashboard_result = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js email_dashboard_result.bundle.js
   Entrypoint error = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js error.bundle.js
   Entrypoint exploration_editor = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js vendors~contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js collection_editor~contributor_dashboard~exploration_editor~preferences~skill_editor~topic_editor~top~29bde881.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js exploration_editor~exploration_player~practice_session~review_test~skill_editor.bundle.js contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js exploration_editor~exploration_player.bundle.js exploration_editor.bundle.js
   Entrypoint exploration_player = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js classroom~exploration_player~practice_session~review_test~skill_editor~topic_editor.bundle.js exploration_editor~exploration_player~practice_session~review_test~skill_editor.bundle.js exploration_player~practice_session~review_test~skill_editor.bundle.js exploration_editor~exploration_player.bundle.js exploration_player.bundle.js
   Entrypoint get_started = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js get_started.bundle.js
   Entrypoint landing = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js landing.bundle.js
   Entrypoint learner_dashboard = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js learner_dashboard.bundle.js
   Entrypoint library = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js vendors~library.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js classroom~library.bundle.js library.bundle.js
   Entrypoint login = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~login.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js login.bundle.js
   Entrypoint logout = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js logout.bundle.js
   Entrypoint maintenance = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js maintenance.bundle.js
   Entrypoint moderator = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js moderator.bundle.js
   Entrypoint notifications_dashboard = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js notifications_dashboard.bundle.js
   Entrypoint pending_account_deletion = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js pending_account_deletion.bundle.js
   Entrypoint playbook = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js playbook.bundle.js
   Entrypoint practice_session = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js classroom~exploration_player~practice_session~review_test~skill_editor~topic_editor.bundle.js exploration_editor~exploration_player~practice_session~review_test~skill_editor.bundle.js exploration_player~practice_session~review_test~skill_editor.bundle.js practice_session~review_test~skill_editor.bundle.js practice_session.bundle.js
   Entrypoint privacy = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js privacy.bundle.js
   Entrypoint preferences = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~preferences.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js collection_editor~contributor_dashboard~exploration_editor~preferences~skill_editor~topic_editor~top~29bde881.bundle.js preferences.bundle.js
   Entrypoint profile = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js profile.bundle.js
   Entrypoint review_test = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js classroom~exploration_player~practice_session~review_test~skill_editor~topic_editor.bundle.js exploration_editor~exploration_player~practice_session~review_test~skill_editor.bundle.js exploration_player~practice_session~review_test~skill_editor.bundle.js practice_session~review_test~skill_editor.bundle.js review_test.bundle.js
   Entrypoint signup = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js signup.bundle.js
   Entrypoint skill_editor = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js vendors~contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js collection_editor~contributor_dashboard~exploration_editor~preferences~skill_editor~topic_editor~top~29bde881.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js classroom~exploration_player~practice_session~review_test~skill_editor~topic_editor.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js exploration_editor~exploration_player~practice_session~review_test~skill_editor.bundle.js contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js exploration_player~practice_session~review_test~skill_editor.bundle.js contributor_dashboard~skill_editor~topic_editor~topics_and_skills_dashboard.bundle.js practice_session~review_test~skill_editor.bundle.js contributor_dashboard~skill_editor~topic_editor.bundle.js skill_editor~topic_editor.bundle.js skill_editor.bundle.js
   Entrypoint splash = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js splash.bundle.js
   Entrypoint stewards = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js stewards.bundle.js
   Entrypoint story_editor = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js vendors~contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js story_editor~topic_editor~topics_and_skills_dashboard.bundle.js story_editor.bundle.js
   Entrypoint story_viewer = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js story_viewer.bundle.js
   Entrypoint subtopic_viewer = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js subtopic_viewer.bundle.js
   Entrypoint teach = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js teach.bundle.js
   Entrypoint terms = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js terms.bundle.js
   Entrypoint thanks = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js thanks.bundle.js
   Entrypoint topic_editor = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js vendors~contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js collection_editor~contributor_dashboard~exploration_editor~preferences~skill_editor~topic_editor~top~29bde881.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js classroom~exploration_player~practice_session~review_test~skill_editor~topic_editor.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js contributor_dashboard~skill_editor~topic_editor~topics_and_skills_dashboard.bundle.js contributor_dashboard~skill_editor~topic_editor.bundle.js story_editor~topic_editor~topics_and_skills_dashboard.bundle.js skill_editor~topic_editor.bundle.js topic_editor~topic_viewer.bundle.js topic_editor.bundle.js
   Entrypoint topics_and_skills_dashboard = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js vendors~topics_and_skills_dashboard.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js collection_editor~contributor_dashboard~exploration_editor~preferences~skill_editor~topic_editor~top~29bde881.bundle.js contributor_dashboard~skill_editor~topic_editor~topics_and_skills_dashboard.bundle.js story_editor~topic_editor~topics_and_skills_dashboard.bundle.js topics_and_skills_dashboard.bundle.js
   Entrypoint topic_viewer = runtime.bundle.js vendors~about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor~70d590c6.bundle.js vendors~admin~collection_editor~collection_player~contributor_dashboard~creator_dashboard~exploratio~c684e070.bundle.js about~admin~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboa~9e03f277.bundle.js about~classroom~collection_editor~collection_player~console_errors~contact~contributor_dashboard~cre~45ee5240.bundle.js topic_editor~topic_viewer.bundle.js topic_viewer.bundle.js
   [./core/templates/pages/about-page/about-page.import.ts] 1.21 KiB {about} [built]
   [./core/templates/pages/admin-page/admin-page.import.ts] 1.3 KiB {admin} [built]
   [./core/templates/pages/classroom-page/classroom-page.import.ts] 1.26 KiB {classroom} [built]
   [./core/templates/pages/collection-editor-page/collection-editor-page.import.ts] 1.6 KiB {collection_editor} [built]
   [./core/templates/pages/collection-player-page/collection-player-page.import.ts] 1.7 KiB {collection_player} [built]
   [./core/templates/pages/contact-page/contact-page.import.ts] 1.22 KiB {contact} [built]
   [./core/templates/pages/contributor-dashboard-page/contributor-dashboard-page.import.ts] 1.36 KiB {contributor_dashboard} [built]
   [./core/templates/pages/creator-dashboard-page/creator-dashboard-page.import.ts] 1.41 KiB {creator_dashboard} [built]
   [./core/templates/pages/delete-account-page/delete-account-page.import.ts] 1.21 KiB {delete_account} [built]
   [./core/templates/pages/donate-page/donate-page.import.ts] 1.21 KiB {donate} [built]
   [./core/templates/pages/email-dashboard-pages/email-dashboard-page.import.ts] 1.26 KiB {email_dashboard} [built]
   [./core/templates/pages/email-dashboard-pages/email-dashboard-result.import.ts] 1.26 KiB {email_dashboard_result} [built]
   [./core/templates/pages/error-pages/error-page.import.ts] 1.2 KiB {error} [built]
   [./core/templates/pages/exploration-editor-page/exploration-editor-page.import.ts] 2.08 KiB {exploration_editor} [built]
   [./core/templates/pages/exploration-player-page/exploration-player-page.import.ts] 1.92 KiB {exploration_player} [built]
       + 3661 hidden modules

   WARNING in ./core/templates/components/skill-selector/skill-selector.component.ts 200:50-67
   "export 'CategorizedSkills' was not found in 'domain/topics_and_skills_dashboard/topics-and-skills-dashboard-backend-api.service'
    @ ./extensions/objects/templates/skill-selector-editor.directive.ts
    @ ./extensions/objects/objectComponentsRequires.ts
    @ ./core/templates/pages/story-editor-page/story-editor-page.component.ts
    @ ./core/templates/pages/story-editor-page/story-editor-page.import.ts

   WARNING in ./core/templates/components/skill-selector/skill-selector.component.ts 200:87-104
   "export 'CategorizedSkills' was not found in 'domain/topics_and_skills_dashboard/topics-and-skills-dashboard-backend-api.service'
    @ ./extensions/objects/templates/skill-selector-editor.directive.ts
    @ ./extensions/objects/objectComponentsRequires.ts
    @ ./core/templates/pages/story-editor-page/story-editor-page.component.ts
    @ ./core/templates/pages/story-editor-page/story-editor-page.import.ts

   WARNING in ./core/templates/components/summary-tile/exploration-summary-tile.component.ts 175:50-68
   "export 'ExplorationRatings' was not found in 'domain/summary/learner-exploration-summary.model'
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/topics-and-skills-dashboard-page/topics-and-skills-dashboard-page.module.ts
    @ ./core/templates/pages/topics-and-skills-dashboard-page/topics-and-skills-dashboard-page.import.ts

   WARNING in ./core/templates/components/summary-tile/exploration-summary-tile.component.ts 175:88-106
   "export 'ExplorationRatings' was not found in 'domain/summary/learner-exploration-summary.model'
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/topics-and-skills-dashboard-page/topics-and-skills-dashboard-page.module.ts
    @ ./core/templates/pages/topics-and-skills-dashboard-page/topics-and-skills-dashboard-page.import.ts

   WARNING in ./extensions/interactions/GraphInput/directives/oppia-interactive-graph-input.component.ts 170:50-61
   "export 'GraphAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/GraphInput/graph-input-interactions.module.ts
    @ ./extensions/objects/object-components.module.ts
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/topics-and-skills-dashboard-page/topics-and-skills-dashboard-page.module.ts
    @ ./core/templates/pages/topics-and-skills-dashboard-page/topics-and-skills-dashboard-page.import.ts

   WARNING in ./extensions/interactions/GraphInput/directives/oppia-interactive-graph-input.component.ts 170:81-92
   "export 'GraphAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/GraphInput/graph-input-interactions.module.ts
    @ ./extensions/objects/object-components.module.ts
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/topics-and-skills-dashboard-page/topics-and-skills-dashboard-page.module.ts
    @ ./core/templates/pages/topics-and-skills-dashboard-page/topics-and-skills-dashboard-page.import.ts

   WARNING in ./extensions/interactions/GraphInput/directives/graph-viz.component.ts 580:50-61
   "export 'GraphAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/GraphInput/graph-input-interactions.module.ts
    @ ./extensions/objects/object-components.module.ts
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/topics-and-skills-dashboard-page/topics-and-skills-dashboard-page.module.ts
    @ ./core/templates/pages/topics-and-skills-dashboard-page/topics-and-skills-dashboard-page.import.ts

   WARNING in ./extensions/interactions/GraphInput/directives/graph-viz.component.ts 580:81-92
   "export 'GraphAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/GraphInput/graph-input-interactions.module.ts
    @ ./extensions/objects/object-components.module.ts
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/topics-and-skills-dashboard-page/topics-and-skills-dashboard-page.module.ts
    @ ./core/templates/pages/topics-and-skills-dashboard-page/topics-and-skills-dashboard-page.import.ts

   WARNING in ./core/templates/components/skill-selector/skill-selector.component.ts 188:50-71
   "export 'GroupedSkillSummaries' was not found in 'pages/skill-editor-page/services/skill-editor-state.service'
    @ ./extensions/objects/templates/skill-selector-editor.directive.ts
    @ ./extensions/objects/objectComponentsRequires.ts
    @ ./core/templates/pages/story-editor-page/story-editor-page.component.ts
    @ ./core/templates/pages/story-editor-page/story-editor-page.import.ts

   WARNING in ./core/templates/components/skill-selector/skill-selector.component.ts 188:91-112
   "export 'GroupedSkillSummaries' was not found in 'pages/skill-editor-page/services/skill-editor-state.service'
    @ ./extensions/objects/templates/skill-selector-editor.directive.ts
    @ ./extensions/objects/objectComponentsRequires.ts
    @ ./core/templates/pages/story-editor-page/story-editor-page.component.ts
    @ ./core/templates/pages/story-editor-page/story-editor-page.import.ts

   WARNING in ./extensions/interactions/ImageClickInput/directives/oppia-interactive-image-click-input.component.ts 233:50-66
   "export 'ImageClickAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/ImageClickInput/image-click-input-interactions.module.ts
    @ ./extensions/interactions/interactions.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts

   WARNING in ./extensions/interactions/ImageClickInput/directives/oppia-interactive-image-click-input.component.ts 233:86-102
   "export 'ImageClickAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/ImageClickInput/image-click-input-interactions.module.ts
    @ ./extensions/interactions/interactions.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts

   WARNING in ./extensions/interactions/AlgebraicExpressionInput/directives/oppia-interactive-algebraic-expression-input.component.ts 120:50-67
   "export 'InteractionAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/AlgebraicExpressionInput/algebraic-expression-input-interactions.module.ts
    @ ./extensions/interactions/interactions.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts

   WARNING in ./extensions/interactions/AlgebraicExpressionInput/directives/oppia-interactive-algebraic-expression-input.component.ts 120:87-104
   "export 'InteractionAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/AlgebraicExpressionInput/algebraic-expression-input-interactions.module.ts
    @ ./extensions/interactions/interactions.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts

   WARNING in ./extensions/interactions/FractionInput/directives/oppia-interactive-fraction-input.component.ts 200:50-67
   "export 'InteractionAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/FractionInput/fraction-input-interactions.module.ts
    @ ./extensions/interactions/interactions.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts

   WARNING in ./extensions/interactions/FractionInput/directives/oppia-interactive-fraction-input.component.ts 200:87-104
   "export 'InteractionAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/FractionInput/fraction-input-interactions.module.ts
    @ ./extensions/interactions/interactions.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts

   WARNING in ./node_modules/d3-scale/src/time.js 70:45-61
   "export 'timeTickInterval' was not found in 'd3-time'
    @ ./node_modules/d3-scale/src/index.js
    @ ./extensions/visualizations/oppia-visualization-click-hexbins.directive.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/templates/state-stats-modal.controller.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/statistics-tab.component.ts
    @ ./core/templates/pages/exploration-editor-page/exploration-editor-page.component.ts
    @ ./core/templates/pages/exploration-editor-page/exploration-editor-page.import.ts

   WARNING in ./node_modules/d3-scale/src/time.js 70:34-43
   "export 'timeTicks' was not found in 'd3-time'
    @ ./node_modules/d3-scale/src/index.js
    @ ./extensions/visualizations/oppia-visualization-click-hexbins.directive.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/templates/state-stats-modal.controller.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/statistics-tab.component.ts
    @ ./core/templates/pages/exploration-editor-page/exploration-editor-page.component.ts
    @ ./core/templates/pages/exploration-editor-page/exploration-editor-page.import.ts

   WARNING in ./node_modules/d3-scale/src/utcTime.js 7:44-59
   "export 'utcTickInterval' was not found in 'd3-time'
    @ ./node_modules/d3-scale/src/index.js
    @ ./extensions/visualizations/oppia-visualization-click-hexbins.directive.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/templates/state-stats-modal.controller.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/statistics-tab.component.ts
    @ ./core/templates/pages/exploration-editor-page/exploration-editor-page.component.ts
    @ ./core/templates/pages/exploration-editor-page/exploration-editor-page.import.ts

   WARNING in ./node_modules/d3-scale/src/utcTime.js 7:34-42
   "export 'utcTicks' was not found in 'd3-time'
    @ ./node_modules/d3-scale/src/index.js
    @ ./extensions/visualizations/oppia-visualization-click-hexbins.directive.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/templates/state-stats-modal.controller.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/statistics-tab.component.ts
    @ ./core/templates/pages/exploration-editor-page/exploration-editor-page.component.ts
    @ ./core/templates/pages/exploration-editor-page/exploration-editor-page.import.ts

   WARNING in ./node_modules/@angular/core/fesm2015/core.js 28642:15-36
   Critical dependency: the request of a dependency is an expression
    @ ./core/templates/pages/story-editor-page/story-editor-page.module.ts
    @ ./core/templates/pages/story-editor-page/story-editor-page.import.ts

   WARNING in ./node_modules/@angular/core/fesm2015/core.js 28654:15-102
   Critical dependency: the request of a dependency is an expression
    @ ./core/templates/pages/story-editor-page/story-editor-page.module.ts
    @ ./core/templates/pages/story-editor-page/story-editor-page.import.ts

   WARNING in ./node_modules/@angular/core/fesm2015/core.js 28642:15-36
   System.import() is deprecated and will be removed soon. Use import() instead.
   For more info visit https://webpack.js.org/guides/code-splitting/
    @ ./core/templates/pages/story-editor-page/story-editor-page.module.ts 32:0-58 47:4-12 68:25-40
    @ ./core/templates/pages/story-editor-page/story-editor-page.import.ts

   WARNING in ./node_modules/@angular/core/fesm2015/core.js 28654:15-102
   System.import() is deprecated and will be removed soon. Use import() instead.
   For more info visit https://webpack.js.org/guides/code-splitting/
    @ ./core/templates/pages/story-editor-page/story-editor-page.module.ts 32:0-58 47:4-12 68:25-40
    @ ./core/templates/pages/story-editor-page/story-editor-page.import.ts
   Child HtmlWebpackCompiler:
        46 assets
       Entrypoint HtmlWebpackPlugin_0 = __child-HtmlWebpackPlugin_0
       Entrypoint HtmlWebpackPlugin_1 = __child-HtmlWebpackPlugin_1
       Entrypoint HtmlWebpackPlugin_2 = __child-HtmlWebpackPlugin_2
       Entrypoint HtmlWebpackPlugin_3 = __child-HtmlWebpackPlugin_3
       Entrypoint HtmlWebpackPlugin_4 = __child-HtmlWebpackPlugin_4
       Entrypoint HtmlWebpackPlugin_5 = __child-HtmlWebpackPlugin_5
       Entrypoint HtmlWebpackPlugin_6 = __child-HtmlWebpackPlugin_6
       Entrypoint HtmlWebpackPlugin_7 = __child-HtmlWebpackPlugin_7
       Entrypoint HtmlWebpackPlugin_8 = __child-HtmlWebpackPlugin_8
       Entrypoint HtmlWebpackPlugin_9 = __child-HtmlWebpackPlugin_9
       Entrypoint HtmlWebpackPlugin_10 = __child-HtmlWebpackPlugin_10
       Entrypoint HtmlWebpackPlugin_11 = __child-HtmlWebpackPlugin_11
       Entrypoint HtmlWebpackPlugin_12 = __child-HtmlWebpackPlugin_12
       Entrypoint HtmlWebpackPlugin_13 = __child-HtmlWebpackPlugin_13
       Entrypoint HtmlWebpackPlugin_14 = __child-HtmlWebpackPlugin_14
       Entrypoint HtmlWebpackPlugin_15 = __child-HtmlWebpackPlugin_15
       Entrypoint HtmlWebpackPlugin_16 = __child-HtmlWebpackPlugin_16
       Entrypoint HtmlWebpackPlugin_17 = __child-HtmlWebpackPlugin_17
       Entrypoint HtmlWebpackPlugin_18 = __child-HtmlWebpackPlugin_18
       Entrypoint HtmlWebpackPlugin_19 = __child-HtmlWebpackPlugin_19
       Entrypoint HtmlWebpackPlugin_20 = __child-HtmlWebpackPlugin_20
       Entrypoint HtmlWebpackPlugin_21 = __child-HtmlWebpackPlugin_21
       Entrypoint HtmlWebpackPlugin_22 = __child-HtmlWebpackPlugin_22
       Entrypoint HtmlWebpackPlugin_23 = __child-HtmlWebpackPlugin_23
       Entrypoint HtmlWebpackPlugin_24 = __child-HtmlWebpackPlugin_24
       Entrypoint HtmlWebpackPlugin_25 = __child-HtmlWebpackPlugin_25
       Entrypoint HtmlWebpackPlugin_26 = __child-HtmlWebpackPlugin_26
       Entrypoint HtmlWebpackPlugin_27 = __child-HtmlWebpackPlugin_27
       Entrypoint HtmlWebpackPlugin_28 = __child-HtmlWebpackPlugin_28
       Entrypoint HtmlWebpackPlugin_29 = __child-HtmlWebpackPlugin_29
       Entrypoint HtmlWebpackPlugin_30 = __child-HtmlWebpackPlugin_30
       Entrypoint HtmlWebpackPlugin_31 = __child-HtmlWebpackPlugin_31
       Entrypoint HtmlWebpackPlugin_32 = __child-HtmlWebpackPlugin_32
       Entrypoint HtmlWebpackPlugin_33 = __child-HtmlWebpackPlugin_33
       Entrypoint HtmlWebpackPlugin_34 = __child-HtmlWebpackPlugin_34
       Entrypoint HtmlWebpackPlugin_35 = __child-HtmlWebpackPlugin_35
       Entrypoint HtmlWebpackPlugin_36 = __child-HtmlWebpackPlugin_36
       Entrypoint HtmlWebpackPlugin_37 = __child-HtmlWebpackPlugin_37
       Entrypoint HtmlWebpackPlugin_38 = __child-HtmlWebpackPlugin_38
       Entrypoint HtmlWebpackPlugin_39 = __child-HtmlWebpackPlugin_39
       Entrypoint HtmlWebpackPlugin_40 = __child-HtmlWebpackPlugin_40
       Entrypoint HtmlWebpackPlugin_41 = __child-HtmlWebpackPlugin_41
       Entrypoint HtmlWebpackPlugin_42 = __child-HtmlWebpackPlugin_42
       Entrypoint HtmlWebpackPlugin_43 = __child-HtmlWebpackPlugin_43
       Entrypoint HtmlWebpackPlugin_44 = __child-HtmlWebpackPlugin_44
       Entrypoint HtmlWebpackPlugin_45 = __child-HtmlWebpackPlugin_45
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/about-page/about-page.mainpage.html] 1.27 KiB {HtmlWebpackPlugin_0} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/admin-page/admin-page.mainpage.html] 872 bytes {HtmlWebpackPlugin_1} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/classroom-page/classroom-page.mainpage.html] 1.35 KiB {HtmlWebpackPlugin_2} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/collection-editor-page/collection-editor-page.mainpage.html] 1.28 KiB {HtmlWebpackPlugin_3} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/collection-player-page/collection-player-page.mainpage.html] 3.43 KiB {HtmlWebpackPlugin_4} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/contact-page/contact-page.mainpage.html] 1.3 KiB {HtmlWebpackPlugin_6} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/contributor-dashboard-page/contributor-dashboard-page.mainpage.html] 1.22 KiB {HtmlWebpackPlugin_8} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/creator-dashboard-page/creator-dashboard-page.mainpage.html] 1.42 KiB {HtmlWebpackPlugin_7} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/delete-account-page/delete-account-page.mainpage.html] 1.21 KiB {HtmlWebpackPlugin_9} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/donate-page/donate-page.mainpage.html] 1.28 KiB {HtmlWebpackPlugin_10} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/email-dashboard-pages/email-dashboard-page.mainpage.html] 1.43 KiB {HtmlWebpackPlugin_11} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/email-dashboard-pages/email-dashboard-result.mainpage.html] 1.32 KiB {HtmlWebpackPlugin_12} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/error-pages/error-iframed.mainpage.html] 2.46 KiB {HtmlWebpackPlugin_13} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/error-pages/error-page.mainpage.html] 1.03 KiB {HtmlWebpackPlugin_14} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/exploration-editor-page/exploration-editor-page.mainpage.html] 6.7 KiB {HtmlWebpackPlugin_15} [built]
           + 40 hidden modules
   INFO     2021-07-17 21:41:11,507 devappserver2.py:289] Skipping SDK update check.
   INFO     2021-07-17 21:41:12,407 api_server.py:282] Starting API server at: http://localhost:54536
   INFO     2021-07-17 21:41:12,431 dispatcher.py:267] Starting module "default" running at: http://0.0.0.0:8181
   INFO     2021-07-17 21:41:12,498 admin_server.py:150] Starting admin server at: http://0.0.0.0:8000
   INFORMATION

   Local development server is ready! Opening a default web browser window pointing to it: http://localhost:8181/

   Starting new Web Browser: open http://localhost:8181/
   /opensource/oppia_tools/google-cloud-sdk-335.0.0/google-cloud-sdk/platform/google_appengine/google/appengine/tools/devappserver2/mtime_file_watcher.py:182: UserWarning: There are too many files in your application for changes in all of them to be monitored. You may have to restart the development server to see some changes to your files.
     'There are too many files in your application for '
   INFO     2021-07-17 21:41:32,030 instance.py:294] Instance PID: 29320
   INFO     2021-07-17 21:41:56,313 module.py:865] default: "GET /_ah/warmup HTTP/1.1" 200 -
   ```
   </details>

  The first time you run this script, it will take a while (about 5 - 10 minutes when we last tested it in Dec 2018, though this depends on your Internet connection). Subsequent runs should be much faster. The `start.py` script downloads and installs the required dependencies (such as Google App Engine) if they are not already present, and sets up a development server for you to play with. The development server logs are then output to this terminal, so you will not be able to enter further commands in it until you disconnect the server.

  **Note**: **Please don't use `sudo` while installing.** It's not required, and using it may cause problems later. If you face permissions issues, ensure that you have the necessary permissions for the directory in which you're trying to set up Oppia. If you run into any other installation problems, please read [[these notes|Issues-with-installation?]]

  **Note**: The script will create a number of files and folders that are siblings of the `oppia/` root directory (e.g. `oppia_tools`). This is done so that these two folders will not be uploaded to App Engine when the application is deployed to the web.

  **Note**: If you run into errors while installing Oppia, please try deleting the directories

  ```text
  ../oppia_tools/
  node_modules/
  third_party/
  core/templates/prod/
  local_compiled_js/
  ```

  and running `start.py` again.

  **Note**: Oppia uses the npm tool to install some packages. This tool accesses both ~/tmp and ~/.npm, and has been known to occasionally encounter permissions issues with those directories. You may need to either delete these directories and all their contents (if they do not contain anything else that needs to be preserved), or change their permissions so that they are owned by you, which you can do by running

  ```
  sudo chown -R {{YOUR_USERNAME}} ~/tmp
  sudo chown -R {{YOUR_USERNAME}} ~/.npm
  ```

  where `{{YOUR_USERNAME}}` should be replaced by your username.

2. The `start.py` script will start a development server at http://localhost:8181. (If this doesn't happen automatically, try navigating directly to http://localhost:8181 in a browser once stuff stops being printed to the terminal.) It should look something like this:

   ![Image showing the default splash page.](https://res.cloudinary.com/dozmja9ir/image/upload/v1538254601/home_page.png)

   You can also view the App Engine admin console at http://localhost:8000.

   **Note:** There may be a few warnings that appear after running `start.py`. Don’t worry about these so long as you see the page once you go to http://localhost:8181. The script should continue to run so long as the development server is on (you’ll see a lot of lines that start with “INFO”) and you’re able to navigate to the page.


3. When you're done, you can shut down the development server by typing Ctrl+C into the terminal. **Then wait for a command prompt to appear.** Oppia has to shut down all the services it's started, and if you abort the graceful shutdown steps (e.g. by typing Ctrl+C many times), you may have trouble re-starting the server.

   <details>
   <summary>Example of shutdown output</summary>
   ```text
   ^CINFO     2021-07-17 21:50:08,043 shutdown.py:50] Shutting down.
   INFO     2021-07-17 21:50:08,043 stub_util.py:377] Applying all pending transactions and saving the datastore
   INFO     2021-07-17 21:50:08,044 stub_util.py:380] Saving search indexes

   i  emulators: Received SIGINT (Ctrl-C) for the first time. Starting a clean shutdown.
   i  emulators: Please wait for a clean shutdown or send the SIGINT (Ctrl-C) signal again to stop right now.
   i  Automatically exporting data using --export-on-exit "/opensource/oppia/../firebase_emulator_cache" please wait for the export to finish...


   Servers are shutting down, please wait for them to end gracefully!


   i  Found running emulator hub for project dev-project-id at http://localhost:4400
   i  Creating export directory /opensource/firebase_emulator_cache
   i  Exporting data to: /opensource/firebase_emulator_cache
   i  emulators: Received export request. Exporting data to /opensource/firebase_emulator_cache.
   ✔  emulators: Export complete.
   ✔  Export complete
   i  emulators: Shutting down emulators.
   i  ui: Stopping Emulator UI
   ⚠  Emulator UI has exited upon receiving signal: SIGINT
   i  auth: Stopping Authentication Emulator
   i  hub: Stopping emulator hub
   i  logging: Stopping Logging Emulator
   Stopping Web Browser(name="open", pid=29306)...
   Stopping GAE Development Server(name="python2.7", pid=29289)...
   Stopping Webpack Compiler(name="node", pid=29234)...
   Stopping Firebase Emulator(name="node", pid=29216)...
   Stopping ElasticSearch Server(name="java", pid=29148)...
   Stopping Redis Server(name="redis-server", pid=29147)...


   Done! Thank you for waiting.


   Traceback (most recent call last):
     File "/Users/user/.pyenv/versions/2.7.16/lib/python2.7/runpy.py", line 174, in _run_module_as_main
       "__main__", fname, loader, pkg_name)
     File "/Users/user/.pyenv/versions/2.7.16/lib/python2.7/runpy.py", line 72, in _run_code
       exec code in run_globals
     File "/opensource/oppia/scripts/start.py", line 205, in <module>
       main()
     File "/opensource/oppia/scripts/start.py", line 201, in main
       dev_appserver.wait()
     File "/opensource/oppia/../oppia_tools/psutil-5.7.3/psutil/__init__.py", line 1350, in wait
       ret = super(Popen, self).wait(timeout)
     File "/opensource/oppia/../oppia_tools/psutil-5.7.3/psutil/__init__.py", line 1259, in wait
       self._exitcode = self._proc.wait(timeout)
     File "/opensource/oppia/../oppia_tools/psutil-5.7.3/psutil/_psosx.py", line 342, in wrapper
       return fun(self, *args, **kwargs)
     File "/opensource/oppia/../oppia_tools/psutil-5.7.3/psutil/_psosx.py", line 550, in wait
       return _psposix.wait_pid(self.pid, timeout, self._name)
     File "/opensource/oppia/../oppia_tools/psutil-5.7.3/psutil/_psposix.py", line 115, in wait_pid
       retpid, status = os.waitpid(pid, flags)
   KeyboardInterrupt
   ```
   </details>

4. If you want to run backend tests and check coverage, please install these 2 pip libraries globally (or in your venv).

   ```
   pip install coverage configparser
   ```

## Tips and tricks

* To preserve the contents of the local datastore between consecutive runs, use the `--save_datastore` argument when starting up the dev server:

```
  python -m scripts.start --save_datastore
```

* The default Oppia installation comes with a set of [demo explorations](https://github.com/oppia/oppia/tree/61f19354098669bcb408ef7b65fa50d92c076488/data/explorations). On startup, none of these are loaded. To load them, log in to your server as an admin, then click your username in the top-right corner and choose 'Admin Page'. This will open the admin page, from which you can load the demo explorations.
