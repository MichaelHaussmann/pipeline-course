## Typical repo structure

- repo name
  - folder named `python` containing
    - the package name: same name as repo
      - cli > commands (using rez alias to run)
      - conf > configuration
      - core > core
        - dt > data classes (dt = "datatypes")
      - libs (or utils) > not core code used by internal repo code
      - tools (with subfolders) 
      - ui > python code containing UIs
        - qt > .ui files
  - scripts 
  - package.py
  - README.md
