[Patterns](../Patterns.md)

# Automated tests, tests, tests
All developed software must be enriched by fully automated tests. This is crucial for ensuring that we provide high-quality
software over the full lifetime of a project! In general, the earlier a bug is found, the less overhead it is to fix it and
the fewer money it costs therefore. Releases are not stressful anymore!

**Automated tests** are executed automatically on a regular basis (preferably before/after each commit; or nightly)
by Continuous Integration (http://jenkins/).

**Manual tests** are tests which are (setup and) executed manually on demand.
There should be no manual tests required for any project (with a few exceptions, though IMHO none of those are matching projects at E.S.R.Labs).

## Why automated?

- Software in the repository is in releasable state always
- Return test results quickly
- Fully reproducible test results
- Required for volatile teams (people joining/leaving)
- test-fix-test-fix-test-fix-...
- Correctness of features the engineer does not know about
- Easily test against multiple versions of another software

## Notes

- It is fine (and even likely) to: Lines of test code > Lines of productive code
- You can also formulate **organizational constraints** as tests as well (e.g. an external company implements code using a specific version of your interface)
- Every component without enough good tests has considerable **technical debt**
- Every project must have a **test framework** that enables every engineer to write every kind of test without any hassle
- There are **unit and integration tests**, talk to each other to find out how your project separates them and how your team implements tests with **real HW**
- Can and should also be implemented for integrating code of **various teams**

## Handling failing tests
If any test fails, this has to be fixed immediately, favourably by the one who broke it. It is high(est) priority of the team to keep the test CI job green. Otherwise no one else in the team can reliably continue to work or will receive test errors late.
