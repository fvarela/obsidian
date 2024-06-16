
`pip install dagster~=1.7`

- Start a project from an example:
```bash
dagster project from-example --example project_dagster_university_start --name dagster_university

```

- Copy environment variables and install the project
```bash
cd .\dagster_university\
cp .\.env.example .\.env
pip install -e ".[dev]"
```

