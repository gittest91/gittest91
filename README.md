Thanks, Kyle. The local end-to-end testing has completed successfully. I haven't checked the current test coverage percentage yet. I'll verify the coverage report and let you know.
git grep -ni "pytest-cov\|coverage\|--cov\|htmlcov\|coverage.xml"

Also check:

dir pytest.ini,pyproject.toml,setup.cfg,.coveragerc
