# Shieldsio Endpoints
A GitHub Action to automate the use of markdown badges from it's sister repository [Shieldsio][library]
- This Action and the Shieldsio library are _NOT_ products of, or affiliated with [Shields.io][shields.io]


## Table of Contents
- [Usage](#usage)
  - [Generator](#generator)
  - [Read Write](#read-write)
- [Outputs](#outputs)


### Usage
There are two ways you can use this Action.

#### Generator
The generator operation allows you to create a badge from inside your workflow. The output of this operation will be a string. You can then take this Shields.io compatible markdown and insert it into any compatible document.

An example of this usage is as follows:
```yaml
- name: Shieldsio Endpoints
  uses: mudlabs/shieldsio-endpoints@v1.0.0
  with:
    # REQUIRED
    operation: generator
    # Required for generator operations.
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

The output from this workflow will be:
```yaml
# A markdown formatted string you can use to display the badge
# i.e. [github-action]: https://image.shields.io/endpoint?url=https://raw.githubusercontent.com/mudlabs/shieldsio/endpoint/badges/github-action.json
steps.shieldsio.outputs.badge

A markdown flavourd string your can use to reference your badge.
# If you specified the inputs `href` property it will look something like this:
# ![github-action](https://github.com/marketplace/actions/shieldsio-endpoints)
steps.shieldsio.outputs.ref
```

#### Read Write
The second way to use this action is to directly markdown your badge requests in your `.md` file(s). When you do this and specify `read-write` as the operation in your workflow the Action will read you markdown file(s) for specific instances of _"[Badge Request Markdown](#badge-request-markdown)"_. When it finds the markdown it with generate a badge from it and replace the markdown in that file.


> When useing the `read-write` operation your workflow can still specify global overrides for badge properties.
> However overrides in the _"Badge Request Markdown"_ will supersede overrides in a workflow.

##### Badge Request Markdown
This markdown syntax is an attempt to introduce a simple, readable method for including badges in your documentation. The most basic example is as follows.
```
This is a Github Action badge {{shieldsio:github-action}}
```

Shields.io allows you to specify property overrides to customise your badges. The _BRM_ syntax for this is simple. Each property is seperated by a `:` character. There is a default ordering of properties, as shown in the table below. You can also specify them a key/value pairs if you wish. 

> You must not mix markdown patterns within any one badge request. If you do the request will fail.

- `{{shieldsio:github-action:red}}` this will create a red github-action badge.
- `{{shieldsio:github-action:color=red}}` this will produce an error because of mismatched syntax.
- `{{shieldsio:name=github-action:color=red}}` this will creat a red github-action badge. Note the order of properties when _named_ does _not_ matter.


| Property | Value |
|---|---|
| name | The name of an existing [Shieldsio][library] badge |
| color | Supports hex, rgb, rgba, hsl, hsla and css named colors |


> The default ordering of properties is as shown in the table; from top to bottom.
> 

If you want to display the markdown in your file instead of convert it into a badge (i.e. for contributor documentation), you would immediatly prepend it with the `!` character.
```
This badge will not be generated !{{shiledsio:github-action}}
```

[library]: https://github.com/mudlabs/shieldsio
[shields.io]: https://shields.io/
