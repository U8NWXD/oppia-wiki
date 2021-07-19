**Note:** If you just want to create and share explorations, you may be able to use the hosted server at https://www.oppia.org (in which case you don't need to install anything).

**Note:** If you have a fresh installation of Ubuntu 20 (not upgraded from previous versions), you might face issues when installing Python 2 packages since Python 2 libraries are no longer present in Ubuntu 20 repositories ([reference](https://linuxize.com/post/how-to-install-pip-on-ubuntu-20.04/)).

*These installation instructions were last tested on 22 Feb 2016. For more information on issues that may occasionally arise with the installation process, please see the [Troubleshooting](https://github.com/oppia/oppia/wiki/Troubleshooting) page.*

**Before following these instructions, you should have followed the [[Installing Oppia wiki page|Installing-Oppia]].**

## Prerequisites

_The following instructions will install Oppia on your local machine._

Oppia relies on a number of programs and third-party libraries. Many of these libraries are downloaded automatically for you when you first run the `start.py` script provided with Oppia (see step 1 in the next section). However, there are some things that you will need to do beforehand:

1. Ensure that you have [Python 2.7](http://www.python.org/download/releases/2.7/) installed (Note: you can check this by running `python --version`). If Python 2.7 is not installed, you can probably install it through your package manager. If not, download and run the latest Python 2.7 installer from https://www.python.org/downloads/. Make sure you download an installer for Python 2 and not Python 3!

2. Make sure you have curl (used to download third-party libraries), setuptools (needed for installing coverage, which checks test coverage for the Python code), git (which allows you to store the source in version control), python-dev (which is used for the numpy installation), python-pip (which is also used for the numpy installation) and pyyaml (which is used to parse YAML files):

   ```console
   sudo apt-get install curl python-setuptools git python-dev python-pip python-yaml
   ```

   Alternatively, if you are on Debian/Ubuntu, you can use the `install_prerequisites.sh` script to install these. From the oppia directory:

   ```
   bash scripts/install_prerequisites.sh
   ```

   Since Python 2 was deprecated, support for it has been dropping across Linux distributions. You may therefore find that some of these python dependencies are not available in your package manager. If that is the case, you can use pyenv instead. First, make sure you install the Python build dependencies for your operating system. These are specified [here](https://github.com/pyenv/pyenv/wiki#suggested-build-environment). Next, install pyenv:

   ```console
   $ curl pyenv.run | bash
     % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                    Dload  Upload   Total   Spent    Left  Speed
   100   270  100   270    0     0    630      0 --:--:-- --:--:-- --:--:--   632
   Cloning into '/home/user/.pyenv'...
   ...
   WARNING: seems you still have not added 'pyenv' to the load path.
   ...
   ```

   If you see the warning at the end, add the following lines to your `.bashrc`:

   ```bash
   export PYENV_ROOT="$HOME/.pyenv"
   export PATH="$PYENV_ROOT/bin:$PATH"
   eval "$(pyenv init --path)"
   
   eval "$(pyenv init -)"
   eval "$(pyenv virtualenv-init -)"
   ```

   Then reload your shell or open a new terminal window to load your updated `~/.bashrc`.

   Now you can install Python 2.7 and the associated pip like this:

   ```console
   $ pyenv install 2.7.18
   Downloading Python-2.7.18.tar.xz...
   -> https://www.python.org/ftp/python/2.7.18/Python-2.7.18.tar.xz
   Installing Python-2.7.18...
   Installed Python-2.7.18 to /home/user/.pyenv/versions/2.7.18
   ```

   Create a virtual environment for oppia:

   ```console
   $ pyenv virtualenv 2.7.18 oppia
   ...
   $ pyenv versions
   ...
   oppia
   ...
   ```

   In the cloned `oppia` folder, run

   ```console
   pyenv local oppia
   ```

   Now whenever you are within the `oppia` folder, the virtual environment will be active. You can install the Python dependencies here:

   ```console
   $ pip install pyyaml setuptools
   Requirement already satisfied: setuptools in /home/user/.pyenv/versions/2.7.18/envs/oppia-tmp/lib/python2.7/site-packages (44.1.1)
   Collecting pyyaml
     Downloading PyYAML-5.4.1-cp27-cp27mu-manylinux1_x86_64.whl (574 kB)
        |████████████████████████████████| 574 kB 2.3 MB/s 
   Installing collected packages: pyyaml
   Successfully installed pyyaml-5.4.1
   ```

   Note that you'll probably see lots of warnings that Python 2 is deprecated. Those are expected.

3. If you want to run backend tests and check coverage, please install these 2 pip libraries globally (or in your venv).

   ```console
   pip install coverage configparser
   ```

4. Install Chrome from [Google's website](https://www.google.com/chrome). You'll need this to run tests.

## Running Oppia on a development server

1. In a terminal, navigate to `oppia/` and run:

   ```console
   python -m scripts.start
   ```

   <details>
   <summary>Example output</summary>
   ```text
   Checking if node.js is installed in /opensource/oppia/../oppia_tools
   Checking if yarn is installed in /opensource/oppia/../oppia_tools
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
   │ gRPC Python library                            │     1.20.0 │  2.1 MiB │
   │ gcloud Beta Commands                           │ 2019.05.17 │  < 1 MiB │
   │ gcloud app Python Extensions                   │     1.9.91 │  6.1 MiB │
   │ gcloud app Python Extensions (Extra Libraries) │     1.9.90 │ 27.1 MiB │
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
   ╠═ Creating backup and activating new installation          ═╣
   ╚════════════════════════════════════════════════════════════╝
   
   Performing post processing steps...done.                                       
   
   Update done!
   
   Checking if coverage is installed in /opensource/oppia/../oppia_tools
   Installing coverage
   Checking if pip is installed on the local machine
   Collecting coverage==5.3
     Downloading coverage-5.3-cp27-cp27mu-manylinux1_x86_64.whl (226 kB)
   Installing collected packages: coverage
   Successfully installed coverage-5.3
   
   Checking if pylint is installed in /opensource/oppia/../oppia_tools
   Installing pylint
   Checking if pip is installed on the local machine
   Collecting pylint==1.9.5
     Downloading pylint-1.9.5-py2.py3-none-any.whl (696 kB)
   Collecting astroid<2.0,>=1.6
     Downloading astroid-1.6.6-py2.py3-none-any.whl (305 kB)
   Collecting six
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Collecting mccabe
     Downloading mccabe-0.6.1-py2.py3-none-any.whl (8.6 kB)
   Collecting singledispatch; python_version < "3.4"
     Using cached singledispatch-3.6.2-py2.py3-none-any.whl (8.2 kB)
   Collecting configparser; python_version == "2.7"
     Using cached configparser-4.0.2-py2.py3-none-any.whl (22 kB)
   Collecting isort>=4.2.5
     Downloading isort-4.3.21-py2.py3-none-any.whl (42 kB)
   Collecting backports.functools-lru-cache; python_version == "2.7"
     Downloading backports.functools_lru_cache-1.6.4-py2.py3-none-any.whl (5.9 kB)
   Collecting wrapt
     Downloading wrapt-1.12.1.tar.gz (27 kB)
   Collecting enum34>=1.1.3; python_version < "3.4"
     Downloading enum34-1.1.10-py2-none-any.whl (11 kB)
   Collecting lazy-object-proxy
     Downloading lazy_object_proxy-1.6.0-cp27-cp27mu-manylinux1_x86_64.whl (53 kB)
   Collecting futures; python_version < "3.2"
     Downloading futures-3.3.0-py2-none-any.whl (16 kB)
   Building wheels for collected packages: wrapt
     Building wheel for wrapt (setup.py): started
     Building wheel for wrapt (setup.py): finished with status 'done'
     Created wheel for wrapt: filename=wrapt-1.12.1-cp27-cp27mu-linux_x86_64.whl size=67771 sha256=1047cc9ed63aae5971444daf657b87e02f1d0f75af6acec06e91c6e711a018b0
     Stored in directory: /home/user/.cache/pip/wheels/5b/d8/8e/81a83cb5321b940a954996f5b57fddc8976e712b3ac3a1a54b
   Successfully built wrapt
   Installing collected packages: wrapt, six, enum34, singledispatch, backports.functools-lru-cache, lazy-object-proxy, astroid, mccabe, configparser, futures, isort, pylint
   Successfully installed astroid-1.6.6 backports.functools-lru-cache-1.6.4 configparser-4.0.2 enum34-1.1.10 futures-3.3.0 isort-4.3.21 lazy-object-proxy-1.6.0 mccabe-0.6.1 pylint-1.9.5 singledispatch-3.6.2 six-1.16.0 wrapt-1.12.1
   
   Checking if Pillow is installed in /opensource/oppia/../oppia_tools
   Installing Pillow
   Checking if pip is installed on the local machine
   Collecting Pillow==6.2.2
     Downloading Pillow-6.2.2-cp27-cp27mu-manylinux1_x86_64.whl (2.1 MB)
   Installing collected packages: Pillow
   Successfully installed Pillow-6.2.2
   
   Checking if pylint-quotes is installed in /opensource/oppia/../oppia_tools
   Installing pylint-quotes
   Checking if pip is installed on the local machine
   Collecting pylint-quotes==0.1.8
     Downloading pylint_quotes-0.1.8-py2.py3-none-any.whl (6.3 kB)
   Collecting pylint
     Using cached pylint-1.9.5-py2.py3-none-any.whl (696 kB)
   Collecting astroid<2.0,>=1.6
     Using cached astroid-1.6.6-py2.py3-none-any.whl (305 kB)
   Collecting six
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Collecting mccabe
     Using cached mccabe-0.6.1-py2.py3-none-any.whl (8.6 kB)
   Collecting singledispatch; python_version < "3.4"
     Using cached singledispatch-3.6.2-py2.py3-none-any.whl (8.2 kB)
   Collecting configparser; python_version == "2.7"
     Using cached configparser-4.0.2-py2.py3-none-any.whl (22 kB)
   Collecting isort>=4.2.5
     Using cached isort-4.3.21-py2.py3-none-any.whl (42 kB)
   Collecting backports.functools-lru-cache; python_version == "2.7"
     Using cached backports.functools_lru_cache-1.6.4-py2.py3-none-any.whl (5.9 kB)
   Processing /home/user/.cache/pip/wheels/5b/d8/8e/81a83cb5321b940a954996f5b57fddc8976e712b3ac3a1a54b/wrapt-1.12.1-cp27-cp27mu-linux_x86_64.whl
   Collecting enum34>=1.1.3; python_version < "3.4"
     Using cached enum34-1.1.10-py2-none-any.whl (11 kB)
   Collecting lazy-object-proxy
     Using cached lazy_object_proxy-1.6.0-cp27-cp27mu-manylinux1_x86_64.whl (53 kB)
   Collecting futures; python_version < "3.2"
     Using cached futures-3.3.0-py2-none-any.whl (16 kB)
   Installing collected packages: wrapt, six, enum34, singledispatch, backports.functools-lru-cache, lazy-object-proxy, astroid, mccabe, configparser, futures, isort, pylint, pylint-quotes
   Successfully installed astroid-1.6.6 backports.functools-lru-cache-1.6.4 configparser-4.0.2 enum34-1.1.10 futures-3.3.0 isort-4.3.21 lazy-object-proxy-1.6.0 mccabe-0.6.1 pylint-1.9.5 pylint-quotes-0.1.8 singledispatch-3.6.2 six-1.16.0 wrapt-1.12.1
   
   Checking if webtest is installed in /opensource/oppia/../oppia_tools
   Installing webtest
   Checking if pip is installed on the local machine
   Collecting webtest==2.0.35
     Downloading WebTest-2.0.35-py2.py3-none-any.whl (32 kB)
   Collecting WebOb>=1.2
     Downloading WebOb-1.8.7-py2.py3-none-any.whl (114 kB)
   Collecting six
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Collecting waitress>=0.8.5
     Downloading waitress-1.4.4-py2.py3-none-any.whl (58 kB)
   Collecting beautifulsoup4
     Downloading beautifulsoup4-4.9.3-py2-none-any.whl (115 kB)
   Collecting soupsieve<2.0,>1.2; python_version < "3.0"
     Downloading soupsieve-1.9.6-py2.py3-none-any.whl (33 kB)
   Collecting backports.functools-lru-cache; python_version < "3"
     Using cached backports.functools_lru_cache-1.6.4-py2.py3-none-any.whl (5.9 kB)
   Installing collected packages: WebOb, six, waitress, backports.functools-lru-cache, soupsieve, beautifulsoup4, webtest
   Successfully installed WebOb-1.8.7 backports.functools-lru-cache-1.6.4 beautifulsoup4-4.9.3 six-1.16.0 soupsieve-1.9.6 waitress-1.4.4 webtest-2.0.35
   
   Checking if isort is installed in /opensource/oppia/../oppia_tools
   Installing isort
   Checking if pip is installed on the local machine
   Collecting isort==4.3.21
     Using cached isort-4.3.21-py2.py3-none-any.whl (42 kB)
   Collecting futures; python_version < "3.2"
     Using cached futures-3.3.0-py2-none-any.whl (16 kB)
   Collecting backports.functools-lru-cache; python_version < "3.2"
     Using cached backports.functools_lru_cache-1.6.4-py2.py3-none-any.whl (5.9 kB)
   Installing collected packages: futures, backports.functools-lru-cache, isort
   Successfully installed backports.functools-lru-cache-1.6.4 futures-3.3.0 isort-4.3.21
   
   Checking if pycodestyle is installed in /opensource/oppia/../oppia_tools
   Installing pycodestyle
   Checking if pip is installed on the local machine
   Collecting pycodestyle==2.6.0
     Downloading pycodestyle-2.6.0-py2.py3-none-any.whl (41 kB)
   Installing collected packages: pycodestyle
   Successfully installed pycodestyle-2.6.0
   
   Checking if esprima is installed in /opensource/oppia/../oppia_tools
   Installing esprima
   Checking if pip is installed on the local machine
   Collecting esprima==4.0.1
     Downloading esprima-4.0.1.tar.gz (47 kB)
   Building wheels for collected packages: esprima
     Building wheel for esprima (setup.py): started
     Building wheel for esprima (setup.py): finished with status 'done'
     Created wheel for esprima: filename=esprima-4.0.1-py2-none-any.whl size=62260 sha256=8c36986b2aa8dae5dca2d46fcd933d45bb487f1899943dcaaf5a4d28a8be20a1
     Stored in directory: /home/user/.cache/pip/wheels/f2/cb/61/c0b3b52f4bf629dec66c42a33ab8ed79b83f36754b5a76542b
   Successfully built esprima
   Installing collected packages: esprima
   Successfully installed esprima-4.0.1
   
   Checking if PyGithub is installed in /opensource/oppia/../oppia_tools
   Installing PyGithub
   Checking if pip is installed on the local machine
   Collecting PyGithub==1.45
     Downloading PyGithub-1.45.tar.gz (113 kB)
   Collecting deprecated
     Downloading Deprecated-1.2.12-py2.py3-none-any.whl (9.5 kB)
   Collecting pyjwt
     Downloading PyJWT-1.7.1-py2.py3-none-any.whl (18 kB)
   Collecting requests>=2.14.0
     Downloading requests-2.26.0-py2.py3-none-any.whl (62 kB)
   Collecting six
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Processing /home/user/.cache/pip/wheels/5b/d8/8e/81a83cb5321b940a954996f5b57fddc8976e712b3ac3a1a54b/wrapt-1.12.1-cp27-cp27mu-linux_x86_64.whl
   Collecting certifi>=2017.4.17
     Downloading certifi-2021.5.30-py2.py3-none-any.whl (145 kB)
   Collecting urllib3<1.27,>=1.21.1
     Downloading urllib3-1.26.6-py2.py3-none-any.whl (138 kB)
   Collecting chardet<5,>=3.0.2; python_version < "3"
     Downloading chardet-4.0.0-py2.py3-none-any.whl (178 kB)
   Collecting idna<3,>=2.5; python_version < "3"
     Downloading idna-2.10-py2.py3-none-any.whl (58 kB)
   Building wheels for collected packages: PyGithub
     Building wheel for PyGithub (setup.py): started
     Building wheel for PyGithub (setup.py): finished with status 'done'
     Created wheel for PyGithub: filename=PyGithub-1.45-py2-none-any.whl size=207489 sha256=5ce195f097e585bf5eb8dd4275feaae3b67853a7047ec7ce94077599b6450401
     Stored in directory: /home/user/.cache/pip/wheels/e5/82/fd/22dd7e6e45214433191cc08efb0b5c63f3e0e489569f10bbcd
   Successfully built PyGithub
   Installing collected packages: wrapt, deprecated, pyjwt, certifi, urllib3, chardet, idna, requests, six, PyGithub
   Successfully installed PyGithub-1.45 certifi-2021.5.30 chardet-4.0.0 deprecated-1.2.12 idna-2.10 pyjwt-1.7.1 requests-2.26.0 six-1.16.0 urllib3-1.26.6 wrapt-1.12.1
   
   Checking if protobuf is installed in /opensource/oppia/../oppia_tools
   Installing protobuf
   Checking if pip is installed on the local machine
   Collecting protobuf==3.13.0
     Downloading protobuf-3.13.0-cp27-cp27mu-manylinux1_x86_64.whl (1.3 MB)
   Collecting setuptools
     Downloading setuptools-44.1.1-py2.py3-none-any.whl (583 kB)
   Collecting six>=1.9
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Installing collected packages: setuptools, six, protobuf
   Successfully installed protobuf-3.13.0 setuptools-44.1.1 six-1.16.0
   
   Checking if psutil is installed in /opensource/oppia/../oppia_tools
   Installing psutil
   Checking if pip is installed on the local machine
   Collecting psutil==5.7.3
     Downloading psutil-5.7.3.tar.gz (465 kB)
   Building wheels for collected packages: psutil
     Building wheel for psutil (setup.py): started
     Building wheel for psutil (setup.py): finished with status 'done'
     Created wheel for psutil: filename=psutil-5.7.3-cp27-cp27mu-linux_x86_64.whl size=272064 sha256=9e15af713409ba73e2f77eaf3bede7c12e758fca88a63fef1461cec6fa08c7ec
     Stored in directory: /home/user/.cache/pip/wheels/3b/8a/d2/25b4aa99bf70907f2db25db3b6f1ce0ae24080a79bef48503c
   Successfully built psutil
   Installing collected packages: psutil
   Successfully installed psutil-5.7.3
   
   Checking if pip-tools is installed in /opensource/oppia/../oppia_tools
   Installing pip-tools
   Checking if pip is installed on the local machine
   Collecting pip-tools==5.4.0
     Downloading pip_tools-5.4.0-py2.py3-none-any.whl (45 kB)
   Collecting click>=7
     Downloading click-7.1.2-py2.py3-none-any.whl (82 kB)
   Collecting pip>=20.1
     Downloading pip-20.3.4-py2.py3-none-any.whl (1.5 MB)
   Collecting six
     Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
   Installing collected packages: click, pip, six, pip-tools
   Successfully installed click-7.1.2 pip-20.3.4 pip-tools-5.4.0 six-1.16.0
   
   Checking if setuptools is installed in /opensource/oppia/../oppia_tools
   Installing setuptools
   Checking if pip is installed on the local machine
   Collecting setuptools==36.6.0
     Downloading setuptools-36.6.0-py2.py3-none-any.whl (481 kB)
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
     Using cached protobuf-3.13.0-cp27-cp27mu-manylinux1_x86_64.whl (1.3 MB)
   Requirement already satisfied: setuptools in /home/user/.pyenv/versions/2.7.18/envs/oppia-tmp/lib/python2.7/site-packages (from protobuf==3.13.0) (44.1.1)
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
   mailchimp3==3.0.14        # via -r requirements.in
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
   requests==2.24.0          # via -r requirements.in, apache-beam, cachecontrol, google-api-core, google-cloud-storage, hdfs, mailchimp3, requests-mock, requests-toolbelt
   rsa==4.5                  # via google-auth, oauth2client
   simplejson==3.17.0        # via -r requirements.in, googleappenginemapreduce
   six==1.15.0               # via -r requirements.in, bleach, fasteners, firebase-admin, google-api-core, google-api-python-client, google-apitools, google-auth, google-auth-httplib2, google-cloud-bigquery, google-cloud-core, google-resumable-media, grpcio, hdfs, html5lib, mock, oauth2client, packaging, protobuf, pyarrow, python-dateutil, requests-mock, webapp2
   soupsieve==1.9.5          # via -r requirements.in, beautifulsoup4
   typing-extensions==3.7.4.3  # via apache-beam
   typing==3.7.4.3           # via -r requirements.in, apache-beam, typing-extensions
   uritemplate==3.0.1        # via google-api-python-client
   urllib3==1.25.11          # via elasticsearch, requests
   webapp2==3.0.0b1          # via -r requirements.in
   webencodings==0.5.1       # via -r requirements.in, bleach, html5lib
   webob==1.8.6              # via webapp2
   
   # The following packages are considered to be unsafe in a requirements file:
   # setuptools
   Checking if pip is installed on the local machine
   Collecting apache-beam[gcp]==2.24.0
     Using cached apache_beam-2.24.0-cp27-cp27mu-manylinux2010_x86_64.whl (7.5 MB)
   Collecting avro==1.9.2
     Using cached avro-1.9.2.tar.gz (49 kB)
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
   Collecting crcmod==1.7
     Using cached crcmod-1.7.tar.gz (89 kB)
   Collecting dill==0.3.1.1
     Using cached dill-0.3.1.1.tar.gz (151 kB)
   Collecting docopt==0.6.2
     Using cached docopt-0.6.2.tar.gz (25 kB)
   Collecting elasticsearch==7.10.0
     Using cached elasticsearch-7.10.0-py2.py3-none-any.whl (321 kB)
   Collecting enum34==1.1.10
     Using cached enum34-1.1.10-py2-none-any.whl (11 kB)
   Collecting fastavro==0.23.6
     Using cached fastavro-0.23.6-cp27-cp27mu-manylinux2010_x86_64.whl (1.1 MB)
   Collecting fasteners==0.16
     Using cached fasteners-0.16-py2.py3-none-any.whl (28 kB)
   Collecting firebase-admin
     Cloning git://github.com/oppia/firebase-admin-python (to revision 8d6deee889733d09ef5327d78c09e4d7b17785ac) to /tmp/pip-install-NHAMCy/firebase-admin
   Collecting funcsigs==1.0.2
     Using cached funcsigs-1.0.2-py2.py3-none-any.whl (17 kB)
   Processing /home/user/.cache/pip/wheels/5f/11/0c/aad680baf5ef4fbcbab992c9f03e1130357e0c173a4fdabfff/future-0.18.2-py2-none-any.whl
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
   Collecting googleappenginecloudstorageclient==1.9.22.1
     Using cached GoogleAppEngineCloudStorageClient-1.9.22.1.tar.gz (28 kB)
   Collecting googleappenginemapreduce==1.9.22.0
     Using cached GoogleAppEngineMapReduce-1.9.22.0.tar.gz (180 kB)
   Collecting googleappenginepipeline==1.9.22.1
     Using cached GoogleAppEnginePipeline-1.9.22.1.tar.gz (89 kB)
   Collecting graphy==1.0.0
     Using cached Graphy-1.0.0.tar.gz (32 kB)
   Collecting grpc-google-iam-v1==0.12.3
     Using cached grpc-google-iam-v1-0.12.3.tar.gz (13 kB)
   Collecting grpcio-gcp==0.2.2
     Using cached grpcio_gcp-0.2.2-py2.py3-none-any.whl (9.4 kB)
   Collecting grpcio==1.32.0
     Using cached grpcio-1.32.0-cp27-cp27mu-manylinux2010_x86_64.whl (3.6 MB)
   Collecting hdfs==2.5.8
     Using cached hdfs-2.5.8.tar.gz (41 kB)
   Collecting html5lib==1.0.1
     Using cached html5lib-1.0.1-py2.py3-none-any.whl (117 kB)
   Collecting httplib2==0.17.4
     Using cached httplib2-0.17.4.tar.gz (256 kB)
   Collecting idna==2.10
     Using cached idna-2.10-py2.py3-none-any.whl (58 kB)
   Collecting mailchimp3==3.0.14
     Using cached mailchimp3-3.0.14-py2.py3-none-any.whl (94 kB)
   Collecting mock==2.0.0
     Using cached mock-2.0.0-py2.py3-none-any.whl (56 kB)
   Collecting monotonic==1.5
     Using cached monotonic-1.5-py2.py3-none-any.whl (5.3 kB)
   Collecting mox==0.5.3
     Using cached mox-0.5.3.tar.gz (32 kB)
   Collecting msgpack==1.0.2
     Using cached msgpack-1.0.2.tar.gz (123 kB)
   Collecting mutagen==1.43.0
     Using cached mutagen-1.43.0-py2.py3-none-any.whl (212 kB)
   Collecting numpy==1.16.6
     Using cached numpy-1.16.6-cp27-cp27mu-manylinux1_x86_64.whl (17.0 MB)
   Collecting oauth2client==3.0.0
     Using cached oauth2client-3.0.0.tar.gz (77 kB)
   Collecting packaging==20.4
     Using cached packaging-20.4-py2.py3-none-any.whl (37 kB)
   Collecting pbr==5.5.1
     Using cached pbr-5.5.1-py2.py3-none-any.whl (106 kB)
   Collecting protobuf==3.13.0
     Using cached protobuf-3.13.0-cp27-cp27mu-manylinux1_x86_64.whl (1.3 MB)
   Collecting pyarrow==0.16.0
     Using cached pyarrow-0.16.0-cp27-cp27mu-manylinux2010_x86_64.whl (20.5 MB)
   Collecting pyasn1-modules==0.2.8
     Using cached pyasn1_modules-0.2.8-py2.py3-none-any.whl (155 kB)
   Collecting pyasn1==0.4.8
     Using cached pyasn1-0.4.8-py2.py3-none-any.whl (77 kB)
   Collecting pydot==1.4.1
     Using cached pydot-1.4.1-py2.py3-none-any.whl (19 kB)
   Collecting pylatexenc==2.6
     Using cached pylatexenc-2.6.tar.gz (156 kB)
   Collecting pymongo==3.11.3
     Using cached pymongo-3.11.3-cp27-cp27mu-manylinux1_x86_64.whl (488 kB)
   Collecting pyparsing==2.4.7
     Using cached pyparsing-2.4.7-py2.py3-none-any.whl (67 kB)
   Collecting python-dateutil==2.8.1
     Using cached python_dateutil-2.8.1-py2.py3-none-any.whl (227 kB)
   Collecting pytz==2020.1
     Using cached pytz-2020.1-py2.py3-none-any.whl (510 kB)
   Collecting pyvcf==0.6.8
     Using cached PyVCF-0.6.8.tar.gz (34 kB)
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
     Using cached simplejson-3.17.0.tar.gz (83 kB)
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
   Collecting webapp2==3.0.0b1
     Using cached webapp2-3.0.0b1.tar.gz (193 kB)
   Collecting webencodings==0.5.1
     Using cached webencodings-0.5.1-py2.py3-none-any.whl (11 kB)
   Collecting webob==1.8.6
     Using cached WebOb-1.8.6-py2.py3-none-any.whl (114 kB)
   Building wheels for collected packages: avro, crcmod, dill, docopt, firebase-admin, googleappenginecloudstorageclient, googleappenginemapreduce, googleappenginepipeline, graphy, grpc-google-iam-v1, hdfs, httplib2, mox, msgpack, oauth2client, pylatexenc, pyvcf, simplejson, webapp2
     Building wheel for avro (setup.py): started
     Building wheel for avro (setup.py): finished with status 'done'
     Created wheel for avro: filename=avro-1.9.2-py2-none-any.whl size=41686 sha256=28a9b6a1dfbcc6f49bc08fa0447380269b1ea2b119c50e4561ebcc08493c6236
     Stored in directory: /home/user/.cache/pip/wheels/28/a0/fc/a3d4892b81eedc9e027323c08e9890bee1ec2d35edd1c1ac96
     Building wheel for crcmod (setup.py): started
     Building wheel for crcmod (setup.py): finished with status 'done'
     Created wheel for crcmod: filename=crcmod-1.7-cp27-cp27mu-linux_x86_64.whl size=28764 sha256=bd59c7eaf78d693d54325adc502952d2f6ee00f1d80098229382013671b4dc67
     Stored in directory: /home/user/.cache/pip/wheels/06/c2/19/2d00b8cea7d9ac6e19d286b0c41cf7a9eb39f64bd21ed43194
     Building wheel for dill (setup.py): started
     Building wheel for dill (setup.py): finished with status 'done'
     Created wheel for dill: filename=dill-0.3.1.1-py2-none-any.whl size=78530 sha256=6632d8ea045e487107eeabfdb39e89bd5c8ff8c94ac391dff87242cd65da693e
     Stored in directory: /home/user/.cache/pip/wheels/54/6e/1d/172ed90bc541c925faff97e03c7a110b8ce876ab13e10b0c77
     Building wheel for docopt (setup.py): started
     Building wheel for docopt (setup.py): finished with status 'done'
     Created wheel for docopt: filename=docopt-0.6.2-py2.py3-none-any.whl size=13705 sha256=402916d9d17ad7805600d5347486e2b55a0251d6a8ca573faa16776dc58844d1
     Stored in directory: /home/user/.cache/pip/wheels/1c/d7/2d/aefbee2bf20e0ed968d4ab943e03451db0f14c52b5f624fc7e
     Building wheel for firebase-admin (setup.py): started
     Building wheel for firebase-admin (setup.py): finished with status 'done'
     Created wheel for firebase-admin: filename=firebase_admin-3.2.1-py2.py3-none-any.whl size=84318 sha256=65acf2d73bfab7fb5759a3811653eca27e767f65c67fd17b8365c52324e1ca15
     Stored in directory: /home/user/.cache/pip/wheels/3d/80/ec/3a4238be9b719dfde109fffd34fa73125aef18f2033c1b2deb
     Building wheel for googleappenginecloudstorageclient (setup.py): started
     Building wheel for googleappenginecloudstorageclient (setup.py): finished with status 'done'
     Created wheel for googleappenginecloudstorageclient: filename=GoogleAppEngineCloudStorageClient-1.9.22.1-py2-none-any.whl size=30728 sha256=9ee48e9be188b3a385db7c485e51c852ae8f0c4669c66dbf656321c837db173a
     Stored in directory: /home/user/.cache/pip/wheels/32/7e/c5/bfe9faf3343d591ec8a7a1b5463a66f9216150d493a627aa0c
     Building wheel for googleappenginemapreduce (setup.py): started
     Building wheel for googleappenginemapreduce (setup.py): finished with status 'done'
     Created wheel for googleappenginemapreduce: filename=GoogleAppEngineMapReduce-1.9.22.0-py2-none-any.whl size=204540 sha256=3abf66e265564e8822e7dd7b93a4b5a9abb0a00d2f1cb098b1c231b09c11b1d9
     Stored in directory: /home/user/.cache/pip/wheels/12/56/e0/631c0c4226da75dbd39b74532eeb3da683bd869399e9c0fbdb
     Building wheel for googleappenginepipeline (setup.py): started
     Building wheel for googleappenginepipeline (setup.py): finished with status 'done'
     Created wheel for googleappenginepipeline: filename=GoogleAppEnginePipeline-1.9.22.1-py2-none-any.whl size=99284 sha256=d0c513c2778eb853f7acc6b482a0b4744e5f74f62acd6bf0ac2bae5cb3b3f753
     Stored in directory: /home/user/.cache/pip/wheels/03/1d/33/5a14156fa58909fc2ef59467f37a4f88a2daea1f026d2edaff
     Building wheel for graphy (setup.py): started
     Building wheel for graphy (setup.py): finished with status 'done'
     Created wheel for graphy: filename=Graphy-1.0.0-py2-none-any.whl size=45982 sha256=ecf6816ffd33e6cf5d30362292fd97b111bcad7dd73d7a906dcbdd72d2750cbe
     Stored in directory: /home/user/.cache/pip/wheels/91/98/a6/08a1cf2d711e2b93927d911480646f5c69e5abcf9e43d3fa9e
     Building wheel for grpc-google-iam-v1 (setup.py): started
     Building wheel for grpc-google-iam-v1 (setup.py): finished with status 'done'
     Created wheel for grpc-google-iam-v1: filename=grpc_google_iam_v1-0.12.3-py2-none-any.whl size=18502 sha256=5e1614841c02bfcff473c8e4e8baa6593c3ee3f61e459c3141865565073d9d23
     Stored in directory: /home/user/.cache/pip/wheels/77/4d/90/443c1cecdcfbf9d97f6e567304aacddc234cf1b26e48c6f0e5
     Building wheel for hdfs (setup.py): started
     Building wheel for hdfs (setup.py): finished with status 'done'
     Created wheel for hdfs: filename=hdfs-2.5.8-py2-none-any.whl size=33212 sha256=5b55f9d9ac0dfec1ad397f4d7451b66193b69c8372ecb021c76ba3215c9bf4c9
     Stored in directory: /home/user/.cache/pip/wheels/3a/18/11/31dfb768f5d55108760cdd028ad7026173f7c0e847cb71fe4b
     Building wheel for httplib2 (setup.py): started
     Building wheel for httplib2 (setup.py): finished with status 'done'
     Created wheel for httplib2: filename=httplib2-0.17.4-py2-none-any.whl size=95766 sha256=754fb12e7cd6d152fe199735804917a47780e4d6a3878435d7c177013f0c13bb
     Stored in directory: /home/user/.cache/pip/wheels/ce/98/d0/7cbebe9de22c986e85e2561069d25c9752b43523240f803199
     Building wheel for mox (setup.py): started
     Building wheel for mox (setup.py): finished with status 'done'
     Created wheel for mox: filename=mox-0.5.3-py2-none-any.whl size=21479 sha256=4c5c79cbb2a35d95bb5f4919e86fda4e5c67dba2c2a91fa6343e076f62c4070d
     Stored in directory: /home/user/.cache/pip/wheels/4e/19/75/ea3124778e7b78f4ef58c91e77e76c2287c7d50d711fa1ec7e
     Building wheel for msgpack (setup.py): started
     Building wheel for msgpack (setup.py): finished with status 'done'
     Created wheel for msgpack: filename=msgpack-1.0.2-py2-none-any.whl size=15813 sha256=e60da5909c2b9f047d98c53dd8bf4f76bcac798e203d9fbc59d254a1c138ae08
     Stored in directory: /home/user/.cache/pip/wheels/9a/c1/2f/dee60aba1e3df6f5a6edd694e62bf14f3537158cf1b63cc39d
     Building wheel for oauth2client (setup.py): started
     Building wheel for oauth2client (setup.py): finished with status 'done'
     Created wheel for oauth2client: filename=oauth2client-3.0.0-py2-none-any.whl size=106380 sha256=13ca7488643ba9076ef28d451cba258d643cad0f0d81300a83211b804b309dd5
     Stored in directory: /home/user/.cache/pip/wheels/b3/ca/7f/39e3e6758df2c1bfc56e12e3a7cb4693a7da0a63f0c9791f14
     Building wheel for pylatexenc (setup.py): started
     Building wheel for pylatexenc (setup.py): finished with status 'done'
     Created wheel for pylatexenc: filename=pylatexenc-2.6-py2-none-any.whl size=129820 sha256=3ba64abd7df6ad758ac0f52e86ea73572ba3309e1660fdaca592c256bf7c4e8d
     Stored in directory: /home/user/.cache/pip/wheels/ee/eb/3e/87a72ffc609d127e801988d6001fb8076614e44e2d8853c4d4
     Building wheel for pyvcf (setup.py): started
     Building wheel for pyvcf (setup.py): finished with status 'done'
     Created wheel for pyvcf: filename=PyVCF-0.6.8-py2-none-any.whl size=36041 sha256=b9d265de8d78cdc83bde4412f687f618dbb9dadb4156bae40df5810aec4fc60b
     Stored in directory: /home/user/.cache/pip/wheels/b8/43/84/5248fa58c81c6f2a9b1e4f1f8b12573f79a75f492c7a1b0e5a
     Building wheel for simplejson (setup.py): started
     Building wheel for simplejson (setup.py): finished with status 'done'
     Created wheel for simplejson: filename=simplejson-3.17.0-cp27-cp27mu-linux_x86_64.whl size=129304 sha256=ea60f7f2297a5d87394a72e00c429f2d919e8be1728ffbc7927a8d7ba996bfa1
     Stored in directory: /home/user/.cache/pip/wheels/9f/c9/94/3df00cc1b76c2fe12de900c4a447178c11157624da56e2bd5d
     Building wheel for webapp2 (setup.py): started
     Building wheel for webapp2 (setup.py): finished with status 'done'
     Created wheel for webapp2: filename=webapp2-3.0.0b1-py2-none-any.whl size=68364 sha256=5fd285aa59c0f354e310af9be071887424c258a5eae5112f4b76ca858452e309
     Stored in directory: /home/user/.cache/pip/wheels/98/78/cb/49b134db6f9effff130cfc90286cb91b59f71981221c1d6047
   Successfully built avro crcmod dill docopt firebase-admin googleappenginecloudstorageclient googleappenginemapreduce googleappenginepipeline graphy grpc-google-iam-v1 hdfs httplib2 mox msgpack oauth2client pylatexenc pyvcf simplejson webapp2
   Installing collected packages: apache-beam, avro, backports.functools-lru-cache, beautifulsoup4, bleach, cachecontrol, cachetools, callbacks, certifi, chardet, contextlib2, crcmod, dill, docopt, elasticsearch, enum34, fastavro, fasteners, firebase-admin, funcsigs, future, futures, google-api-core, google-api-python-client, google-apitools, google-auth-httplib2, google-auth, google-cloud-bigquery, google-cloud-bigtable, google-cloud-core, google-cloud-datastore, google-cloud-dlp, google-cloud-firestore, google-cloud-language, google-cloud-pubsub, google-cloud-spanner, google-cloud-storage, google-cloud-tasks, google-cloud-translate, google-cloud-videointelligence, google-cloud-vision, google-resumable-media, googleapis-common-protos, googleappenginecloudstorageclient, googleappenginemapreduce, googleappenginepipeline, graphy, grpc-google-iam-v1, grpcio-gcp, grpcio, hdfs, html5lib, httplib2, idna, mailchimp3, mock, monotonic, mox, msgpack, mutagen, numpy, oauth2client, packaging, pbr, protobuf, pyarrow, pyasn1-modules, pyasn1, pydot, pylatexenc, pymongo, pyparsing, python-dateutil, pytz, pyvcf, redis, requests-mock, requests-toolbelt, requests, rsa, simplejson, six, soupsieve, typing-extensions, typing, uritemplate, urllib3, webapp2, webencodings, webob
   Successfully installed apache-beam-2.24.0 avro-1.9.2 backports.functools-lru-cache-1.6.1 beautifulsoup4-4.9.1 bleach-3.3.0 cachecontrol-0.12.6 cachetools-3.1.1 callbacks-0.3.0 certifi-2020.6.20 chardet-3.0.4 contextlib2-0.6.0.post1 crcmod-1.7 dill-0.3.1.1 docopt-0.6.2 elasticsearch-7.10.0 enum34-1.1.10 fastavro-0.23.6 fasteners-0.16 firebase-admin-3.2.1 funcsigs-1.0.2 future-0.18.2 futures-3.3.0 google-api-core-1.22.4 google-api-python-client-1.12.8 google-apitools-0.5.31 google-auth-1.22.1 google-auth-httplib2-0.0.4 google-cloud-bigquery-1.28.0 google-cloud-bigtable-1.7.0 google-cloud-core-1.5.0 google-cloud-datastore-1.15.3 google-cloud-dlp-1.0.0 google-cloud-firestore-1.9.0 google-cloud-language-1.3.0 google-cloud-pubsub-1.7.0 google-cloud-spanner-1.19.1 google-cloud-storage-1.35.0 google-cloud-tasks-1.5.0 google-cloud-translate-2.0.1 google-cloud-videointelligence-1.16.1 google-cloud-vision-1.0.0 google-resumable-media-1.2.0 googleapis-common-protos-1.52.0 googleappenginecloudstorageclient-1.9.22.1 googleappenginemapreduce-1.9.22.0 googleappenginepipeline-1.9.22.1 graphy-1.0.0 grpc-google-iam-v1-0.12.3 grpcio-1.32.0 grpcio-gcp-0.2.2 hdfs-2.5.8 html5lib-1.0.1 httplib2-0.17.4 idna-2.10 mailchimp3-3.0.14 mock-2.0.0 monotonic-1.5 mox-0.5.3 msgpack-1.0.2 mutagen-1.43.0 numpy-1.16.6 oauth2client-3.0.0 packaging-20.4 pbr-5.5.1 protobuf-3.13.0 pyarrow-0.16.0 pyasn1-0.4.8 pyasn1-modules-0.2.8 pydot-1.4.1 pylatexenc-2.6 pymongo-3.11.3 pyparsing-2.4.7 python-dateutil-2.8.1 pytz-2020.1 pyvcf-0.6.8 redis-3.5.3 requests-2.24.0 requests-mock-1.5.2 requests-toolbelt-0.9.1 rsa-4.5 simplejson-3.17.0 six-1.15.0 soupsieve-1.9.5 typing-3.7.4.3 typing-extensions-3.7.4.3 uritemplate-3.0.1 urllib3-1.25.11 webapp2-3.0.0b1 webencodings-0.5.1 webob-1.8.6
   
   Downloading file yuicompressor-2.4.8.jar to ../oppia_tools/yuicompressor-2.4.8 ...
   Download of yuicompressor-2.4.8.jar succeeded.
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
   Downloading and unzipping file MathJax-2.7.5 to ./third_party/static ...
   Download of MathJax-2.7.5 succeeded.
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
   Downloading file angular-translate.min.js to ./third_party/static/bower-angular-translate-2.18.1 ...
   Download of angular-translate.min.js succeeded.
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
   cd src && make all
   make[1]: Entering directory '/opensource/oppia_tools/redis-cli-6.0.10/src'
       CC Makefile.dep
   rm -rf redis-server redis-sentinel redis-cli redis-benchmark redis-check-rdb redis-check-aof *.o *.gcda *.gcno *.gcov redis.info lcov-html Makefile.dep dict-benchmark
   rm -f adlist.d quicklist.d ae.d anet.d dict.d server.d sds.d zmalloc.d lzf_c.d lzf_d.d pqsort.d zipmap.d sha1.d ziplist.d release.d networking.d util.d object.d db.d replication.d rdb.d t_string.d t_list.d t_set.d t_zset.d t_hash.d config.d aof.d pubsub.d multi.d debug.d sort.d intset.d syncio.d cluster.d crc16.d endianconv.d slowlog.d scripting.d bio.d rio.d rand.d memtest.d crcspeed.d crc64.d bitops.d sentinel.d notify.d setproctitle.d blocked.d hyperloglog.d latency.d sparkline.d redis-check-rdb.d redis-check-aof.d geo.d lazyfree.d module.d evict.d expire.d geohash.d geohash_helper.d childinfo.d defrag.d siphash.d rax.d t_stream.d listpack.d localtime.d lolwut.d lolwut5.d lolwut6.d acl.d gopher.d tracking.d connection.d tls.d sha256.d timeout.d setcpuaffinity.d anet.d adlist.d dict.d redis-cli.d zmalloc.d release.d ae.d crcspeed.d crc64.d siphash.d crc16.d ae.d anet.d redis-benchmark.d adlist.d dict.d zmalloc.d siphash.d
   (cd ../deps && make distclean)
   make[2]: Entering directory '/opensource/oppia_tools/redis-cli-6.0.10/deps'
   (cd hiredis && make clean) > /dev/null || true
   (cd linenoise && make clean) > /dev/null || true
   (cd lua && make clean) > /dev/null || true
   (cd jemalloc && [ -f Makefile ] && make distclean) > /dev/null || true
   (rm -f .make-*)
   make[2]: Leaving directory '/opensource/oppia_tools/redis-cli-6.0.10/deps'
   (rm -f .make-*)
   echo STD=-std=c11 -pedantic -DREDIS_STATIC='' >> .make-settings
   echo WARN=-Wall -W -Wno-missing-field-initializers >> .make-settings
   echo OPT=-O2 >> .make-settings
   echo MALLOC=jemalloc >> .make-settings
   echo BUILD_TLS= >> .make-settings
   echo USE_SYSTEMD= >> .make-settings
   echo CFLAGS= >> .make-settings
   echo LDFLAGS= >> .make-settings
   echo REDIS_CFLAGS= >> .make-settings
   echo REDIS_LDFLAGS= >> .make-settings
   echo PREV_FINAL_CFLAGS=-std=c11 -pedantic -DREDIS_STATIC='' -Wall -W -Wno-missing-field-initializers -O2 -g -ggdb   -I../deps/hiredis -I../deps/linenoise -I../deps/lua/src -DUSE_JEMALLOC -I../deps/jemalloc/include >> .make-settings
   echo PREV_FINAL_LDFLAGS=  -g -ggdb -rdynamic >> .make-settings
   (cd ../deps && make hiredis linenoise lua jemalloc)
   make[2]: Entering directory '/opensource/oppia_tools/redis-cli-6.0.10/deps'
   (cd hiredis && make clean) > /dev/null || true
   (cd linenoise && make clean) > /dev/null || true
   (cd lua && make clean) > /dev/null || true
   (cd jemalloc && [ -f Makefile ] && make distclean) > /dev/null || true
   (rm -f .make-*)
   (echo "" > .make-cflags)
   (echo "" > .make-ldflags)
   MAKE hiredis
   cd hiredis && make static 
   make[3]: Entering directory '/opensource/oppia_tools/redis-cli-6.0.10/deps/hiredis'
   cc -std=c99 -pedantic -c -O3 -fPIC   -Wall -W -Wstrict-prototypes -Wwrite-strings -Wno-missing-field-initializers -g -ggdb net.c
   cc -std=c99 -pedantic -c -O3 -fPIC   -Wall -W -Wstrict-prototypes -Wwrite-strings -Wno-missing-field-initializers -g -ggdb hiredis.c
   cc -std=c99 -pedantic -c -O3 -fPIC   -Wall -W -Wstrict-prototypes -Wwrite-strings -Wno-missing-field-initializers -g -ggdb sds.c
   cc -std=c99 -pedantic -c -O3 -fPIC   -Wall -W -Wstrict-prototypes -Wwrite-strings -Wno-missing-field-initializers -g -ggdb async.c
   cc -std=c99 -pedantic -c -O3 -fPIC   -Wall -W -Wstrict-prototypes -Wwrite-strings -Wno-missing-field-initializers -g -ggdb read.c
   cc -std=c99 -pedantic -c -O3 -fPIC   -Wall -W -Wstrict-prototypes -Wwrite-strings -Wno-missing-field-initializers -g -ggdb sockcompat.c
   ar rcs libhiredis.a net.o hiredis.o sds.o async.o read.o sockcompat.o
   make[3]: Leaving directory '/opensource/oppia_tools/redis-cli-6.0.10/deps/hiredis'
   MAKE linenoise
   cd linenoise && make
   make[3]: Entering directory '/opensource/oppia_tools/redis-cli-6.0.10/deps/linenoise'
   cc  -Wall -Os -g  -c linenoise.c
   make[3]: Leaving directory '/opensource/oppia_tools/redis-cli-6.0.10/deps/linenoise'
   MAKE lua
   cd lua/src && make all CFLAGS="-O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC='' " MYLDFLAGS="" AR="ar rcu"
   make[3]: Entering directory '/opensource/oppia_tools/redis-cli-6.0.10/deps/lua/src'
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lapi.o lapi.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lcode.o lcode.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ldebug.o ldebug.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ldo.o ldo.c
   ldo.c: In function ‘f_parser’:
   ldo.c:496:7: warning: unused variable ‘c’ [-Wunused-variable]
     496 |   int c = luaZ_lookahead(p->z);
         |       ^
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
   lauxlib.c: In function ‘luaL_loadfile’:
   lauxlib.c:577:4: warning: this ‘while’ clause does not guard... [-Wmisleading-indentation]
     577 |    while ((c = getc(lf.f)) != EOF && c != LUA_SIGNATURE[0]) ;
         |    ^~~~~
   lauxlib.c:578:5: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘while’
     578 |     lf.extraline = 0;
         |     ^~
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lbaselib.o lbaselib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ldblib.o ldblib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o liolib.o liolib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lmathlib.o lmathlib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o loslib.o loslib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ltablib.o ltablib.c
   ltablib.c: In function ‘addfield’:
   ltablib.c:137:3: warning: this ‘if’ clause does not guard... [-Wmisleading-indentation]
     137 |   if (!lua_isstring(L, -1))
         |   ^~
   ltablib.c:140:5: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘if’
     140 |     luaL_addvalue(b);
         |     ^~~~~~~~~~~~~
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lstrlib.o lstrlib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o loadlib.o loadlib.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o linit.o linit.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua_cjson.o lua_cjson.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua_struct.o lua_struct.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua_cmsgpack.o lua_cmsgpack.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua_bit.o lua_bit.c
   ar rcu liblua.a lapi.o lcode.o ldebug.o ldo.o ldump.o lfunc.o lgc.o llex.o lmem.o lobject.o lopcodes.o lparser.o lstate.o lstring.o ltable.o ltm.o lundump.o lvm.o lzio.o strbuf.o fpconv.o lauxlib.o lbaselib.o ldblib.o liolib.o lmathlib.o loslib.o ltablib.o lstrlib.o loadlib.o linit.o lua_cjson.o lua_struct.o lua_cmsgpack.o lua_bit.o	# DLL needs all object files
   ar: `u' modifier ignored since `D' is the default (see `U')
   ranlib liblua.a
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua.o lua.c
   cc -o lua  lua.o liblua.a -lm 
   /usr/bin/ld: liblua.a(loslib.o): in function `os_tmpname':
   loslib.c:(.text+0x2b5): warning: the use of `tmpnam' is dangerous, better use `mkstemp'
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o luac.o luac.c
   cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o print.o print.c
   cc -o luac  luac.o print.o liblua.a -lm 
   make[3]: Leaving directory '/opensource/oppia_tools/redis-cli-6.0.10/deps/lua/src'
   MAKE jemalloc
   cd jemalloc && ./configure --with-version=5.1.0-0-g0 --with-lg-quantum=3 --with-jemalloc-prefix=je_ --enable-cc-silence CFLAGS="-std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops " LDFLAGS=""
   configure: WARNING: unrecognized options: --enable-cc-silence
   checking for xsltproc... false
   checking for gcc... gcc
   checking whether the C compiler works... yes
   checking for C compiler default output file name... a.out
   checking for suffix of executables... 
   checking whether we are cross compiling... no
   checking for suffix of object files... o
   checking whether we are using the GNU C compiler... yes
   checking whether gcc accepts -g... yes
   checking for gcc option to accept ISO C89... none needed
   checking whether compiler is cray... no
   checking whether compiler supports -std=gnu11... yes
   checking whether compiler supports -Wall... yes
   checking whether compiler supports -Wshorten-64-to-32... no
   checking whether compiler supports -Wsign-compare... yes
   checking whether compiler supports -Wundef... yes
   checking whether compiler supports -Wno-format-zero-length... yes
   checking whether compiler supports -pipe... yes
   checking whether compiler supports -g3... yes
   checking how to run the C preprocessor... gcc -E
   checking for g++... g++
   checking whether we are using the GNU C++ compiler... yes
   checking whether g++ accepts -g... yes
   checking whether g++ supports C++14 features by default... yes
   checking whether compiler supports -Wall... yes
   checking whether compiler supports -g3... yes
   checking whether libstdc++ linkage is compilable... yes
   checking for grep that handles long lines and -e... /usr/bin/grep
   checking for egrep... /usr/bin/grep -E
   checking for ANSI C header files... yes
   checking for sys/types.h... yes
   checking for sys/stat.h... yes
   checking for stdlib.h... yes
   checking for string.h... yes
   checking for memory.h... yes
   checking for strings.h... yes
   checking for inttypes.h... yes
   checking for stdint.h... yes
   checking for unistd.h... yes
   checking whether byte ordering is bigendian... no
   checking size of void *... 8
   checking size of int... 4
   checking size of long... 8
   checking size of long long... 8
   checking size of intmax_t... 8
   checking build system type... x86_64-pc-linux-gnu
   checking host system type... x86_64-pc-linux-gnu
   checking whether pause instruction is compilable... yes
   checking number of significant virtual address bits... 48
   checking for ar... ar
   checking for nm... nm
   checking for gawk... no
   checking for mawk... mawk
   checking malloc.h usability... yes
   checking malloc.h presence... yes
   checking for malloc.h... yes
   checking whether malloc_usable_size definition can use const argument... no
   checking for library containing log... -lm
   checking whether __attribute__ syntax is compilable... yes
   checking whether compiler supports -fvisibility=hidden... yes
   checking whether compiler supports -fvisibility=hidden... yes
   checking whether compiler supports -Werror... yes
   checking whether compiler supports -herror_on_warning... no
   checking whether tls_model attribute is compilable... yes
   checking whether compiler supports -Werror... yes
   checking whether compiler supports -herror_on_warning... no
   checking whether alloc_size attribute is compilable... yes
   checking whether compiler supports -Werror... yes
   checking whether compiler supports -herror_on_warning... no
   checking whether format(gnu_printf, ...) attribute is compilable... yes
   checking whether compiler supports -Werror... yes
   checking whether compiler supports -herror_on_warning... no
   checking whether format(printf, ...) attribute is compilable... yes
   checking for a BSD-compatible install... /usr/bin/install -c
   checking for ranlib... ranlib
   checking for ld... /usr/bin/ld
   checking for autoconf... false
   checking for memalign... yes
   checking for valloc... yes
   checking whether compiler supports -O3... yes
   checking whether compiler supports -O3... yes
   checking whether compiler supports -funroll-loops... yes
   checking configured backtracing method... N/A
   checking for sbrk... yes
   checking whether utrace(2) is compilable... no
   checking whether a program using __builtin_unreachable is compilable... yes
   checking whether a program using __builtin_ffsl is compilable... yes
   checking LG_PAGE... 12
   checking pthread.h usability... yes
   checking pthread.h presence... yes
   checking for pthread.h... yes
   checking for pthread_create in -lpthread... yes
   checking dlfcn.h usability... yes
   checking dlfcn.h presence... yes
   checking for dlfcn.h... yes
   checking for dlsym... no
   checking for dlsym in -ldl... yes
   checking whether pthread_atfork(3) is compilable... yes
   checking whether pthread_setname_np(3) is compilable... yes
   checking for library containing clock_gettime... none required
   checking whether clock_gettime(CLOCK_MONOTONIC_COARSE, ...) is compilable... yes
   checking whether clock_gettime(CLOCK_MONOTONIC, ...) is compilable... yes
   checking whether mach_absolute_time() is compilable... no
   checking whether compiler supports -Werror... yes
   checking whether syscall(2) is compilable... yes
   checking for secure_getenv... yes
   checking for sched_getcpu... yes
   checking for sched_setaffinity... yes
   checking for issetugid... no
   checking for _malloc_thread_cleanup... no
   checking for _pthread_mutex_init_calloc_cb... no
   checking for TLS... yes
   checking whether C11 atomics is compilable... no
   checking whether GCC __atomic atomics is compilable... yes
   checking whether GCC __sync atomics is compilable... yes
   checking whether Darwin OSAtomic*() is compilable... no
   checking whether madvise(2) is compilable... yes
   checking whether madvise(..., MADV_FREE) is compilable... yes
   checking whether madvise(..., MADV_DONTNEED) is compilable... yes
   checking whether madvise(..., MADV_DO[NT]DUMP) is compilable... yes
   checking whether madvise(..., MADV_[NO]HUGEPAGE) is compilable... yes
   checking whether to force 32-bit __sync_{add,sub}_and_fetch()... no
   checking whether to force 64-bit __sync_{add,sub}_and_fetch()... no
   checking for __builtin_clz... yes
   checking whether Darwin os_unfair_lock_*() is compilable... no
   checking whether Darwin OSSpin*() is compilable... no
   checking whether glibc malloc hook is compilable... yes
   checking whether glibc memalign hook is compilable... yes
   checking whether pthreads adaptive mutexes is compilable... yes
   checking whether compiler supports -D_GNU_SOURCE... yes
   checking whether compiler supports -Werror... yes
   checking whether compiler supports -herror_on_warning... no
   checking whether strerror_r returns char with gnu source is compilable... yes
   checking for stdbool.h that conforms to C99... yes
   checking for _Bool... yes
   configure: creating ./config.status
   config.status: creating Makefile
   config.status: creating jemalloc.pc
   config.status: creating doc/html.xsl
   config.status: creating doc/manpages.xsl
   config.status: creating doc/jemalloc.xml
   config.status: creating include/jemalloc/jemalloc_macros.h
   config.status: creating include/jemalloc/jemalloc_protos.h
   config.status: creating include/jemalloc/jemalloc_typedefs.h
   config.status: creating include/jemalloc/internal/jemalloc_preamble.h
   config.status: creating test/test.sh
   config.status: creating test/include/test/jemalloc_test.h
   config.status: creating config.stamp
   config.status: creating bin/jemalloc-config
   config.status: creating bin/jemalloc.sh
   config.status: creating bin/jeprof
   config.status: creating include/jemalloc/jemalloc_defs.h
   config.status: creating include/jemalloc/internal/jemalloc_internal_defs.h
   config.status: creating test/include/test/jemalloc_test_defs.h
   config.status: executing include/jemalloc/internal/public_symbols.txt commands
   config.status: executing include/jemalloc/internal/private_symbols.awk commands
   config.status: executing include/jemalloc/internal/private_symbols_jet.awk commands
   config.status: executing include/jemalloc/internal/public_namespace.h commands
   config.status: executing include/jemalloc/internal/public_unnamespace.h commands
   config.status: executing include/jemalloc/internal/size_classes.h commands
   config.status: executing include/jemalloc/jemalloc_protos_jet.h commands
   config.status: executing include/jemalloc/jemalloc_rename.h commands
   config.status: executing include/jemalloc/jemalloc_mangle.h commands
   config.status: executing include/jemalloc/jemalloc_mangle_jet.h commands
   config.status: executing include/jemalloc/jemalloc.h commands
   configure: WARNING: unrecognized options: --enable-cc-silence
   ===============================================================================
   jemalloc version   : 5.1.0-0-g0
   library revision   : 2
   
   CONFIG             : --with-version=5.1.0-0-g0 --with-lg-quantum=3 --with-jemalloc-prefix=je_ --enable-cc-silence 'CFLAGS=-std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops ' LDFLAGS=
   CC                 : gcc
   CONFIGURE_CFLAGS   : -std=gnu11 -Wall -Wsign-compare -Wundef -Wno-format-zero-length -pipe -g3 -fvisibility=hidden -O3 -funroll-loops
   SPECIFIED_CFLAGS   : -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops 
   EXTRA_CFLAGS       : 
   CPPFLAGS           : -D_GNU_SOURCE -D_REENTRANT
   CXX                : g++
   CONFIGURE_CXXFLAGS : -Wall -g3 -fvisibility=hidden -O3
   SPECIFIED_CXXFLAGS : 
   EXTRA_CXXFLAGS     : 
   LDFLAGS            : 
   EXTRA_LDFLAGS      : 
   DSO_LDFLAGS        : -shared -Wl,-soname,$(@F)
   LIBS               : -lm -lstdc++ -lpthread -ldl
   RPATH_EXTRA        : 
   
   XSLTPROC           : false
   XSLROOT            : 
   
   PREFIX             : /usr/local
   BINDIR             : /usr/local/bin
   DATADIR            : /usr/local/share
   INCLUDEDIR         : /usr/local/include
   LIBDIR             : /usr/local/lib
   MANDIR             : /usr/local/share/man
   
   srcroot            : 
   abs_srcroot        : /opensource/oppia_tools/redis-cli-6.0.10/deps/jemalloc/
   objroot            : 
   abs_objroot        : /opensource/oppia_tools/redis-cli-6.0.10/deps/jemalloc/
   
   JEMALLOC_PREFIX    : je_
   JEMALLOC_PRIVATE_NAMESPACE
                      : je_
   install_suffix     : 
   malloc_conf        : 
   autogen            : 0
   debug              : 0
   stats              : 1
   prof               : 0
   prof-libunwind     : 0
   prof-libgcc        : 0
   prof-gcc           : 0
   fill               : 1
   utrace             : 0
   xmalloc            : 0
   log                : 0
   lazy_lock          : 0
   cache-oblivious    : 1
   cxx                : 1
   ===============================================================================
   cd jemalloc && make CFLAGS="-std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops " LDFLAGS="" lib/libjemalloc.a
   make[3]: Entering directory '/opensource/oppia_tools/redis-cli-6.0.10/deps/jemalloc'
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/jemalloc.sym.o src/jemalloc.c
   nm -a src/jemalloc.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/jemalloc.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/arena.sym.o src/arena.c
   nm -a src/arena.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/arena.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/background_thread.sym.o src/background_thread.c
   nm -a src/background_thread.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/background_thread.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/base.sym.o src/base.c
   nm -a src/base.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/base.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/bin.sym.o src/bin.c
   nm -a src/bin.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/bin.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/bitmap.sym.o src/bitmap.c
   nm -a src/bitmap.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/bitmap.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/ckh.sym.o src/ckh.c
   nm -a src/ckh.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/ckh.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/ctl.sym.o src/ctl.c
   nm -a src/ctl.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/ctl.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/div.sym.o src/div.c
   nm -a src/div.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/div.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/extent.sym.o src/extent.c
   nm -a src/extent.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/extent.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/extent_dss.sym.o src/extent_dss.c
   nm -a src/extent_dss.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/extent_dss.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/extent_mmap.sym.o src/extent_mmap.c
   nm -a src/extent_mmap.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/extent_mmap.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/hash.sym.o src/hash.c
   nm -a src/hash.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/hash.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/hooks.sym.o src/hooks.c
   nm -a src/hooks.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/hooks.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/large.sym.o src/large.c
   nm -a src/large.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/large.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/log.sym.o src/log.c
   nm -a src/log.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/log.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/malloc_io.sym.o src/malloc_io.c
   src/malloc_io.c: In function ‘malloc_vsnprintf’:
   src/malloc_io.c:369:2: warning: case label value exceeds maximum value for type [-Wswitch-outside-range]
     369 |  case '?' | 0x80:      \
         |  ^~~~
   src/malloc_io.c:581:5: note: in expansion of macro ‘GET_ARG_NUMERIC’
     581 |     GET_ARG_NUMERIC(val, 'p');
         |     ^~~~~~~~~~~~~~~
   src/malloc_io.c:387:2: warning: case label value exceeds maximum value for type [-Wswitch-outside-range]
     387 |  case 'j' | 0x80:      \
         |  ^~~~
   src/malloc_io.c:581:5: note: in expansion of macro ‘GET_ARG_NUMERIC’
     581 |     GET_ARG_NUMERIC(val, 'p');
         |     ^~~~~~~~~~~~~~~
   src/malloc_io.c:375:2: warning: case label value exceeds maximum value for type [-Wswitch-outside-range]
     375 |  case 'l' | 0x80:      \
         |  ^~~~
   src/malloc_io.c:581:5: note: in expansion of macro ‘GET_ARG_NUMERIC’
     581 |     GET_ARG_NUMERIC(val, 'p');
         |     ^~~~~~~~~~~~~~~
   src/malloc_io.c:381:2: warning: case label value exceeds maximum value for type [-Wswitch-outside-range]
     381 |  case 'q' | 0x80:      \
         |  ^~~~
   src/malloc_io.c:581:5: note: in expansion of macro ‘GET_ARG_NUMERIC’
     581 |     GET_ARG_NUMERIC(val, 'p');
         |     ^~~~~~~~~~~~~~~
   src/malloc_io.c:396:2: warning: case label value exceeds maximum value for type [-Wswitch-outside-range]
     396 |  case 'z' | 0x80:      \
         |  ^~~~
   src/malloc_io.c:581:5: note: in expansion of macro ‘GET_ARG_NUMERIC’
     581 |     GET_ARG_NUMERIC(val, 'p');
         |     ^~~~~~~~~~~~~~~
   nm -a src/malloc_io.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/malloc_io.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/mutex.sym.o src/mutex.c
   nm -a src/mutex.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/mutex.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/mutex_pool.sym.o src/mutex_pool.c
   nm -a src/mutex_pool.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/mutex_pool.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/nstime.sym.o src/nstime.c
   nm -a src/nstime.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/nstime.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/pages.sym.o src/pages.c
   nm -a src/pages.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/pages.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/prng.sym.o src/prng.c
   nm -a src/prng.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/prng.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/prof.sym.o src/prof.c
   nm -a src/prof.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/prof.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/rtree.sym.o src/rtree.c
   nm -a src/rtree.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/rtree.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/stats.sym.o src/stats.c
   nm -a src/stats.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/stats.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/sz.sym.o src/sz.c
   nm -a src/sz.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/sz.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/tcache.sym.o src/tcache.c
   nm -a src/tcache.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/tcache.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/ticker.sym.o src/ticker.c
   nm -a src/ticker.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/ticker.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/tsd.sym.o src/tsd.c
   nm -a src/tsd.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/tsd.sym
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -DJEMALLOC_NO_PRIVATE_NAMESPACE -o src/witness.sym.o src/witness.c
   nm -a src/witness.sym.o | mawk -f include/jemalloc/internal/private_symbols.awk > src/witness.sym
   /bin/sh include/jemalloc/internal/private_namespace.sh src/jemalloc.sym src/arena.sym src/background_thread.sym src/base.sym src/bin.sym src/bitmap.sym src/ckh.sym src/ctl.sym src/div.sym src/extent.sym src/extent_dss.sym src/extent_mmap.sym src/hash.sym src/hooks.sym src/large.sym src/log.sym src/malloc_io.sym src/mutex.sym src/mutex_pool.sym src/nstime.sym src/pages.sym src/prng.sym src/prof.sym src/rtree.sym src/stats.sym src/sz.sym src/tcache.sym src/ticker.sym src/tsd.sym src/witness.sym > include/jemalloc/internal/private_namespace.gen.h
   cp include/jemalloc/internal/private_namespace.gen.h include/jemalloc/internal/private_namespace.gen.h
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/jemalloc.o src/jemalloc.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/arena.o src/arena.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/background_thread.o src/background_thread.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/base.o src/base.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/bin.o src/bin.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/bitmap.o src/bitmap.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/ckh.o src/ckh.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/ctl.o src/ctl.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/div.o src/div.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/extent.o src/extent.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/extent_dss.o src/extent_dss.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/extent_mmap.o src/extent_mmap.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/hash.o src/hash.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/hooks.o src/hooks.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/large.o src/large.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/log.o src/log.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/malloc_io.o src/malloc_io.c
   src/malloc_io.c: In function ‘je_malloc_vsnprintf’:
   src/malloc_io.c:369:2: warning: case label value exceeds maximum value for type [-Wswitch-outside-range]
     369 |  case '?' | 0x80:      \
         |  ^~~~
   src/malloc_io.c:581:5: note: in expansion of macro ‘GET_ARG_NUMERIC’
     581 |     GET_ARG_NUMERIC(val, 'p');
         |     ^~~~~~~~~~~~~~~
   src/malloc_io.c:387:2: warning: case label value exceeds maximum value for type [-Wswitch-outside-range]
     387 |  case 'j' | 0x80:      \
         |  ^~~~
   src/malloc_io.c:581:5: note: in expansion of macro ‘GET_ARG_NUMERIC’
     581 |     GET_ARG_NUMERIC(val, 'p');
         |     ^~~~~~~~~~~~~~~
   src/malloc_io.c:375:2: warning: case label value exceeds maximum value for type [-Wswitch-outside-range]
     375 |  case 'l' | 0x80:      \
         |  ^~~~
   src/malloc_io.c:581:5: note: in expansion of macro ‘GET_ARG_NUMERIC’
     581 |     GET_ARG_NUMERIC(val, 'p');
         |     ^~~~~~~~~~~~~~~
   src/malloc_io.c:381:2: warning: case label value exceeds maximum value for type [-Wswitch-outside-range]
     381 |  case 'q' | 0x80:      \
         |  ^~~~
   src/malloc_io.c:581:5: note: in expansion of macro ‘GET_ARG_NUMERIC’
     581 |     GET_ARG_NUMERIC(val, 'p');
         |     ^~~~~~~~~~~~~~~
   src/malloc_io.c:396:2: warning: case label value exceeds maximum value for type [-Wswitch-outside-range]
     396 |  case 'z' | 0x80:      \
         |  ^~~~
   src/malloc_io.c:581:5: note: in expansion of macro ‘GET_ARG_NUMERIC’
     581 |     GET_ARG_NUMERIC(val, 'p');
         |     ^~~~~~~~~~~~~~~
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/mutex.o src/mutex.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/mutex_pool.o src/mutex_pool.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/nstime.o src/nstime.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/pages.o src/pages.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/prng.o src/prng.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/prof.o src/prof.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/rtree.o src/rtree.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/stats.o src/stats.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/sz.o src/sz.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/tcache.o src/tcache.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/ticker.o src/ticker.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/tsd.o src/tsd.c
   gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/witness.o src/witness.c
   g++ -Wall -g3 -fvisibility=hidden -O3 -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/jemalloc_cpp.o src/jemalloc_cpp.cpp
   ar crus lib/libjemalloc.a src/jemalloc.o src/arena.o src/background_thread.o src/base.o src/bin.o src/bitmap.o src/ckh.o src/ctl.o src/div.o src/extent.o src/extent_dss.o src/extent_mmap.o src/hash.o src/hooks.o src/large.o src/log.o src/malloc_io.o src/mutex.o src/mutex_pool.o src/nstime.o src/pages.o src/prng.o src/prof.o src/rtree.o src/stats.o src/sz.o src/tcache.o src/ticker.o src/tsd.o src/witness.o src/jemalloc_cpp.o
   ar: `u' modifier ignored since `D' is the default (see `U')
   make[3]: Leaving directory '/opensource/oppia_tools/redis-cli-6.0.10/deps/jemalloc'
   make[2]: Leaving directory '/opensource/oppia_tools/redis-cli-6.0.10/deps'
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
   
   make[1]: Leaving directory '/opensource/oppia_tools/redis-cli-6.0.10/src'
   Redis-cli installed successfully.
   Installing ElasticSearch...
   Downloading and untarring file elasticsearch-7.10.1 to ../oppia_tools ...
   Download of elasticsearch-7.10.1 succeeded.
   ElasticSearch installed successfully.
   Copying Google Cloud SDK modules to third_party/python_libs...
   Checking that all google library modules contain __init__.py files...
   yarn install v1.22.10
   [1/4] Resolving packages...
   [2/4] Fetching packages...
   warning Pattern ["@definitelytyped/typescript-versions@latest"] is trying to unpack in the same destination "/home/user/.cache/yarn/v6/npm-@definitelytyped-typescript-versions-0.0.84-3cead40ca6131542609e8e3e621a23b8e72f7ddf-integrity/node_modules/@definitelytyped/typescript-versions" as pattern ["@definitelytyped/typescript-versions@^0.0.84","@definitelytyped/typescript-versions@^0.0.84","@definitelytyped/typescript-versions@^0.0.84"]. This could result in non-deterministic behavior, skipping.
   info There appears to be trouble with your network connection. Retrying...
   info There appears to be trouble with your network connection. Retrying...
   info There appears to be trouble with your network connection. Retrying...
   info fsevents@2.3.2: The platform "linux" is incompatible with this module.
   info "fsevents@2.3.2" is an optional dependency and failed compatibility check. Excluding it from installation.
   info fsevents@1.2.13: The platform "linux" is incompatible with this module.
   info "fsevents@1.2.13" is an optional dependency and failed compatibility check. Excluding it from installation.
   [3/4] Linking dependencies...
   warning " > @angular/elements@11.2.10" has incorrect peer dependency "@angular/core@11.2.10".
   warning " > @angular/elements@11.2.10" has incorrect peer dependency "@angular/platform-browser@11.2.10".
   warning " > @asymmetrik/ngx-leaflet@8.1.0" has unmet peer dependency "tslib@2".
   warning " > @ng-bootstrap/ng-bootstrap@8.0.4" has incorrect peer dependency "@angular/common@^10.0.0".
   warning " > @ng-bootstrap/ng-bootstrap@8.0.4" has incorrect peer dependency "@angular/core@^10.0.0".
   warning " > @ng-bootstrap/ng-bootstrap@8.0.4" has incorrect peer dependency "@angular/forms@^10.0.0".
   warning " > @ng-bootstrap/ng-bootstrap@8.0.4" has unmet peer dependency "@angular/localize@^10.0.0".
   warning " > bootstrap@4.6.0" has unmet peer dependency "popper.js@^1.16.1".
   warning " > ngx-translate-cache@9.0.2" has incorrect peer dependency "@angular/common@^9.1.0".
   warning " > ngx-translate-cache@9.0.2" has incorrect peer dependency "@angular/core@^9.1.0".
   warning " > ngx-translate-cache@9.0.2" has unmet peer dependency "tslib@^1.10.0".
   [4/4] Building fresh packages...
   Done in 560.87s.
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
   i  ui: downloading ui-v1.4.2.zip...
   Starting new Webpack Compiler: /opensource/oppia/../oppia_tools/node-14.15.0/bin/node /opensource/oppia/node_modules/webpack/bin/webpack.js --config webpack.dev.config.ts --color --watch --progress
   Progress: ==============================================================================================================> (100% of 4MB)
   i  ui: Emulator UI logging to ui-debug.log
   
   ┌─────────────────────────────────────────────────────────────┐
   │ ✔  All emulators ready! It is now safe to connect your app. │
   │ i  View Emulator UI at http://localhost:4000                │
   └─────────────────────────────────────────────────────────────┘
   
   ┌────────────────┬────────────────┬────────────────────────────┐
   │ Emulator       │ Host:Port      │ View in Emulator UI        │
   ├────────────────┼────────────────┼────────────────────────────┤
   │ Authentication │ localhost:9099 │ http://localhost:4000/auth │
   └────────────────┴────────────────┴────────────────────────────┘
     Emulator Hub running at localhost:4400
     Other reserved ports: 4500
   
   Issues? Report them at https://github.com/firebase/firebase-tools/issues and attach the *-debug.log files.
    
   10% building 0/0 modules 0 active
   webpack is watching the files…
   
   Hash: 3b95e4c98b43cf9b1ab3
   Version: webpack 4.46.0
   Time: 192714ms
   Built at: 07/18/2021 8:23:42 PM
   Starting new GAE Development Server: /home/user/.pyenv/versions/oppia-tmp/bin/python /opensource/oppia_tools/google-cloud-sdk-335.0.0/google-cloud-sdk/platform/google_appengine/dev_appserver.py --host 0.0.0.0 --port 8181 --admin_host 0.0.0.0 --admin_port 8000 --clear_datastore true --enable_console false --enable_host_checking true --automatic_restart true --skip_sdk_update_check true --log_level info --dev_appserver_log_level info app_dev.yaml
                                                                                                                     Asset      Size                                                                                                         Chunks             Chunk Names
                                                                                                  about-page.mainpage.html  4.47 KiB                                                                                                                 [emitted]  
                                                                                                           about.bundle.js  53.9 KiB                                                                                                          about  [emitted]  about
   about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js  5.01 MiB  about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff  [emitted]  about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff
                                                                                                  admin-page.mainpage.html  4.05 KiB                                                                                                                 [emitted]  
                                                                                                           admin.bundle.js   154 KiB                                                                                                          admin  [emitted]  admin
                                                                                                admin~blog_admin.bundle.js  14.6 KiB                                                                                               admin~blog_admin  [emitted]  admin~blog_admin
   admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js  1.96 MiB  admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2  [emitted]  admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2
                                                                                             blog-admin-page.mainpage.html  4.04 KiB                                                                                                                 [emitted]  
                                                                                                      blog_admin.bundle.js  41.7 KiB                                                                                                     blog_admin  [emitted]  blog_admin
                                                                                              classroom-page.mainpage.html   5.3 KiB                                                                                                                 [emitted]  
                                                                                                       classroom.bundle.js  46.4 KiB                                                                                                      classroom  [emitted]  classroom
                                                                                      collection-editor-page.mainpage.html  5.63 KiB                                                                                                                 [emitted]  
                                                                                      collection-player-page.mainpage.html  7.41 KiB                                                                                                                 [emitted]  
                                                                                               collection_editor.bundle.js   117 KiB                                                                                              collection_editor  [emitted]  collection_editor
                            collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js  98.7 KiB                           collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor  [emitted]  collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor
   collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor~topics_and_skil~68685f5f.bundle.js  78.9 KiB  collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor~topics_and_skil~68685f5f  [emitted]  collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor~topics_and_skil~68685f5f
                                                                                               collection_player.bundle.js    69 KiB                                                                                              collection_player  [emitted]  collection_player
                                                                                                  console_errors.bundle.js  17.5 KiB                                                                                                 console_errors  [emitted]  console_errors
                                                                                                       console_errors.html  5.15 KiB                                                                                                                 [emitted]  
                                                                                                contact-page.mainpage.html   4.2 KiB                                                                                                                 [emitted]  
                                                                                                         contact.bundle.js  29.7 KiB                                                                                                        contact  [emitted]  contact
                                                                            contributor-dashboard-admin-page.mainpage.html  3.97 KiB                                                                                                                 [emitted]  
                                                                                  contributor-dashboard-page.mainpage.html  6.41 KiB                                                                                                                 [emitted]  
                                                                                           contributor_dashboard.bundle.js   246 KiB                                                                                          contributor_dashboard  [emitted]  contributor_dashboard
                                                                                     contributor_dashboard_admin.bundle.js  51.2 KiB                                                                                    contributor_dashboard_admin  [emitted]  contributor_dashboard_admin
   contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js   835 KiB  contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33  [emitted]  contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33
         contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js   145 KiB        contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor  [emitted]  contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor
               contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js  22.7 KiB              contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor  [emitted]  contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor
   contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js   196 KiB  contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53  [emitted]  contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53
                                              contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js  1.18 MiB                                             contributor_dashboard~exploration_editor~skill_editor~topic_editor  [emitted]  contributor_dashboard~exploration_editor~skill_editor~topic_editor
                                                                 contributor_dashboard~skill_editor~topic_editor.bundle.js  31.9 KiB                                                                contributor_dashboard~skill_editor~topic_editor  [emitted]  contributor_dashboard~skill_editor~topic_editor
                                                                                      creator-dashboard-page.mainpage.html  5.96 KiB                                                                                                                 [emitted]  
                                                                                               creator_dashboard.bundle.js  97.5 KiB                                                                                              creator_dashboard  [emitted]  creator_dashboard
                                                                                         delete-account-page.mainpage.html  4.25 KiB                                                                                                                 [emitted]  
                                                                                                  delete_account.bundle.js  43.8 KiB                                                                                                 delete_account  [emitted]  delete_account
                                                                                                 donate-page.mainpage.html  4.21 KiB                                                                                                                 [emitted]  
                                                                                                          donate.bundle.js  36.7 KiB                                                                                                         donate  [emitted]  donate
                                                                                        email-dashboard-page.mainpage.html  5.34 KiB                                                                                                                 [emitted]  
                                                                                      email-dashboard-result.mainpage.html  5.24 KiB                                                                                                                 [emitted]  
                                                                                                 email_dashboard.bundle.js  28.6 KiB                                                                                                email_dashboard  [emitted]  email_dashboard
                                                                                          email_dashboard_result.bundle.js  28.3 KiB                                                                                         email_dashboard_result  [emitted]  email_dashboard_result
                                                                                               error-iframed.mainpage.html  6.33 KiB                                                                                                                 [emitted]  
                                                                                              error-page-400.mainpage.html  4.88 KiB                                                                                                                 [emitted]  
                                                                                              error-page-401.mainpage.html  4.88 KiB                                                                                                                 [emitted]  
                                                                                              error-page-404.mainpage.html  4.88 KiB                                                                                                                 [emitted]  
                                                                                              error-page-500.mainpage.html  4.88 KiB                                                                                                                 [emitted]  
                                                                                                           error.bundle.js  25.6 KiB                                                                                                          error  [emitted]  error
                                                                                     exploration-editor-page.mainpage.html  9.18 KiB                                                                                                                 [emitted]  
                                                                                     exploration-player-page.mainpage.html  8.09 KiB                                                                                                                 [emitted]  
                                                                                              exploration_editor.bundle.js  74.9 KiB                                                                                             exploration_editor  [emitted]  exploration_editor
                                                                           exploration_editor~exploration_player.bundle.js  1.17 MiB                                                                          exploration_editor~exploration_player  [emitted]  exploration_editor~exploration_player
                                                                                              exploration_player.bundle.js  39.4 KiB                                                                                             exploration_player  [emitted]  exploration_player
                                                    exploration_player~practice_session~review_test~skill_editor.bundle.js  67.3 KiB                                                   exploration_player~practice_session~review_test~skill_editor  [emitted]  exploration_player~practice_session~review_test~skill_editor
                                                                                            get-started-page.mainpage.html  4.33 KiB                                                                                                                 [emitted]  
                                                                                                     get_started.bundle.js  25.5 KiB                                                                                                    get_started  [emitted]  get_started
                                                                                                         landing.bundle.js  45.6 KiB                                                                                                        landing  [emitted]  landing
                                                                                      learner-dashboard-page.mainpage.html  6.13 KiB                                                                                                                 [emitted]  
                                                                                               learner_dashboard.bundle.js   208 KiB                                                                                              learner_dashboard  [emitted]  learner_dashboard
                                                                                                library-page.mainpage.html  5.38 KiB                                                                                                                 [emitted]  
                                                                                                         library.bundle.js  86.6 KiB                                                                                                        library  [emitted]  library
                                                                                                         license.bundle.js  22.4 KiB                                                                                                        license  [emitted]  license
                                                                                                     license.mainpage.html  4.83 KiB                                                                                                                 [emitted]  
                                                                                                  login-page.mainpage.html  4.21 KiB                                                                                                                 [emitted]  
                                                                                                           login.bundle.js  39.2 KiB                                                                                                          login  [emitted]  login
                                                                                                 logout-page.mainpage.html  5.21 KiB                                                                                                                 [emitted]  
                                                                                                          logout.bundle.js  23.4 KiB                                                                                                         logout  [emitted]  logout
                                                                                            maintenance-page.mainpage.html  4.01 KiB                                                                                                                 [emitted]  
                                                                                                     maintenance.bundle.js  25.7 KiB                                                                                                    maintenance  [emitted]  maintenance
                                                                                              moderator-page.mainpage.html  5.24 KiB                                                                                                                 [emitted]  
                                                                                                       moderator.bundle.js  33.1 KiB                                                                                                      moderator  [emitted]  moderator
                                                                                           partnerships-page.mainpage.html  4.24 KiB                                                                                                                 [emitted]  
                                                                                                    partnerships.bundle.js  41.8 KiB                                                                                                   partnerships  [emitted]  partnerships
                                                                               pending-account-deletion-page.mainpage.html  4.44 KiB                                                                                                                 [emitted]  
                                                                                        pending_account_deletion.bundle.js  30.4 KiB                                                                                       pending_account_deletion  [emitted]  pending_account_deletion
                                                                                                        playbook.bundle.js  28.6 KiB                                                                                                       playbook  [emitted]  playbook
                                                                                                    playbook.mainpage.html  5.06 KiB                                                                                                                 [emitted]  
                                                                                       practice-session-page.mainpage.html  6.07 KiB                                                                                                                 [emitted]  
                                                                                                practice_session.bundle.js  30.6 KiB                                                                                               practice_session  [emitted]  practice_session
                                                                       practice_session~review_test~skill_editor.bundle.js  81.3 KiB                                                                      practice_session~review_test~skill_editor  [emitted]  practice_session~review_test~skill_editor
                                                                                            preferences-page.mainpage.html  5.49 KiB                                                                                                                 [emitted]  
                                                                                                     preferences.bundle.js  71.6 KiB                                                                                                    preferences  [emitted]  preferences
                                                                                             preferences~profile.bundle.js  17.4 KiB                                                                                            preferences~profile  [emitted]  preferences~profile
                                                                                                privacy-page.mainpage.html  4.23 KiB                                                                                                                 [emitted]  
                                                                                                         privacy.bundle.js  46.5 KiB                                                                                                        privacy  [emitted]  privacy
                                                                                                profile-page.mainpage.html  12.2 KiB                                                                                                                 [emitted]  
                                                                                                         profile.bundle.js  40.9 KiB                                                                                                        profile  [emitted]  profile
                                                                                    release-coordinator-page.mainpage.html  4.03 KiB                                                                                                                 [emitted]  
                                                                                             release_coordinator.bundle.js   111 KiB                                                                                            release_coordinator  [emitted]  release_coordinator
                                                                                            review-test-page.mainpage.html  5.98 KiB                                                                                                                 [emitted]  
                                                                                                     review_test.bundle.js  30.4 KiB                                                                                                    review_test  [emitted]  review_test
                                                                                                         runtime.bundle.js  6.13 KiB                                                                                                        runtime  [emitted]  runtime
                                                                                                 signup-page.mainpage.html  5.15 KiB                                                                                                                 [emitted]  
                                                                                                          signup.bundle.js  41.2 KiB                                                                                                         signup  [emitted]  signup
                                                                                           skill-editor-page.mainpage.html  7.11 KiB                                                                                                                 [emitted]  
                                                                                                    skill_editor.bundle.js   147 KiB                                                                                                   skill_editor  [emitted]  skill_editor
                                                                                       skill_editor~topic_editor.bundle.js  93.4 KiB                                                                                      skill_editor~topic_editor  [emitted]  skill_editor~topic_editor
                                                                                                 splash-page.mainpage.html  4.84 KiB                                                                                                                 [emitted]  
                                                                                                          splash.bundle.js  57.5 KiB                                                                                                         splash  [emitted]  splash
                                                                                       stewards-landing-page.mainpage.html  4.94 KiB                                                                                                                 [emitted]  
                                                                                                        stewards.bundle.js  57.8 KiB                                                                                                       stewards  [emitted]  stewards
                                                                                           story-editor-page.mainpage.html  5.73 KiB                                                                                                                 [emitted]  
                                                                                           story-viewer-page.mainpage.html  12.3 KiB                                                                                                                 [emitted]  
                                                                                                    story_editor.bundle.js   176 KiB                                                                                                   story_editor  [emitted]  story_editor
                                                                                                    story_viewer.bundle.js    58 KiB                                                                                                   story_viewer  [emitted]  story_viewer
                                                                                        subtopic-viewer-page.mainpage.html   5.5 KiB                                                                                                                 [emitted]  
                                                                                                 subtopic_viewer.bundle.js  43.5 KiB                                                                                                subtopic_viewer  [emitted]  subtopic_viewer
                                                                                                  teach-page.mainpage.html  4.34 KiB                                                                                                                 [emitted]  
                                                                                                           teach.bundle.js  67.9 KiB                                                                                                          teach  [emitted]  teach
                                                                                                  terms-page.mainpage.html  4.33 KiB                                                                                                                 [emitted]  
                                                                                                           terms.bundle.js  40.8 KiB                                                                                                          terms  [emitted]  terms
                                                                                                 thanks-page.mainpage.html   4.1 KiB                                                                                                                 [emitted]  
                                                                                                          thanks.bundle.js  29.8 KiB                                                                                                         thanks  [emitted]  thanks
                                                                                           topic-editor-page.mainpage.html  6.97 KiB                                                                                                                 [emitted]  
                                                                                          topic-landing-page.mainpage.html  4.22 KiB                                                                                                                 [emitted]  
                                                                                           topic-viewer-page.mainpage.html  5.43 KiB                                                                                                                 [emitted]  
                                                                                                    topic_editor.bundle.js   204 KiB                                                                                                   topic_editor  [emitted]  topic_editor
                                                                                       topic_editor~topic_viewer.bundle.js  36.8 KiB                                                                                      topic_editor~topic_viewer  [emitted]  topic_editor~topic_viewer
                                                                                                    topic_viewer.bundle.js  39.6 KiB                                                                                                   topic_viewer  [emitted]  topic_viewer
                                                                            topics-and-skills-dashboard-page.mainpage.html  5.57 KiB                                                                                                                 [emitted]  
                                                                                     topics_and_skills_dashboard.bundle.js   206 KiB                                                                                    topics_and_skills_dashboard  [emitted]  topics_and_skills_dashboard
   vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js  15.5 MiB  vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248  [emitted]  vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248
   vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js  22.9 KiB  vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5  [emitted]  vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5
   vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js   206 KiB  vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466  [emitted]  vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466
   vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js  35.4 KiB  vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867  [emitted]  vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867
                                      vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js  1.41 MiB                                     vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor  [emitted]  vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor
                                                                                     vendors~preferences~profile.bundle.js   121 KiB                                                                                    vendors~preferences~profile  [emitted]  vendors~preferences~profile
                                                                                     vendors~release_coordinator.bundle.js   317 KiB                                                                                    vendors~release_coordinator  [emitted]  vendors~release_coordinator
   Entrypoint about = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js about.bundle.js
   Entrypoint admin = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js admin~blog_admin.bundle.js admin.bundle.js
   Entrypoint blog_admin = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js admin~blog_admin.bundle.js blog_admin.bundle.js
   Entrypoint classroom = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js classroom.bundle.js
   Entrypoint collection_editor = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor~topics_and_skil~68685f5f.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js collection_editor.bundle.js
   Entrypoint collection_player = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js collection_player.bundle.js
   Entrypoint contact = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js contact.bundle.js
   Entrypoint console_errors = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js console_errors.bundle.js
   Entrypoint creator_dashboard = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js creator_dashboard.bundle.js
   Entrypoint contributor_dashboard = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor~topics_and_skil~68685f5f.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js contributor_dashboard~skill_editor~topic_editor.bundle.js contributor_dashboard.bundle.js
   Entrypoint contributor_dashboard_admin = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js contributor_dashboard_admin.bundle.js
   Entrypoint delete_account = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js delete_account.bundle.js
   Entrypoint donate = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js donate.bundle.js
   Entrypoint email_dashboard = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js email_dashboard.bundle.js
   Entrypoint email_dashboard_result = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js email_dashboard_result.bundle.js
   Entrypoint error = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js error.bundle.js
   Entrypoint exploration_editor = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor~topics_and_skil~68685f5f.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js exploration_editor~exploration_player.bundle.js exploration_editor.bundle.js
   Entrypoint exploration_player = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js exploration_player~practice_session~review_test~skill_editor.bundle.js exploration_editor~exploration_player.bundle.js exploration_player.bundle.js
   Entrypoint get_started = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js get_started.bundle.js
   Entrypoint landing = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js landing.bundle.js
   Entrypoint learner_dashboard = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js learner_dashboard.bundle.js
   Entrypoint library = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js library.bundle.js
   Entrypoint license = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js license.bundle.js
   Entrypoint login = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js login.bundle.js
   Entrypoint logout = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js logout.bundle.js
   Entrypoint maintenance = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js maintenance.bundle.js
   Entrypoint moderator = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js moderator.bundle.js
   Entrypoint partnerships = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js partnerships.bundle.js
   Entrypoint pending_account_deletion = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js pending_account_deletion.bundle.js
   Entrypoint playbook = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js playbook.bundle.js
   Entrypoint practice_session = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js exploration_player~practice_session~review_test~skill_editor.bundle.js practice_session~review_test~skill_editor.bundle.js practice_session.bundle.js
   Entrypoint privacy = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js privacy.bundle.js
   Entrypoint preferences = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~preferences~profile.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js preferences~profile.bundle.js preferences.bundle.js
   Entrypoint profile = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~preferences~profile.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js preferences~profile.bundle.js profile.bundle.js
   Entrypoint release_coordinator = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js vendors~release_coordinator.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js release_coordinator.bundle.js
   Entrypoint review_test = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js exploration_player~practice_session~review_test~skill_editor.bundle.js practice_session~review_test~skill_editor.bundle.js review_test.bundle.js
   Entrypoint signup = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js signup.bundle.js
   Entrypoint skill_editor = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor~topics_and_skil~68685f5f.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js exploration_player~practice_session~review_test~skill_editor.bundle.js practice_session~review_test~skill_editor.bundle.js contributor_dashboard~skill_editor~topic_editor.bundle.js skill_editor~topic_editor.bundle.js skill_editor.bundle.js
   Entrypoint splash = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js splash.bundle.js
   Entrypoint stewards = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js stewards.bundle.js
   Entrypoint story_editor = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js story_editor.bundle.js
   Entrypoint story_viewer = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js story_viewer.bundle.js
   Entrypoint subtopic_viewer = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js subtopic_viewer.bundle.js
   Entrypoint teach = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js teach.bundle.js
   Entrypoint terms = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js terms.bundle.js
   Entrypoint thanks = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js thanks.bundle.js
   Entrypoint topic_editor = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js vendors~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~practice_session~revie~418ffd33.bundle.js contributor_dashboard~exploration_editor~exploration_player~practice_session~review_test~skill_edito~375d2c53.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~exploration_player~skill_editor~topic_editor.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor~topics_and_skil~68685f5f.bundle.js contributor_dashboard~creator_dashboard~exploration_editor~skill_editor~story_editor~topic_editor.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js contributor_dashboard~exploration_editor~skill_editor~topic_editor.bundle.js contributor_dashboard~skill_editor~topic_editor.bundle.js skill_editor~topic_editor.bundle.js topic_editor~topic_viewer.bundle.js topic_editor.bundle.js
   Entrypoint topics_and_skills_dashboard = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js collection_editor~contributor_dashboard~exploration_editor~skill_editor~topic_editor~topics_and_skil~68685f5f.bundle.js topics_and_skills_dashboard.bundle.js
   Entrypoint topic_viewer = runtime.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~01b80248.bundle.js vendors~about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~~f5d6d3c5.bundle.js vendors~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_da~c3532466.bundle.js vendors~admin~blog_admin~collection_editor~collection_player~contributor_dashboard~contributor_dashb~a5f68867.bundle.js about~admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contact~contribu~ddc80bff.bundle.js admin~blog_admin~classroom~collection_editor~collection_player~console_errors~contributor_dashboard~~b44401a2.bundle.js topic_editor~topic_viewer.bundle.js topic_viewer.bundle.js
   [./core/templates/pages/about-page/about-page.import.ts] 1.42 KiB {about} [built]
   [./core/templates/pages/admin-page/admin-page.import.ts] 1.23 KiB {admin} [built]
   [./core/templates/pages/blog-admin-page/blog-admin-page.import.ts] 1.24 KiB {blog_admin} [built]
   [./core/templates/pages/classroom-page/classroom-page.import.ts] 1.25 KiB {classroom} [built]
   [./core/templates/pages/collection-editor-page/collection-editor-page.import.ts] 1.58 KiB {collection_editor} [built]
   [./core/templates/pages/collection-player-page/collection-player-page.import.ts] 1.68 KiB {collection_player} [built]
   [./core/templates/pages/contact-page/contact-page.import.ts] 1.43 KiB {contact} [built]
   [./core/templates/pages/contributor-dashboard-admin-page/contributor-dashboard-admin-page.import.ts] 1.41 KiB {contributor_dashboard_admin} [built]
   [./core/templates/pages/contributor-dashboard-page/contributor-dashboard-page.import.ts] 1.34 KiB {contributor_dashboard} [built]
   [./core/templates/pages/creator-dashboard-page/creator-dashboard-page.import.ts] 1.39 KiB {creator_dashboard} [built]
   [./core/templates/pages/delete-account-page/delete-account-page.import.ts] 1.45 KiB {delete_account} [built]
   [./core/templates/pages/donate-page/donate-page.import.ts] 1.42 KiB {donate} [built]
   [./core/templates/pages/email-dashboard-pages/email-dashboard-page.import.ts] 1.23 KiB {email_dashboard} [built]
   [./core/templates/pages/email-dashboard-pages/email-dashboard-result.import.ts] 1.24 KiB {email_dashboard_result} [built]
   [./core/templates/pages/error-pages/error-page.import.ts] 1.17 KiB {error} [built]
       + 3828 hidden modules
   
   WARNING in ./core/templates/components/skill-selector/skill-selector.component.ts 200:50-67
   "export 'CategorizedSkills' was not found in 'domain/topics_and_skills_dashboard/topics-and-skills-dashboard-backend-api.service'
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./core/templates/components/skill-selector/skill-selector.component.ts 200:87-104
   "export 'CategorizedSkills' was not found in 'domain/topics_and_skills_dashboard/topics-and-skills-dashboard-backend-api.service'
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./core/templates/components/summary-tile/exploration-summary-tile.component.ts 179:50-68
   "export 'ExplorationRatings' was not found in 'domain/summary/learner-exploration-summary.model'
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./core/templates/components/summary-tile/exploration-summary-tile.component.ts 179:88-106
   "export 'ExplorationRatings' was not found in 'domain/summary/learner-exploration-summary.model'
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./extensions/objects/templates/graph-editor.component.ts 49:50-61
   "export 'GraphAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/objects/object-components.module.ts
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./extensions/objects/templates/graph-editor.component.ts 49:81-92
   "export 'GraphAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/objects/object-components.module.ts
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./extensions/interactions/GraphInput/directives/oppia-interactive-graph-input.component.ts 170:50-61
   "export 'GraphAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/GraphInput/graph-input-interactions.module.ts
    @ ./extensions/objects/object-components.module.ts
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./extensions/interactions/GraphInput/directives/oppia-interactive-graph-input.component.ts 170:81-92
   "export 'GraphAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/GraphInput/graph-input-interactions.module.ts
    @ ./extensions/objects/object-components.module.ts
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./extensions/interactions/GraphInput/directives/graph-viz.component.ts 580:50-61
   "export 'GraphAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/GraphInput/graph-input-interactions.module.ts
    @ ./extensions/objects/object-components.module.ts
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./extensions/interactions/GraphInput/directives/graph-viz.component.ts 580:81-92
   "export 'GraphAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/GraphInput/graph-input-interactions.module.ts
    @ ./extensions/objects/object-components.module.ts
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./core/templates/components/skill-selector/skill-selector.component.ts 188:50-71
   "export 'GroupedSkillSummaries' was not found in 'pages/skill-editor-page/services/skill-editor-state.service'
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./core/templates/components/skill-selector/skill-selector.component.ts 188:91-112
   "export 'GroupedSkillSummaries' was not found in 'pages/skill-editor-page/services/skill-editor-state.service'
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
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
   
   WARNING in ./core/templates/pages/exploration-player-page/learner-experience/input-response-pair.component.ts 101:50-67
   "export 'InputResponsePair' was not found in 'domain/state_card/state-card.model'
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./core/templates/pages/exploration-player-page/learner-experience/input-response-pair.component.ts 101:87-104
   "export 'InputResponsePair' was not found in 'domain/state_card/state-card.model'
    @ ./core/templates/components/shared-component.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.module.ts
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./extensions/interactions/NumericExpressionInput/directives/oppia-interactive-numeric-expression-input.component.ts 134:50-67
   "export 'InteractionAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/NumericExpressionInput/numeric-expression-input-interactions.module.ts
    @ ./extensions/interactions/interactions.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts
   
   WARNING in ./extensions/interactions/NumericExpressionInput/directives/oppia-interactive-numeric-expression-input.component.ts 134:87-104
   "export 'InteractionAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/NumericExpressionInput/numeric-expression-input-interactions.module.ts
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
   
   WARNING in ./extensions/interactions/FractionInput/directives/oppia-interactive-fraction-input.component.ts 199:50-67
   "export 'InteractionAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/FractionInput/fraction-input-interactions.module.ts
    @ ./extensions/interactions/interactions.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts
   
   WARNING in ./extensions/interactions/FractionInput/directives/oppia-interactive-fraction-input.component.ts 199:87-104
   "export 'InteractionAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/FractionInput/fraction-input-interactions.module.ts
    @ ./extensions/interactions/interactions.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts
   
   WARNING in ./extensions/interactions/MathEquationInput/directives/oppia-interactive-math-equation-input.component.ts 102:50-67
   "export 'InteractionAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/MathEquationInput/math-equation-input-interactions.module.ts
    @ ./extensions/interactions/interactions.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.module.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts
   
   WARNING in ./extensions/interactions/MathEquationInput/directives/oppia-interactive-math-equation-input.component.ts 102:87-104
   "export 'InteractionAnswer' was not found in 'interactions/answer-defs'
    @ ./extensions/interactions/MathEquationInput/math-equation-input-interactions.module.ts
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
    @ ./core/templates/pages/exploration-editor-page/editor-tab/exploration-editor-tab.component.ts
    @ ./core/templates/components/state-editor/state-editor.component.ts
    @ ./core/templates/components/question-directives/question-editor/question-editor.directive.ts
    @ ./core/templates/components/question-directives/questions-list/questions-list.component.ts
    @ ./core/templates/pages/topic-editor-page/questions-tab/topic-questions-tab.component.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.component.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts
   
   WARNING in ./node_modules/d3-scale/src/time.js 70:34-43
   "export 'timeTicks' was not found in 'd3-time'
    @ ./node_modules/d3-scale/src/index.js
    @ ./extensions/visualizations/oppia-visualization-click-hexbins.directive.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/templates/state-stats-modal.controller.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/statistics-tab.component.ts
    @ ./core/templates/pages/exploration-editor-page/exploration-editor-page.component.ts
    @ ./core/templates/pages/exploration-editor-page/editor-tab/exploration-editor-tab.component.ts
    @ ./core/templates/components/state-editor/state-editor.component.ts
    @ ./core/templates/components/question-directives/question-editor/question-editor.directive.ts
    @ ./core/templates/components/question-directives/questions-list/questions-list.component.ts
    @ ./core/templates/pages/topic-editor-page/questions-tab/topic-questions-tab.component.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.component.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts
   
   WARNING in ./node_modules/d3-scale/src/utcTime.js 7:44-59
   "export 'utcTickInterval' was not found in 'd3-time'
    @ ./node_modules/d3-scale/src/index.js
    @ ./extensions/visualizations/oppia-visualization-click-hexbins.directive.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/templates/state-stats-modal.controller.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/statistics-tab.component.ts
    @ ./core/templates/pages/exploration-editor-page/exploration-editor-page.component.ts
    @ ./core/templates/pages/exploration-editor-page/editor-tab/exploration-editor-tab.component.ts
    @ ./core/templates/components/state-editor/state-editor.component.ts
    @ ./core/templates/components/question-directives/question-editor/question-editor.directive.ts
    @ ./core/templates/components/question-directives/questions-list/questions-list.component.ts
    @ ./core/templates/pages/topic-editor-page/questions-tab/topic-questions-tab.component.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.component.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts
   
   WARNING in ./node_modules/d3-scale/src/utcTime.js 7:34-42
   "export 'utcTicks' was not found in 'd3-time'
    @ ./node_modules/d3-scale/src/index.js
    @ ./extensions/visualizations/oppia-visualization-click-hexbins.directive.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/templates/state-stats-modal.controller.ts
    @ ./core/templates/pages/exploration-editor-page/statistics-tab/statistics-tab.component.ts
    @ ./core/templates/pages/exploration-editor-page/exploration-editor-page.component.ts
    @ ./core/templates/pages/exploration-editor-page/editor-tab/exploration-editor-tab.component.ts
    @ ./core/templates/components/state-editor/state-editor.component.ts
    @ ./core/templates/components/question-directives/question-editor/question-editor.directive.ts
    @ ./core/templates/components/question-directives/questions-list/questions-list.component.ts
    @ ./core/templates/pages/topic-editor-page/questions-tab/topic-questions-tab.component.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.component.ts
    @ ./core/templates/pages/topic-editor-page/topic-editor-page.import.ts
   
   WARNING in ./node_modules/@angular/core/fesm2015/core.js 29739:15-36
   Critical dependency: the request of a dependency is an expression
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./node_modules/@angular/core/fesm2015/core.js 29751:15-102
   Critical dependency: the request of a dependency is an expression
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts
   
   WARNING in ./node_modules/@angular/core/fesm2015/core.js 29739:15-36
   System.import() is deprecated and will be removed soon. Use import() instead.
   For more info visit https://webpack.js.org/guides/code-splitting/
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts 25:0-47 27:4-18
   
   WARNING in ./node_modules/@angular/core/fesm2015/core.js 29751:15-102
   System.import() is deprecated and will be removed soon. Use import() instead.
   For more info visit https://webpack.js.org/guides/code-splitting/
    @ ./core/templates/pages/landing-pages/topic-landing-page/topic-landing-page.import.ts 25:0-47 27:4-18
   Child HtmlWebpackCompiler:
        50 assets
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
       Entrypoint HtmlWebpackPlugin_46 = __child-HtmlWebpackPlugin_46
       Entrypoint HtmlWebpackPlugin_47 = __child-HtmlWebpackPlugin_47
       Entrypoint HtmlWebpackPlugin_48 = __child-HtmlWebpackPlugin_48
       Entrypoint HtmlWebpackPlugin_49 = __child-HtmlWebpackPlugin_49
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/about-page/about-page.mainpage.html] 788 bytes {HtmlWebpackPlugin_0} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/admin-page/admin-page.mainpage.html] 905 bytes {HtmlWebpackPlugin_1} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/blog-admin-page/blog-admin-page.mainpage.html] 884 bytes {HtmlWebpackPlugin_2} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/classroom-page/classroom-page.mainpage.html] 1.39 KiB {HtmlWebpackPlugin_3} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/collection-editor-page/collection-editor-page.mainpage.html] 1.31 KiB {HtmlWebpackPlugin_4} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/collection-player-page/collection-player-page.mainpage.html] 3.46 KiB {HtmlWebpackPlugin_5} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/contact-page/contact-page.mainpage.html] 798 bytes {HtmlWebpackPlugin_7} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/contributor-dashboard-admin-page/contributor-dashboard-admin-page.mainpage.html] 868 bytes {HtmlWebpackPlugin_9} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/contributor-dashboard-page/contributor-dashboard-page.mainpage.html] 1.24 KiB {HtmlWebpackPlugin_10} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/creator-dashboard-page/creator-dashboard-page.mainpage.html] 1.44 KiB {HtmlWebpackPlugin_8} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/delete-account-page/delete-account-page.mainpage.html] 696 bytes {HtmlWebpackPlugin_11} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/donate-page/donate-page.mainpage.html] 795 bytes {HtmlWebpackPlugin_12} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/email-dashboard-pages/email-dashboard-page.mainpage.html] 1.45 KiB {HtmlWebpackPlugin_13} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/email-dashboard-pages/email-dashboard-result.mainpage.html] 1.34 KiB {HtmlWebpackPlugin_14} [built]
       [./node_modules/html-webpack-plugin/lib/loader.js!./core/templates/pages/error-pages/error-iframed.mainpage.html] 2.49 KiB {HtmlWebpackPlugin_15} [built]
           + 44 hidden modules
   INFO     2021-07-19 00:24:08,029 devappserver2.py:289] Skipping SDK update check.
   WARNING  2021-07-19 00:24:09,020 simple_search_stub.py:1198] Could not read search indexes from /tmp/appengine.None.naomi/search_indexes
   INFO     2021-07-19 00:24:09,023 api_server.py:282] Starting API server at: http://localhost:37691
   INFORMATION
   
   Local development server is ready! Opening a default web browser window pointing to it: http://localhost:8181/
   
   Starting new Web Browser: xdg-open http://localhost:8181/
   ```
   </details>


   The first time you run this script, it will take a while -- about 5 - 10 minutes when we last tested it in Sep 2020, though this depends on your Internet connection. (It might also hang after "Checking if pip is installed on the local machine" due to the grpcio build being slow -- just give it some time, and it should finish.) Subsequent runs should be much faster. The `start.py` script downloads and installs the required dependencies (such as Google App Engine) if they are not already present, and sets up a development server for you to play with. The development server logs are then output to this terminal, so you will not be able to enter further commands in it until you disconnect the server.

   **Note**: **Please don't use `sudo` while installing.** It's not required, and using it may cause problems later. If you face permissions issues, ensure that you have the necessary permissions for the directory in which you're trying to set up Oppia. If you run into any other installation problems, please read [[these notes|Issues-with-installation?]].

   **Note**: The script will create some files and folders that are siblings of the `oppia/` root directory, for example `oppia_tools`. This is done so that these two folders will not be uploaded to App Engine when the application is deployed to the web.
   
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

   ```console
   sudo chown -R {{YOUR_USERNAME}} ~/tmp
   sudo chown -R {{YOUR_USERNAME}} ~/.npm
   ```

   where `{{YOUR_USERNAME}}` should be replaced by your username.

2. The `start.py` script will start a development server at http://localhost:8181. It should look something like this:

  ![Image showing the default splash page.](https://res.cloudinary.com/dozmja9ir/image/upload/v1538254601/home_page.png)

  You can also view the App Engine admin console at http://localhost:8000.

  **Note:** There may be a few warnings that appear after running `start.py`. Don’t worry about these so long as you see the page above once you go to http://localhost:8181. The script should continue to run so long as the development server is on (you’ll see a lot of lines that start with “INFO”) and you’re able to navigate to the page. 

3. When you're done, you can shut down the development server by typing Ctrl+C into the terminal. **Then wait for a command prompt to appear.** Oppia has to shut down all the services it's started, and if you abort the graceful shutdown steps (e.g. by typing Ctrl+C many times), you may have trouble re-starting the server.

   <details>
   <summary>Example shutdown output</summary>
   ```text
   ^CINFO     2021-07-19 00:31:32,627 shutdown.py:50] Shutting down.
   INFO     2021-07-19 00:31:32,627 stub_util.py:377] Applying all pending transactions and saving the datastore
   INFO     2021-07-19 00:31:32,628 stub_util.py:380] Saving search indexes
    
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
   Stopping Web Browser(name="xdg-open", pid=14416)...
   Stopping GAE Development Server(name="sh", pid=14405)...
   Stopping Webpack Compiler(name="sh", pid=14338)...
   Stopping Firebase Emulator(name="sh", pid=14311)...
   Stopping ElasticSearch Server(name="sh", pid=14060)...
   Stopping Redis Server(name="sh", pid=14045)...
   
   
   Done! Thank you for waiting.
   
   
   Traceback (most recent call last):
     File "/home/user/.pyenv/versions/2.7.18/lib/python2.7/runpy.py", line 174, in _run_module_as_main
       "__main__", fname, loader, pkg_name)
     File "/home/user/.pyenv/versions/2.7.18/lib/python2.7/runpy.py", line 72, in _run_code
       exec code in run_globals
     File "/opensource/oppia/scripts/start.py", line 202, in <module>
       main()
     File "/opensource/oppia/scripts/start.py", line 198, in main
       dev_appserver.wait()
     File "/opensource/oppia/../oppia_tools/psutil-5.7.3/psutil/__init__.py", line 1350, in wait
       ret = super(Popen, self).wait(timeout)
     File "/opensource/oppia/../oppia_tools/psutil-5.7.3/psutil/__init__.py", line 1259, in wait
       self._exitcode = self._proc.wait(timeout)
     File "/opensource/oppia/../oppia_tools/psutil-5.7.3/psutil/_pslinux.py", line 1517, in wrapper
       return fun(self, *args, **kwargs)
     File "/opensource/oppia/../oppia_tools/psutil-5.7.3/psutil/_pslinux.py", line 1725, in wait
       return _psposix.wait_pid(self.pid, timeout, self._name)
     File "/opensource/oppia/../oppia_tools/psutil-5.7.3/psutil/_psposix.py", line 115, in wait_pid
       retpid, status = os.waitpid(pid, flags)
   KeyboardInterrupt
   ```
   </details>

## Tips and tricks

* To preserve the contents of the local datastore between consecutive runs, use the `--save_datastore` argument when starting up the dev server:

  ```console
  python -m scripts.start --save_datastore
  ```

* The default Oppia installation comes with a set of [demo explorations](https://github.com/oppia/oppia/tree/master/data/explorations). On startup, none of these are loaded. To load them, log in to your server as an admin, then click your username in the top-right corner and choose 'Admin Page'. This will open the admin page, from which you can load the demo explorations.

## Notes on installation on Arch Linux systems

_The following notes are thanks to Prasanna Patil (@prasanna08). They come with no guarantees, and may change some settings on your local machine, so please make sure you fully understand their ramifications before following them!_

### Installation prerequisites

Arch uses pacman as package manager, so the install_prerequisites.sh script is not going to work and all of the prerequisites have to be installed manually using pacman. Just type the following command in the shell (notation: # denotes sudo access while $ denotes normal user access):

```
   # pacman -Sy python2 python2-pip python2-setuptools curl jre7-openjdk unzip git python2-yaml
```

Also, note that pacman doesn't support google chrome in the default package manager (which is needed to run frontend and e2e tests). However, you can use the chromium package instead; this is an open-source fork of google chrome. Here's how to do it -- install the chromium browser, and then create a soft link from the google-chrome command to chromium:

```
   # pacman -Sy chromium
   # cd /usr/bin
   # ln -sf chromium google-chrome
```

If you do want to use google chrome instead, you could also use the third-party repository AUR (with the help of yaourt).

### Install 3rd party libraries

Arch uses the pip command for pip 3 (which installs libraries for python 3) and pip2 command for python 2, so we have to install all necessary (python’s) 3rd party libraries manually. For this go to the ‘oppia_tools’ directory and open a terminal and type following commands (note: make sure that you are in oppia_tools folder).

```
  $ pip2 install pylint==1.7.1 --target="./pylint-1.7.1"
  $ pip2 install numpy==1.6.1 --target="./numpy-1.6.1"
  $ pip2 install browsermob-proxy==0.7.1 --target="./browsermob-proxy-0.7.1"
  $ pip2 install selenium==2.53.2 --target="./selenium-2.53.2"
  $ curl -o webtest-download.zip -L https://github.com/Pylons/webtest/archive/1.4.2.zip
  $ unzip webtest-download.zip -d .
  $ rm webtest-download.zip
  $ touch ./pylint-1.7.1/backports/__init__.py
```

Once this step is done, run `python -m scripts.start` to install other necessary files such as node modules and static js libraries and google app engine. Even after downloading everything server will fail to start and show errors. If you don’t see any errors then you have successfully setup Oppia in Arch and don’t have to execute following steps but it is highly likely that server won’t work.

### Fixing Python

In Arch, the `python` command refers to python 3 (in contrast to Ubuntu, where `python` refers to python 2). This has to be fixed. There are two ways to do so. One is to modify the python files and other is to modify system links.
1. Modify python (.py) files: two files have to be modified slightly here. First is dev_appserver.py file of the google app engine. Go to ‘oppia_tools/google_appengine_1.9.50/google_appengine’ and open ‘dev_appserver.py’ file. On the first line replace ‘python’ with ‘python2’. Secondly go to the ‘oppia/.git/hooks/prepush.py’ file and open it. On the very first line replace ‘python’ with ‘python2’.
2. Modify system links: go to the /usr/bin and type following command.
```
	# ln -sf python2 python
```

### Fix Google App Engine

Note: make sure you have already executed ‘python -m scripts.start’ before doing this step and all the necessary files were downloaded by the script. Basically at this point your Oppia server should start showing logs (error logs) in the terminal but you won’t be able to access Oppia in browser.

One of the highlights of Arch is that it is always up to date from linux to all packages. That is also the case with python2. Arch uses latest version of the python 2 which is 2.7.14. This version is incompatible with Google App Engine v1.9.50, currently used by Oppia. To fix this go to ‘oppia_tools/google_appengine_1.9.50/google_appengine/google/appengine/dist27’ and open ‘socket.py’ file. In this file go to the line 73 (or, alternatively, search for ‘RAND_egd’) and remove import of ‘RAND_egd’ from that line.

   
