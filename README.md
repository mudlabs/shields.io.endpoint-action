# Shieldsio Endpoints
A GitHub Action to retrieve or generate [Shields.io][shields.io] markdown badges.


## Table of Contents
- [Usage](#usage)
- [Outputs](#outputs)
- [Examplets](#examples);
- [Notes](#notes)


### Usage
There are two operations you can perform, with this Github Action.
1. Retrieve a badge from this actions sister repository, [`mudlabs/shieldsio`][library]
2. Create an endpoint on your repository. _Make sure you checkout your repo first_
```yaml
- name: Shieldsio Endpoints
  uses: mudlabs/shieldsio-endpoints@v1.0.0
  with:
    # The name of a badge on this actions sister repository.
    # https://github.com/mudlabs/shieldsio
    badge: github-action
    # Some of the badges use named logos and some use custom svg logos.
    # Shields.io does not let you specify a color for custom logos, so we
    # will make the change for you.
    logoColor: 'c50f0f'
    # If you plan on using the badge as a link to some content, you can
    # provide that here. This will be returned in the outputs `ref` prop.
    href: 'https://github.com/marketplace/actions/shieldsio-endpoints'
    # The json endpoint you want written to you repository.
    endpoint: json-data
    # A path to where you want the new `endpoint` file located on your repo. 
    # If this path ends in a `.json` file, that will be the filename.
    path: ./my/endpoint/badge.json
    # A path to an existing endpoint file this one replaces.
    # If you've been creating badges with `prepend`, you can specify a
    # glob like this example.
    replaces: ./my/endpoint/badge*.json
    # Specifies the filename for the generated endpoint should be prepended 
    # with a random ID. If no filename is specified under `path`, this will 
    # be the filename, even if you specify false.
    prepend: true;
```

---


### Outputs
| Output | Type | Description |
| --- | --- | --- |
| `badge` | string | A markdown formatted string you can use to display the badge _(i.e. `[my-badge]: shield.io/badge/url`)_. |
| `ref` | string | A markdown flavoured string you can use to reference your badge _(i.e. `![my-badge]`)_. If you specified the inputs `href` property it will look something like this; `![my-bandge](my-link)`. |
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
