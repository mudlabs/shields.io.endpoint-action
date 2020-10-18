# Shieldsio Endpoints
A GitHub Action to retrieve or generate [Shields.io][shields.io] markdown badges.


## Table of Contents
- [Usage](#usage)
- [Inputs](#inputs)
- [Outputs](#outputs)
- [Examplets](#examples);
- [Notes](#notes)


### Usage
```yaml
- name: Shieldsio Endpoints
  uses: mudlabs/shieldsio-endpoints@v1.0.0
  with:
    badge: github-action
```


---


### Inputs
| Input | Type | Description | Default |
| --- | --- | --- | --- |
| `badge` | string | The name of an available badge on this actions sister repository, [mudlabs/shieldsio][library]. | |
| `logoColor` | string | Only used if you are specifying `bandge`. Some of the badges use named logos and some use custom svg logos. _Shields.io_ does not let you specify a color for custom logos, so we will make the change for you. | |
| `link` | string | If you plan on using the badge as a link to some content, you can provide that link here. This will be returned in the outputs `ref` property. | |
| `endpoint` | JSON | Your own json endpoint for the action to create somewhere on your repo. | |
| `path` | string | A path to where you want the new `endpoint` file located on your repo. If this path ends in a `.json` file, that will be the files name. | `./` |
| `replaces` | string | A path to an existing endpoint file this one replaces. This file will be removed. | |
| `prepend` | boolean | Specifies the filename for the generated endpoint should be prepended with a random _id_. If no filename is specified under `path`, this will be the filename _(even if you specify false)_. | `true` |


---


### Outputs
| Output | Type | Description |
| --- | --- | --- |
| `badge` | string | A markdown formatted string you can use to display the badge _(i.e. `[my-badge]: shield.io/badge/url`)_. |
| `ref` | string | A markdown flavoured string you can use to reference your badge _(i.e. `![my-badge]`)_. If you specified the inputs `link` property it will look something like this; `![my-bandge](my-link)`. |
| `path` | string | The path to your generated endpoint, if that was the action you requested. |
| `name` | string | The filename of your endpoint, or badge if that's what you requested. |


---


### Examples

- Getting a badge, specifying your own logoColor, and link.
   ```yaml
   - uses: mudlabs/shieldsio-endpoints@v1.0.0
     id: badge
     with:
       badge: github-sponsor
       logoColor: 'c50f0f'
       link: 'https://github.com/sponsors/mudlabs'
   ```

- Creating your own badge endpoint
   ```yaml
   - uses: mudlabs/shieldsio-endpoints@v1.0.0
     with:
       endpoint: json-data
       path: ./my/endpoints/my-badge.json
       replaces: ./my/endpoints/my-badge*.json
       prepend: true
   ```

---


### Notes:
- The Action does not commit any changes to your repository. I recomment using [Add & Commit](https://github.com/marketplace/actions/add-commit) for this.
- This Action and its sister [repository][library] are _NOT_ products of, or affiliated with [Shields.io][shields.io]

[library]: https://github.com/mudlabs/shieldsio
[shields.io]: https://shields.io/
