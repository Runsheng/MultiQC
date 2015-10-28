---
title: Plugins
layout: toc
---

# MultiQC Plugins
MultiQC is written around a system designed for extensibility and plugins.
These features allow custom code to be written without polluting the central
code base.

Please note that we want MultiQC to grow as a community tool! So if you're
writing a module or theme that can be used by others, please keep it within
the main MultiQC framework and submit a pull request.

## Entry Points
The plugin system works using setuptools
[entry points](https://pythonhosted.org/setuptools/setuptools.html#dynamic-discovery-of-services-and-plugins).
In `setup.py` you will see a section of code that looks like this _(truncated)_:
```python
entry_points = {
    'multiqc.modules.v1': [
        'qualimap = multiqc.modules.qualimap:MultiqcModule',
    ],
    'multiqc.templates.v1': [
        'default = multiqc.templates.default',
    ],
    # 'multiqc.hooks.v1': [
        # 'execution_start = myplugin.hooks:execution_start',
    # ]
},
```

These three sets of entry points define the modules and templates available
to MultiQC, as well as description additional functions to be run as hooks.

Any python program can create entry points with the same name, once installed
MultiQC will find these and run them accordingly. For an example of this in
action, see the [MultiQC_NGI](https://github.com/ewels/MultiQC_NGI/blob/master/setup.py)
setup file:
```python
entry_points = {
        'multiqc.templates.v1': [
            'ngi = multiqc_ngi.templates.ngi',
            'genstat = multiqc_ngi.templates.genstat',
        ],
        'multiqc.hooks.v1': [
            'after_modules = multiqc_ngi.hooks:after_modules',
        ]
    },
```

Here, two new templates are added, plus a new code hook.

## Modules
List items added to `multiqc.modules.v1` specify new modules. They should
be described as follows:
```
modname = python_mod.dirname.submodname:classname'
```

Once this is done, everything else should be the same as described in the
[writing modules](writing_modules.md) documentation.

## Templates
As above, though no need to specify a class name at the end. See the
[writing templates](templates.md) documentation for further instructions.

## Hooks
Hooks are a little more complicated - these define points in the core
MultiQC code where you can run custom functions. This can be useful as
your code is able to access data generated by other parts of the program.
For example, you could tie into the `after_modules` hook to insert data
processed modules into a database automatically.

Here, the entry point names are the hook titles, described as commented out
lines in the core MultiQC `setup.py`: `execution_start`, `before_modules`,
`after_modules` and `execution_finish`.

These should point to a function in your code which will be executed when
that hook fires. Your custom code can import the core MultiQC modules to
access configuration and loggers. For example:

```python
#!/usr/bin/env python
""" MultiQC hook functions - we tie into the MultiQC
core here to add in extra functionality. """

import logging
from multiqc.utils import (report, config)

log = logging.getLogger('multiqc')

def after_modules():
  """ Plugin code to run when MultiQC modules have completed  """
  num_modules = len(report.modules_output)
  status_string = "MultiQC hook - {} modules repoted!".format(num_modules)
  log.critical(status_string)
```