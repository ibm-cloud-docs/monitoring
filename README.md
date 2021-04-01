# Monitoring with Sysdig

## Local Build

- [Official Guide](https://test.cloud.ibm.com/docs/developing/writing/markdown?topic=writing-setting-up-your-markdown-environment)
1. Before One-Liner:

  ```
  npm install marked-it-cli
  ```

2. One-liner:

  ```
  pushd .. && ./monitoring/node_modules/.bin/marked-it-cli ${PWD}/monitoring --output=${PWD}/monitoring-build --overwrite --verbose; popd
  ```

3. HTML files will be in `../monitoring-build/`
