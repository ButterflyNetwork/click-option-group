# click-option-group

Option groups missing in Click

## The aim and motivation

## Quickstart

The example of usage:

```python
# app.py

import click
from click_option_group import optgroup, MutuallyExclusiveOptionGroup


@click.command()
@optgroup.group('Server configuration', 
                help='The configuration of some server connection')
@optgroup.option('--host', default='localhost', help='Server host name')
@optgroup.option('--port', type=int, default=8888, help='Server port')
@optgroup.option('--attempts', type=int, default=3, help='The number of connection attempts')
@optgroup.option('--timeout', type=int, default=30, help='The server response timeout')
@optgroup.group('Input data sources', cls=MutuallyExclusiveOptionGroup, required=True, 
                help='The sources of the input data')
@optgroup.option('--tsv-file', type=click.File(), help='CVS/TSV input data file')
@optgroup.option('--json-file', type=click.File(), help='JSON input data file')
@click.option('--debug/--no-debug', default=False, help='Debug flag')
def cli(**params):
    print(params)

if __name__ == '__main__':
    cli()
```

```bash
$ python app.py --help
Usage: app3.py [OPTIONS]

Options:
  Server configuration:           The configuration of some server connection
    --host TEXT                   Server host name
    --port INTEGER                Server port
    --attempts INTEGER            The number of connection attempts
    --timeout INTEGER             The server response timeout
  Input data sources: [mutually_exclusive, required]
                                  The sources of the input data
    --tsv-file FILENAME           CVS/TSV input data file
    --json-file FILENAME          JSON input data file
  --debug / --no-debug            Debug flag
  --help                          Show this message and exit.
```
