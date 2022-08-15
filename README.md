# lerna-projen

A forked version of Amin Fazl's [lerna-projen](https://github.com/AminFazlMondo/Lerna-Projen)

It adds the [independent version mode ](https://lerna.js.org/docs/features/version-and-publish#independent-mode) to allow sub-projects to be versioned independently

This is a library to use manage mono repositories using projen.

## Getting started

To create a new project, run the following command and follow the instructions:

```
console
$ mkdir my-project
$ cd my-project
$ git init
$ npx projen new --from lerna-projen
🤖 Synthesizing project...
...
```

The project type can be anything to start with, then in the `projenrc` file, initiate a lerna project and add all of the sub normal projen project to the lerna project.

### Example
```javascript
const { LernaProject } = require('lerna-projen');
const { TypeScriptProject } = require('projen');

const parentProject = new LernaProject({
  name: 'my-parent-project',
  independentMode: true
  ...
});

const firstProject = new TypeScriptProject({
  name: 'my-first-project',
  parent: parentProject,
  ...
});

parentProject.addSubProject(firstProject);

parentProject.synth()
```

The rest of the process is taken care of by projen. All of the scripts on the parent project are chained by running the same command from the sub project using lerna.
