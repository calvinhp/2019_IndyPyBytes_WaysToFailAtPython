# Half a Dozen Ways to Fail at Python 

# Intro: Where you don’t want to end

![](https://imgs.xkcd.com/comics/python_environment.png)

    - https://xkcd.com/1987/

# Fail 1: ‘Python not found’

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558972953603_image.png)

  - Installing Python on Windows/OS X/Linux

# Fail 2: ‘ImportError: No module named requests’

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558973132749_image.png)

  - How do I get 3rd party tools installed
  - Using/installing pip if you can’t find it
      - included with python as of 2.7 and 3.something but may not be obvious


# Fail 3: My two projects need different versions

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558971804604_image.png)

  - Proj A requires v 1.2 of dependent package and Proj B needs version 2.5…
  - virtualenv — sandboxing your Python for specific projects
    - Needs to be installed, maybe with `pip`, but could also be used standalone
    - What if you don’t install it globally?
    - using `pip` safely in the sandbox
    - virtualenvwrapper — bonus material

# Fail 4: It works for me but not my team-mate

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558971763326_image.png)

  - My Co-worker cloned the repo and can’t get the project started due to version issues
  - pipenv — repeatable sandboxes and installing packages
    - Alternatives to pipenv, because it may not fit your workflow
      - Poetry
      - Hatch

# Fail 5: My old Python project won’t run

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558971706396_image.png)

  - I’ve been told to work on a legacy project that requires Python 2.6 and I only have newer python installed
  - pyenv — using different versions of python for your projects

# Fail 6: Halp, I’m on Windows!

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558971681645_image.png)

  - Halp, I’m on Windows and don’t have a C compiler and want to use NumPy!
  - What about anaconda?

# Take Aways

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558972909570_image.png)

- Top recommendations:
  - Never use sudo or admin mode
  - Always use a Sandbox
  - Always track your requirements and their versions


