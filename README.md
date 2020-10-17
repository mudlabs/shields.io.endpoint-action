# Shields.io Endpoints
A GitHub Action to retrieve or generate [Shields.io][shields.io] markdown badges.


## Table of Contents
- [Usage](#usage)
- [Inputs](#inputs)
- [Outputs](#outputs)


### Usage
```yaml
- name: Shields.io Endpoints
  uses: mudlabs/shields.io.endpoints@v1.0.0
  with:
    badge: github-action
```


### Inputs
| Input | Type | Description | Default |
| --- | --- | --- | --- |
| `badge` | string | The name of an available badge on this actions sister repository, [mudlabs/shields.io.endpoint][library]. | |
| `endpoint` | JSON | Your own json endpoint for the action to create somewhere on your repo. | |
| `path` | string | A path to where you want the new `endpoint` file located on your repo. If this path ends in a `.json` file, that will be the files name. | `./` |
| `replaces` | string | A path to an existing endpoint file this one replaces. This file will be removed. | |
| `prepend` | boolean | Specifies the filename for the generated endpoint should be prepended with a random _id_. If no filename is specified under `path`, this will be the filename _(even if you specify false)_. | `true` |


### Outputs
| Output | Type | Description |
| --- | --- | --- |
| `badge` | string | A markdown formatted string you can use to display the badge _(i.e. `[my-badge]: shield.io/badge/url`)_. |
| `ref` | string | A markdown flavoured string you can use to reference you badge _(i.e. `![my-badge]`)_. |
| `path` | string | The path to your generated endpoint, if that was the action you requested. |
| `name` | string | The filename of your endpoint, or badge if that's what you requested. |


### Notes:
- The Action does not commit any changes to your repository. I recomment using [Add & Commit](https://github.com/marketplace/actions/add-commit) for this.
- This Action and its sister [repository][library] are _NOT_ products of, or affiliated with [Shields.io][shields.io]

[library]: https://github.com/mudlabs/shields.io.endpoint
[shields.io]: https://shields.io/
