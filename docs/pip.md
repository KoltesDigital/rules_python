<!-- Generated with Stardoc: http://skydoc.bazel.build -->

<a name="#pip_import"></a>

## pip_import

<pre>
pip_import(<a href="#pip_import-name">name</a>, <a href="#pip_import-requirements">requirements</a>)
</pre>

A rule for importing `requirements.txt` dependencies into Bazel.

This rule imports a `requirements.txt` file and generates a new
`requirements.bzl` file.  This is used via the `WORKSPACE` pattern:

```python
pip_import(
    name = "foo",
    requirements = ":requirements.txt",
)
load("@foo//:requirements.bzl", "pip_install")
pip_install()
```

You can then reference imported dependencies from your `BUILD` file with:

```python
load("@foo//:requirements.bzl", "requirement")
py_library(
    name = "bar",
    ...
    deps = [
       "//my/other:dep",
       requirement("futures"),
       requirement("mock"),
    ],
)
```

Or alternatively:
```python
load("@foo//:requirements.bzl", "all_requirements")
py_binary(
    name = "baz",
    ...
    deps = [
       ":foo",
    ] + all_requirements,
)
```


### Attributes

<table class="params-table">
  <colgroup>
    <col class="col-param" />
    <col class="col-description" />
  </colgroup>
  <tbody>
    <tr id="pip_import-name">
      <td><code>name</code></td>
      <td>
        <a href="https://bazel.build/docs/build-ref.html#name">Name</a>; required
        <p>
          A unique name for this repository.
        </p>
      </td>
    </tr>
    <tr id="pip_import-requirements">
      <td><code>requirements</code></td>
      <td>
        <a href="https://bazel.build/docs/build-ref.html#labels">Label</a>; required
        <p>
          The label of the requirements.txt file.
        </p>
      </td>
    </tr>
  </tbody>
</table>


<a name="#pip_repositories"></a>

## pip_repositories

<pre>
pip_repositories()
</pre>

Pull in dependencies needed to use the packaging rules.


