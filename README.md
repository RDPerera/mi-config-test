# Environment Config Support Testing for WSO2 MI 4.4.0

This README provides a guide for testing the environment config support feature developed for WSO2 MI 4.4.0. The tests ensure that configurables are correctly read from the environment and can be overridden in the `.env` file.

## Test Cases

### 1. Test Item 1: Use an Env Config in a File Connector to Fetch a Location

#### Steps:
- Configure an environment variable for a location (e.g., `LOCATION_PATH=/path/to/location`).
- In the file connector configuration, use this environment variable to fetch the location dynamically.

#### Expected Result:
- The file connector should successfully fetch the location from the environment variable and process files from the specified location.

#### Pass/Fail: 
- [x] Pass
- [ ] Fail

---

### 2. Test Item 2: Use .env File to Override Environment Variables in the File Connector

#### Steps:
- Create a `.env` file in the project root with the following content:
  ```
  LOCATION_PATH=/new/path/to/location
  ```
- In the file connector, reference `LOCATION_PATH` from the `.env` file.
- Restart the server to ensure the `.env` file is read.

#### Expected Result:
- The file connector should fetch the location from the `.env` file and process files from `/new/path/to/location`.

#### Pass/Fail: 
- [ ] Pass
- [ ] Fail

---

### 3. Test Item 3: Use Env Config in Payload Mediator

#### Steps:
- Define an environment variable (e.g., `API_URL=https://api.example.com`).
- In the payload mediator configuration, reference the environment variable to dynamically set the API URL.

#### Expected Result:
- The payload mediator should successfully use the environment variable `API_URL` and make requests to the correct endpoint.

#### Pass/Fail: 
- [ ] Pass
- [ ] Fail

---

### 4. Test Item 4: Use Env Config in Variable Mediator

#### Steps:
- Define an environment variable (e.g., `CUSTOM_VAR=some_value`).
- In the variable mediator, reference this environment variable and set a new variable using the value from the environment variable.
- Example configuration:
  ```xml
  <sequence xmlns="http://ws.apache.org/ns/synapse">
      <set-property name="var1" expression="get-property('CUSTOM_VAR')"/>
  </sequence>
  ```
  
#### Expected Result:
- The variable mediator should correctly set the property `var1` to the value of `CUSTOM_VAR`.

#### Pass/Fail: 
- [ ] Pass
- [ ] Fail

---

### 5. Test Item 5: Check for Multiple Overrides Between Environment and .env

#### Steps:
- Set an environment variable `API_URL=https://env-api.example.com`.
- Create a `.env` file with `API_URL=https://envfile-api.example.com`.
- Use the `API_URL` variable in both a connector and a mediator configuration.
- Restart the server to apply changes from the `.env` file.

#### Expected Result:
- The connector and mediator should both fetch the value from the `.env` file (`https://envfile-api.example.com`), overriding the environment variable.

#### Pass/Fail: 
- [ ] Pass
- [ ] Fail
