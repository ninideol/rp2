# Contributing To RP2

## Table of Contents
* **[Reporting Bugs](#reporting-bugs)**
* **[Contributing To The Repository](#contributing-to-the-repository)**
  * [Development Workflow](#development-workflow)
  * [Submitting Pull Requests](#submitting-pull-requests)

## Reporting Bugs
Feel free to submit bugs via Issue Tracker.

**IMPORTANT**: RP2 stores logs and outputs locally on the user's machine and doesn't send this data elsewhere. Logs, inputs and outputs can be useful to reproduce a bug, so a user can decide (or not) to share them to help fix a problem. If you decide to share this information, be mindful of what you post or send out: stack traces are typically free of personal data, but RP2 logs, inputs and outputs, while very useful to reproduce an issue, may contain information that can identify you and your transactions. Before posting such data publicly or even sending it privately to the author of RP2, make sure that:
- the data is sanitized of personal information (although this may make it harder to reproduce the problem), or
- you're comfortable sharing your personal data.

Logs are stored in the `log/` directory and each file name is appended with a timestamp. Outputs are stored in the `output/` directory or where specified by the user with the `-o` option.

## Contributing To The Repository

### Development Workflow

The RP2 source tree contains a Makefile that has a few targets, which encapsulate common tasks that are relevant for development:
* `make`: installs RP2 package requirements
* `make archive`: creates a .zip file with the contents of the RP2 directory
* `make check`: runs all RP2 unit tests
* `make clean`: removes the virtual environment, logs, outputs, caches, etc.
* `make lint`: analyzes all Python sources with Pylint
* `make reformat`: formats all Python sources using Black
* `make typecheck`: analyzes all Python sources with Mypy static type checker

The following make targets perform static and runtime (unit test) checks: they are ran automatically in continuous integration on push and pull requests, but they are also useful while coding (use them liberally on your machine): `make check lint typecheck`

The development and test workflows are supported only on Linux and macOS (not on Windows).

Logs are stored in the `log` directory. To generate debug logs, prepend the command line with `LOG_LEVEL=DEBUG`, e.g.:
```
LOG_LEVEL=DEBUG bin/rp2.py -o output -p crypto_example_ config/crypto_example.config input/crypto_example.ods
```

### Submitting Pull Requests
Feel free to submit pull requests. Please follow these practices:
- follow the [PEP 8](https://www.python.org/dev/peps/pep-0008/) coding standard and use `make reformat` before pushing;
- add [unit tests](test/) for any new code;
- make sure your code doesn't cause new issues with `make check lint typecheck`;
- ensure your commits are atomic (one feature per commit);
- write a clear log message for your commits.