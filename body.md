name: Golang web example
on:
  push:
    branches:
        - "v1.0"
    tags:
        - "latest"

jobs
    ci:
        runs-on: ubuntu-latest
        permissions:
            contents: write
        steps:
            - name: Checkout
            - uses: actions/chekout@v4
            - name: Create tag
            - uses: rickstaa/action-create-tag@v1
                id: "tag_create"
                with:
                    tag: "latest"
                    force_push_tag: true
                    message: "Latest release"
            - name: Release
                uses: ncipollo/release-action@v1
                with:
                    skipIfReleaseExists: true
                    tag: "latest"
                    artifacts: "release.tar.gz.foo/ .txt"
            - bodyfile: body.md