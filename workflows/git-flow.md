# Git Flow
Introduced in 2010 by Vincent Driessen, Git-Flow presents an alternative branching model. This model utilizes feature branches and multiple primary branches assigning them specific roles and defining rules for their interaction. 


## Workflow

The concept of the Git Flow utilizes two branches for storying the history of a project. The first one, the `main`, holds the official release history. The second one, the `develop`, is used for integrating individual features. 

1. MAIN
Unlike the `develop` branch, the `main` should always provide the most stable and deploytable state of the project. Only the finalized features should be merged into the `main` branch. Each commit to the `main` branch should represent a new version of the project with consistent notation in place. 

2. DEVELOP 
In the `develop` branch, new features should be tested. Prior merging them to the `main` branch, interaction between new features is tested on the `develop` branch to ensure proper functionality. Feature branches are created from the `develop` branch. Once completed, they are merged back to the `develop` branch. Hence, the `develop` branch serves primarily as a staging area for new features, allowing for testing compatibility of newly developed features. This results in high frequency of updates of the `develop` branch. 

To conclude, the `main` brach is a stable production line with deployable code. On the contrary, the `develop` branch serves as a place for testing, integrating and developing features. This separation allows for maintaing stable production while allowing for continuous development in a controlled manner at the same time. 

## Feature Branches

As mentioned previously, features do not directly interact with the `main` branch. Features use the `develop` branch as their parent branch. Once feature is complete it is merged back to the `develop` branch. 

### Creating a feature branch

Without the git-flow extensions:
> git checkout develop
> git checkout -b feature_branch

When using git-flow extension:
> git flow feature start feature_branch

### Finishing a feature branch 

When the feature development is finished, the `feature_brach` is merged into `develop` branch.

Without the git-flow extensions:
> git checkout develop
> git merge feature_branch

When using git-flow extension:
> git flow feature finish feature_branch

## Release Branches

Once `develop` has enough features for a release, `release` branch is forked off from `develop`. This allows to prepare a potential branch for merging into `main` without affecting further work on the `develop` branch. Once it is ready to ship, the `release` branch is merged into `main`, creating a new release. The `release` is also merged back to the `develop` to ensure consistency of versions between `main` and `develop`. Like `feature` branches, `release` branches are also based on the `develop` branch. A new `release` branch is created as follows:

Without the git-flow extensions:
> git checkout develop
> git checkout -b release/0.1.0

When using git-flow extension:
> $ git flow release start 0.1.0
> Switched to a new branch 'release/0.1.0'

Following code can be used to finish a `release` branch:

Without the git-flow extensions:
> git checkout main
> git merge release/0.1.0

Or with the git-flow extension:
> git flow release finish '0.1.0'

----

## Hotfix Branches
In the git-flow, it is also crucial to be able to quickly patch production releases. `Hotfix` branches are similar to the `release` branches. The only difference is that they are based on `main` instead of `develop` branch. After merging `hotfix` back to the `main`, it should be merged into the `develop` as well. `Hotfix` branch can be created using the following methods:

Without the git-flow extensions:
> git checkout main
> git checkout -b hotfix_branch

When using the git-flow extensions:
> $ git flow hotfix start hotfix_branch

Similar to finishing a `release` branch, a `hotfix` branch gets merged into both `main` and `develop`.

> git checkout main
> git merge hotfix_branch
> git checkout develop
> git merge hotfix_branch
> git branch -D hotfix_branch
> $ git flow hotfix finish hotfix_branch

-----
