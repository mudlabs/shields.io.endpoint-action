# Shieldsio Endpoints
A GitHub Action to retrieve [Shields.io][shields.io] markdown badges.
- This Action and its sister [repository][library] are _NOT_ products of, or affiliated with [Shields.io][shields.io]


## Table of Contents
- [Usage](#usage)
- [Outputs](#outputs)


### Usage
This Github Action retrieves [Shields.io][shields.io] badges from its sister repository, [`mudlabs/shieldsio`][library].
```yaml
- name: Shieldsio Endpoints
  uses: mudlabs/shieldsio-endpoints@v1.0.0
  with:
    # REQUIRED
    # The name of a badge on this actions sister repository.
    # https://github.com/mudlabs/shieldsio
    badge: github-action
    # If you plan on using the badge as a link to some content, you can
    # provide that here. This will be returned in the outputs `ref` prop.
    href: 'https://github.com/marketplace/actions/shieldsio-endpoints'
    # Overrides the badges preset property.
    label: Foo
    # Overrides the badges preset property.
    color: red
    # Overrides the badges preset property.
    labelColor: black
    # Some of the badges use named logos and some use custom svg logos.
    # Shields.io does not let you specify a color for custom logos, so we
    # will make the change for you.
    logoColor: 'c50f0f'
    # Overrides the badges preset property.
    # Default: for-the-badge.
    style: flat
```

---


### Outputs
```yaml
# A markdown formatted string you can use to display the badge
# I.e. [github-action]: https://img.shields.io/endpoint?url=...
steps.shieldsio.outputs.badge
# A markdown flavoured string you can use to reference your badge.
# If you specified the inputs `href` property it will look something like this;
# ![github-action](https://github.com/marketplace/actions/shieldsio-endpoints)
steps.shieldsio.outputs.ref
```


---


[library]: https://github.com/mudlabs/shieldsio
[shields.io]: https://shields.io/
