# Release guide
#
# Audience: maintainers of Genesis Design System

This document explains the exact steps required to cut a new version of the
design-system so that consumers can start using the updated package.

## 1. Author a changeset

Run the interactive CLI and describe **why** the change is user-facing.

```bash
yarn changeset
```

Commit the generated file.

## 2. Merge into `main`

CI makes sure the build stays green. A typical PR will contain:

* Implementation code  
* Storybook stories  
* Tests  
* A `changeset/*.md` file

## 3. Bump versions

Checkout `main`, then bump package versions and changelog headings:

```bash
yarn changeset version
git add .
git commit -m "chore(release): version packages"
```

## 4. Create & push a tag

```bash
git tag -s vX.Y.Z -m "Genesis DS vX.Y.Z"
git push origin vX.Y.Z
```

Replace `X.Y.Z` with the version created in step 3.

## 5. Wait for the Azure pipeline

The **Build & Test** pipeline runs automatically for every tag. When finished it
uploads two artefacts:

| Artefact name | Description                     |
| ------------- | ------------------------------- |
| gends-dist    | Compiled library (ES, CJS, UMD) |
| storybook     | Static Storybook site           |

## 6. Share the release

Consumers can either:

1. Pin to the git tag in their `package.json`.
2. Download the artefact and publish it to the internal registry.

That’s it – no external registry or manual copying of `dist/` is needed!
