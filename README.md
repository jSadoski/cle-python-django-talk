# Django - Useful Tools and Patterns

Django is a very useful batteries-included system for creating a full server-side rendered site. It's a large library of related tools, and some are often overlooked. Additionally, some of the modules can be arranged to increase effectiveness, consistency, and developer experience as you design your site. It also provides examples of how to use [PEP 484 - Type Hints](https://peps.python.org/pep-0484/) as best as currently possible with Django.

## CLEPy - Cleveland Area Python User Group

This was made for a talk at the [Cleveland Area Python User Group (CLEpy)](https://www.meetup.com/Cleveland-Area-Python-Interest-Group/) in May of 2022. If you'd like to attend or pitch your own talk, drop them a line at clevelandpython@gmail.com!

## Scenario

This demo site models a private clubhouse where only users from specific email domains are allowed to sign up. All other users are able to submit a request to join. Administrators can add email groups from the built-in admin panel.

## The Goodies

- Decorators
  - `@time_request`: Get rudimentary endpoint performance monitoring. Good for level-1 app insights and debugging.
  - `@login_required_or_401`: Django provides a great `@login_reqiured` decorator that handles a view which delivers a template. However, it's not so useful for other endpoints, such as a JSON GET/POST endpoint. This decorator will behave the same, but return `401 Unauthorized` to the client if not logged in.
  - `@allowed_methods`: Also for API endpoints, this will allow you to specify what methods are allowed for a given endpoint (`GET`, `POST`, etc.).
  - `@api_endpoint`: A combination of `@login_required_or_401`, `@allowed_methods`, and anything else you want to toss into your standard API endpoints!
- Email domain restriction
  - `EmailDomain` group management through the Django Admin panel.
  - Signals allow group assignment, triggers, and restrictions based on email address.

## Setup

### `poetry` (recommended)

If `poetry` is not installed:

```bash
python -m pip install poetry
```

Create virtual environment & install dependencies:

*Note: I use `pyenv` on macOS, and I found `python -m` to be **very important in this context.** Without it, `poetry` would install using my system python3.*

```bash
python -m poetry install
```

Open virtual environment (or just do it through VSCode):

```bash
source .venv/bin/activate
```

All set! 👍

### `pip`

Create virtual environment:

```bash
python -m venv venv
```

Install dependencies:

```bash
python -m pip install -r requirements.txt -r requirements-dev.txt
```

All set! 👍

## Run the server

*(Runs on sqlite3 for this demo)*

```bash
./manage.py migrate
./manage.py runserver
```
