# Tutorial
- [CRUD with python, flask, and react](https://developer.okta.com/blog/2018/12/20/crud-app-with-python-flask-react)

# Environment Setup
  - Check Python version
    - terminal: python --version
      => zsh: command not found: python
    - Mac no longer has Python
    - Going to need to manually install
  - Using Brew to install Pyenv
    - terminal: brew doctor
      => lots of output, but the main piece is that Command Line Tools are outdated
  - Command Line Tools needed updates
    - terminal: sudo rm -rf /Library/Developer/CommandLineTools
    - terminal: sudo xcode-select --install
    - Takes forever
  - Brew needed updates
    - terminal: brew update
  - Using Brew to install PART 2
    - terminal: brew install pyenv
      - Takes forever
    - terminal: pyenv install 3.6.3
      => BUILD FAILED (OS X 12.5.1 using python-build 20180424)
      - terminal: brew upgrade
      - terminal: brew reinstall pyenv
      - terminal: pyenv install 3.6.3
        => Still failed
      - terminal: sudo rm -rf /Library/Developer/CommandLineTools
      - terminal: sudo xcode-select --install
      - terminal: pyenv install 3.6.3
        => Still failed
        - Research: https://github.com/pyenv/pyenv/issues/2143
        - Helped me figure out I need a different version with my Mac OS version...
      - terminal: pyenv install 3.11.1
    - ~~terminal: pyenv global 3.6.3~~
    - terminal: pyenv global 3.11.1
  - Restart terminal
    - Still didn't work
    - Tried brew install python3
    - Finally worked
    - terminal: python3 --version
      => Python 3.10.9
    - BUT... this means python didn't install with pyenv
      - Hmmm.. funky
    - LIESSSSSSSS!!! It was a zsh issue
    - Update ~/.zshrc file
      - terminal: echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
      - terminal: echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
      - You might have to open zshrc and split these into two lines
      - terminal: echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init --path)"\n  eval "$(pyenv init -)"\nfi' >> ~/.zshrc
      - Restart terminal
      - Success!
      - terminal: python --version
        => Python 3.11.1
  - Install Pipenv
    - terminal: brew install pipenv
    - terminal: pipenv --version
    - => pipenv, version 2023.2.4
  - Setup project
    - terminal: cd Documents/Learning
    - terminal: mkdir Python && cd Python
    - terminal: mkdir kudos_oss && cd kudos_oss
    - terminal: pipenv install flask
      => Successfully created virtual environment!
      => To activate this project's virtualenv, run pipenv shell.
      => Alternatively, run a command inside the virtualenv with pipenv run.
    - Add absolute import and print function
      - terminal: touch __init__.py && touch __main__.py
    - Open project in IDE
      - terminal: code .
    - Add git and github repo
      - terminal: git init
      - Add and commit all files
      - (Optional) Add a README, LICENSE, and gitignore
      - On Github, click "Add new Repository"
        - Don't initialize with Readme, license, or gitignore
      - terminal: git remote add origin git@github.com:<gh username>/<repo name>
        - git remote add origin git@github.com:priyapower/Kudos.git
      - terminal: git push -u origin main
      - Refresh github repo and you should see your project
    - Add details to main.py

# Backend user stories
  - Add schemas for our work
    - terminal: mkdir -p app/kudo
      - What is the '-p' flag?
      - Creates missing intermediate path name directories. If the -p flag is not specified, the parent directory of each-newly created directory must already exist
    - terminal: touch app/kudo/schema.py
    - terminal: touch app/kudo/service.py
    - terminal: touch app/kudo/__init__.py
  - QUESTION: HOW DO WE TEST????? I know we have PyTest, but what does TDD look like for schema development?
  - Schema in Python
    - The schemas were created to represent the incoming request data as well as the data your application persists in the MongoDB
    - General definition: schema is a library for validating Python data structures, such as those obtained from config-files, forms, external services or command-line parsing, converted from JSON/YAML (or something else) to Python data-types
  - Update schema.py file
    - Marshmallow: https://marshmallow.readthedocs.io/en/stable/
      - Marshmallow is an ORM/ODM/framework-agnostic library for serializing/deserializing complex data types, such as objects, to and from native Python data types
    - terminal: pipenv install marshmallow
    - Add schema details
  - MongoDB REST API persistence
    - terminal: pipenv install pymongo
    - Install Docker and docker-compose
      - https://docs.docker.com/desktop/install/mac-install/
        - Install Docker desktop as an Application
        - Open Docker verify and accept terms
        - Docker Desktop comes with Docker Compose
    - Add docker compose yml
      - terminal: touch docker-compose.yml
    - Spin up docker with mongodb (this is a db server, so you might want to use a new tab in your terminal)
      - terminal: docker-compose up
        - You must have docker desktop running for this to work
        - You should now see "Kudos" project on your Docker Desktop!
    - Build MongoRepository class
      - terminal: mkdir -p app/repository
