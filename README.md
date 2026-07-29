pytest tests/ --cov=src --cov-report=term-missing

or exactly what Jenkins runs:

python -m pytest tests/ -v -m "not integration" --cov=src --cov-report=term
