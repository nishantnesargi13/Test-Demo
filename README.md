#complete explanations
name: my first git hub actions
#on : push   = triggers this file/github actions for every commit
on: [push]

#jobs =pipeline job ,if 3 jobs means 3 jenkin pipeline
jobs:
 build:
 
 #runs-on =ubuntu os   set up python env/image
 
  runs-on: ubuntu-latest

  strategy:
   matrix:
   #app to run on these 2 version seperately
     python-version: [3.10]

#satges start
  steps:
  # actions/checkout@v4 =it's a plugin
  - uses: actions/checkout@v4
  - name: set up python
  #actions/setup-python@v2 ==it's a plugin
  - uses: actions/setup-python@v2 
    with:
        python-version: ${{ matrix.python-version }}
        
  - name: Install dependencies
    run: |
        python -m pip install --upgrade pip
        pip install pytest

  - name: Run tests
    run: |
        cd src
        python -m pytest addition.py
