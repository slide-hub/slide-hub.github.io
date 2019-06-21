### Prerequisites

* On your computer
	* Python 3.6 or 3.7 [(HowTo?)](https://www.anaconda.com/distribution/)
	* `pip` installed   [(HowTo?)](https://pip.pypa.io/en/stable/installing/)

--

### Prerequisites

* Provided infrastructure
	* `ssh` client
	* ... or a webbrowser

installed on your computer

---

### Virtual Environment

* Install `virtualenv` if not available
```bash
$ python3 -m pip install virtualenv
```

* Create a new virtual environment
```bash
$ python3 -m virtualenv tardis_tutorial
```
* Activate your virtual environment
```bash
$ source tardis_tutorial/bin/activate
```

> We recommend to run `TARDIS` in a Python virtual environment

--

### Installation

* Install `COBalD/TARDIS` from PyPi
```bash
$ python3 -m pip install cobald-tardis
```

* Change into `tardis` directory
```bash
$ cd tardis
```

> All dependencies are automatically installed as well
