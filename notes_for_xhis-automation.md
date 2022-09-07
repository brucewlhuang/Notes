## Repo
* https://github.com/ASUS-AICS/xhis-automation
## Env set up
* Windows common
    * Azure cli: Check permission to access (az login / az logout)
    * Runtime: **python3.8.10+**
    * Chromedriver: Please find your chrome version in your environment and
    download the correspond chromedriver version.
    Finally, put it to the corresponding path. (default: under repo dir)
        * How to find your chrome version: chrome://settings/help
        * Download chromedriver: https://chromedriver.chromium.org/downloads
    * Packages: Install requirements
        ```
        python -m pip install -r requirements.txt
        ```
* Windows + powershell / cmd / bash
    * Like windows common metioned

* Windows + wsl2 + zsh
    * Besides windows common metioned, you need to do another setting
    * Install linux chrome
        ```
        wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
        sudo apt install ./google-chrome-stable_current_amd64.deb
        ```
    * Check it worked
        ```
        google-chrome --version
        ```
    * Install linux chromedriver
        ```
        wget https://chromedriver.storage.googleapis.com/86.0.4240.22/chromedriver_linux64.zip
        unzip chromedriver_linux64.zip
        sudo mv chromedriver /usr/bin/chromedriver
        sudo chown root:root /usr/bin/chromedriver
        sudo chmod +x /usr/bin/chromedriver
        ```
    * Check it worked
        ```
        chromedriver --version
        which chromedriver # should be /usr/bin/chromedriver
        ```
    * Download X Server
        * Run xlaunch.exe (from the VcXsrv folder in Program Files). You can leave most of the settings as default, but make sure to check **disable access control**
        * Download X Server: https://sourceforge.net/projects/vcxsrv/
    * Add display environment variable
        ```
        export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2; exit;}'):0.0
        ```
    * ref : https://www.gregbrisebois.com/posts/chromedriver-in-wsl2/

## How to test
* prepare files under the **spec** folder
* refer to **config.json** under the **script_assistant** folder (setting like pytest)
* produce **site files** under the **automation_test/test_case**
    ```
    python -m script_assistant.run
    ```
* **runner_config.json** path: **automation_test/runner/config/** (setting like pytest)
    * step_sleep_time
    * include_test_target: you can change your test target. e.q.
    ```
    "automation_test/test_case/cc/azure_dev/soap_spell_check/e2e_show_spell_check.side"
    ```
* **his_agent.json** path: **automation_test/his_agent/config/**
    * headless: if it setting to false, the chromedriver will display the whole test prograss. 
    * chrome_driver_executable_path
        * common windows: **/chromedriver.exe**
        * wsl2: **/usr/bin/chromedriver**

* run test:
    ```
    python script_runner.py 
    ```
