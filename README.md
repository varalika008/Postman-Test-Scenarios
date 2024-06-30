name: Automated API tests using Postman CLI

on: push

jobs:
  automated-api-tests:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install Postman CLI
        run: |
          powershell.exe -NoProfile -InputFormat None -ExecutionPolicy AllSigned -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://dl-cli.pstmn.io/install/win64.ps1'))"
      - name: Login to Postman CLI
        run: postman login --with-api-key ${{ secrets.PMAK-66816316a5839f0001ac5afe-056fc5910c99f49172302614e02d02c5dc }}
      - name: Run API tests
        run: |
          postman collection run "13519785-33dda898-b090-4739-9ba0-9ff2799d1caa" -e "13519785-f58c8576-addb-4f3e-8608-f0a666bb51d0"
