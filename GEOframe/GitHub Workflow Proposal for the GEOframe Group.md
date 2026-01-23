# Github workflow proposal

##  General Principles

The source code of our components must remain centralized, accessible, and recoverable over time. We need a workflow that:

* ensures no work is lost;
    
* enables simple and efficient code review;
    
* keeps all repositories organized and consistent;
    
* supports reproducibility and enhances model readability.


## Structure: Branch-based Workflow

All team members work **directly within the repositories of the organization**, creating personal or thematic branches.  Forks are not used, except in special cases.
The repository should contains two main branches:
* **main** : stable, documented, production-ready version. No direct commits.
*  **dev** : integration branch where approved PRs are merged. No direct commits here either.
* 
Each developer work on its own branch creates inside the repository: `<developer-name>-<short-description>`. These branches are the space for development, experiments, and prototyping. When a bug is fixed or an enanche  is implemented, it can be subbmittet througt a  **pull request to dev**. Then merging into **main** happens only from **dev**, after tests and documentation updates.
Note:
- PRs must have **at least one mandatory reviewer**. 
- The reviewer checks:
    - code correctness,
    - consistency with the physical model,
    - absence of duplicates,    
    - documentation quality.
- Protect `main` and `dev`
	- No direct pushes allowed
	- Only merge through pull requests. [Creating a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)
	- Review required. [About pull request reviews](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/about-pull-request-reviews)
	- All checks must pass (if CI is added in the future)

Forks should be used only for: occasional contributors, short-term projects, experimental work completely indipendent  code.


##   Release Management (Automated JAR Creation)

pubblication in some maven repository????


## Testing Policy

Every module in the GEOframe ecosystem must include a basic and consistent test suite.   **Testing is not optional!!!!!**. With testing we can:
- Ensure numerical correctness.
- Validate physical consistency of models.
- Reduce bugs introduced by refactoring.
- Improve trust in scientific results.

###  Minimum Test Checklist for Each Module

1. Physical Model Tests
	- Verify that the main model equation produces reasonable outputs for known test cases.
	- If possible Include  one case from literature or previous stable versions.
	- Check sign correctness (e.g., no negative water, no negative SWE, etc.).
2. Numericall test
	- Test with extreme  values
	- Test with edge cases (empty storage, missing data).

###  Automated Testing (Continuous Integration)

ALways when merging in main branch
