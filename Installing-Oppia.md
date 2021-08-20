__If you are looking for more elaborate instructions on how to get started with Oppia, go to [setting things up](https://github.com/oppia/oppia/wiki/Contributing-code-to-Oppia#setting-things-up).__

Following is the list of installation instructions for various platforms:
1. Create a new, empty folder called `opensource/`. If you're transferring to Python 3 version and still want to keep the older Python 2 version of Oppia please create some other folder with a different name.
2. Follow the instructions for your platform:
   * [Linux](https://github.com/oppia/oppia/wiki/Installing-Oppia-(Linux;-Python-3))
   * [Mac OS](https://github.com/oppia/oppia/wiki/Installing-Oppia-(Mac-OS;-Python-3))
   * [Windows](https://github.com/oppia/oppia/wiki/Installing-Oppia-(Windows;-Python-3))
3. You might need to install an older version of Oppia that uses Python 2 (only do this when you need to get some older code working or you need to make some changes to a release that is not in Python 3 yet), follow these instructions for your platform:
   * [Linux](https://github.com/oppia/oppia/wiki/Installing-Oppia-%28Linux%29)
   * [Mac OS](https://github.com/oppia/oppia/wiki/Installing-Oppia-%28Mac-OS%29)
   * [Windows](https://github.com/oppia/oppia/wiki/Installing-Oppia-%28Windows%29) (might be a bit complicated, we recommend to use Linux or Mac if you can)
4. If you run into any problems during installation, please read [these notes](https://github.com/oppia/oppia/wiki/Issues-with-installation%3F) and the [troubleshooting](https://github.com/oppia/oppia/wiki/Troubleshooting) page.
5. Take a look at our [[guide for getting started with some common code editors|Tips-for-common-IDEs]].

   **Warning:** You should always edit Oppia code on your local machine. Do not use web-based editors like github.dev or the editor on github.com. These web-based editors won't run the automated checks that run on your loacl machine. Pushing without these checks just means that the tests will fail on your PR.
