# aar-doc-config

> [!WARNING]
> **This repository has moved to GitHub:
> [github.com/lingfra/aar-doc-config](https://github.com/lingfra/aar-doc-config).**
> The Codeberg repository is no longer maintained.
>
> In July 2026 the Codeberg e.V. assembly
> [voted](https://blog.codeberg.org/protecting-our-floss-commons-from-llms.html)
> to extend Codeberg's Terms of Use with
> [§ 2 (1) 7](https://codeberg.org/Codeberg/org/commit/71149c7fc95ccfeae36109b5cddca339e4aa1473),
> which prohibits sharing projects that mostly consist of code written by
> generative AI tools such as Claude or OpenAI Codex. AI assistance is used for
> this repository, so it moved to GitHub.

Repository containing configurations and templates for
[Automated-Ansible-Role-Documentation](https://github.com/telekom-mms/Automated-Ansible-Role-Documentation).

## Prerequisites

[Automated-Ansible-Role-Documentation](https://github.com/telekom-mms/Automated-Ansible-Role-Documentation)
need to be installed. Follow the install instructions on upstream.

## Installation

The recommended way is to add this repository as [git
submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) to another
repository (which is properly an Ansible collection).

1. Add as submodule:

    ```bash
    cd /path/to/your/project
    git submodule add https://github.com/lingfra/aar-doc-config.git .aar_doc
    ```

2. Add `.aar_doc.yml` and configure the template path:

    ```yaml
    ---
    output_template: .aar_doc/templates/role.md.j2
    ```

## Usage

Generate README.md for role _foo_:

```bash
aar-doc roles/foo markdown
```

Generate defaults, but overwrite the default output file name (`main.yml`) to
`main.yaml`:

```bash
aar-doc --output-file main.yaml roles/foo defaults
```

## Custom Documentation

It may be desired to add additional information to the role documentation, which
doesn't fit into the `argument_specs.yaml` file. For this purpose the template
optionally include two templates from the role:

- `templates/doc/preface.md.j2`: Included between the top level section and the
`Role Arguments` section. Can be used to add an elaborate description to the top
level section or other sections that make sense to be placed before the
arguments like _Features_, _Limitations_ or _Requirements_.
- `templates/doc/closure.md.j2`: Included between _Example Playbook_ and
_Project Information_ (the last section). Can be used to add more elaborate
example playbooks and/or other documentation, which make sense to be placed at
the end of the document.

The template variables are known in the included templates, see the Jinja2
upstream documentation on
[Include](https://jinja.palletsprojects.com/en/stable/templates/#include) and
[Import Context
Behavior](https://jinja.palletsprojects.com/en/stable/templates/#import-visibility)
for more information.

Please note some hints to comply with
[markdownlint](https://github.com/DavidAnson/markdownlint) rules
[`MD012`](https://github.com/DavidAnson/markdownlint/blob/main/doc/md012.md) and
[`MD022`](https://github.com/DavidAnson/markdownlint/blob/main/doc/md022.md):
Start the custom template with **one** blank line. Avoid leading blank lines.
The include tag in the template already creates the necessary blank line needed
for the next heading.

## License

[MIT](./LICENSE.md)

## Acknowledgments

This templates are derived of the provided template from
[telekom-mms/Automated-Ansible-Role-Documentation](https://github.com/telekom-mms/Automated-Ansible-Role-Documentation)
(MIT License):

- [Miika Kankare](https://github.com/quulah) (original author)
- [Kevin P. Fleming](https://github.com/kpfleming) (contributions to the
original project)
- [Sebastian Gumprich](https://github.com/rndmh3ro) from
[telekom-mms](https://github.com/telekom-mms)

Thanks for your work!
