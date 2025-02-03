# yearly-version
Simple reusable workflow for YYYY.XX version.

Use the current year and increment a repository variable (`RELEASE_NUMBER`) for the second number.

## Enable increment

Get a [Personal Access Token (PAT)](https://github.com/settings/tokens) with all repo access and save it as a secret named: `GH_PAT`. 

## Usage

Create a workflow and reference it:

```yml
name: Get Version

jobs:
  version:
    uses: starburst997/yearly-version/.github/workflows/version.yml@v1
    secrets: inherit
    with:
      increment: false

  test_version:
    name: Get Version
    runs-on: ubuntu-latest
    needs: [version]
    steps:
      - name: Display version
        run: |
          echo "Year: ${{ needs.version.outputs.year }}"
          echo "Release: ${{ needs.version.outputs.release }}"
          echo "Version: ${{ needs.version.outputs.version }}"
```

Was made to save me a bit of time since I do love the `YEAR.RELEASE.BUILD` (ex; `2025.1.23`) format of versioning for products.

Whenever I do a new build, only `BUILD` is incremented, when I do a new public release, `RELEASE` is incremented. `YEAR` is whatever year it is currently at the time of the build.

Semantic versioning is of course much better for library, frameworks, etc. But to each it's own, it's a pretty subjective matter.