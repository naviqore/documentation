# Release

## Semantic Versioning

This project adheres to [Semantic Versioning](https://semver.org/). We use a three-part version numbering system:
`MAJOR.MINOR.PATCH`. Here is what each part represents:

- **MAJOR version** when we make incompatible API changes,
- **MINOR version** when we add functionality in a backwards compatible manner, and
- **PATCH version** when we make backwards compatible bug fixes.

Version tags are prefixed with a `v`, e.g., `v3.1.4`.

## Release Process

To ensure a smooth and consistent release process, follow these steps:

1. **Release branch:**
   Create a new release branch from `main` with the semantic version number to be
   published: `git checkout -b release/vX.X.X`

2. **Version and documentation:**
   Set the correct version number in the version file (`pom.xml`, `CMakeLists.txt`, `package.json` `poetry.toml`, ...).
   Update any other necessary documentation.

3. **Pull request:**
   Submit a pull request with the new version number and documentation changes. Include a release description to be used
   later in the release. Since we are generating the changelog automatically, keep it concise and mention the most
   important aspects.

4. **Publish:**
   Upon review and merging of the pull request, use the GitHub web interface to create a new release
   named `<REPOSITORY-NAME> <X.X.X>` (e.g., `public-transit-service 0.2.1`). Set the version tag as `vX.X.X` and
   automatically generate the changelog for the release. Add the release description from the PR comment and hit
   publish, which triggers the appropriate GitHub actions (e.g., Maven or Docker Publish).
