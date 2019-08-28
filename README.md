# Monitoring with Sysdig

## Local Build

- [Official Guide](https://test.cloud.ibm.com/docs/developing/writing/markdown?topic=writing-setting-up-your-markdown-environment)
1. Before One-Liner:

  ```
  npm install marked-it-cli
  ```

2. One-liner:

  ```
  pushd .. && ./Monitoring-with-Sysdig/node_modules/.bin/marked-it-cli ${PWD}/Monitoring-with-Sysdig --output=${PWD}/Monitoring-with-Sysdig-build --overwrite --verbose; popd
  ```

3. HTML files will be in `../Monitoring-with-Sysdig-build/`
