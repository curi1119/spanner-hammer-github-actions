# Spanner Hammer Github Actions

Run hammer for Google Cloud Spanner on Github Actions.  
Support following commands:
- create
- diff
- apply

## Example configuations

If you are using spanner-emulator, config `use_emulator: true`.  
See full example [here](https://github.com/curi1119/spanner-hammer-github-actions/blob/main/.github/workflows/test.yaml).
```
jobs:
  test:
    name: test
    services:
        image: gcr.io/cloud-spanner-emulator/emulator:latest
        ports:
          - 9010:9010
          - 9020:9020
    steps:
      - name: Create Spanner instance
~~~~
      - name: test-apply
        uses: curi1119/spanner-hammer-github-actions@v1.0.2
        with:
          schema: db/schema.sql
          hammer_cmd: apply
          project_id: emu-project
          instance_id: emu-instance
          database_id: emu-database
          use_emulator: true
```

If you are targeting real Spanner, save your credentials json on GitHub Secret.
```
      - name: test-apply
        uses: curi1119/spanner-hammer-github-actions@v1.0.2
        with:
          schema: db/schema.sql
          hammer_cmd: apply
          project_id: your-project-id
          instance_id: your-instance-id
          database_id: your-database-id
          google_application_credentials: ${{secrets.your_gcp_credenttial}} 
```
