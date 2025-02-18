# Environment Config Support Testing for WSO2 MI 4.4.0  

This README provides a guide for testing the environment config support feature developed for WSO2 MI 4.4.0. The tests ensure that configurables are correctly read from the environment and can be overridden in the `.env` file.  

## Test Cases and Results  

### 1. Use an Env Variable Deployed in Env in File Connector to Get a File Location (Deployed Manually via MicroIntegrator)  

#### Steps:  
- Configure an environment variable for a file location:  
  ```bash
  export LOCATION_PATH=/Users/dilanperera/files
  ```  
- In the file connector configuration, reference this environment variable to fetch the file location.  
- Deploy manually via MicroIntegrator.  

#### Expected Result:  
- The file connector should successfully fetch the location from the environment variable.  

#### Actual Result:  
✅ **Worked**  

#### Pass/Fail:  
✅ **PASS**  

---  

### 2. Use an Env Variable Deployed in Env in File Connector to Get a File Location (Deployed via VS Code)  

#### Steps:  
- Configure an environment variable for a file location:  
  ```bash
  export LOCATION_PATH=/Users/dilanperera/files
  ```  
- In the file connector configuration, reference this environment variable to fetch the file location.  
- Deploy via VS Code.  

#### Expected Result:  
- The file connector should successfully fetch the location from the environment variable.  

#### Actual Result:  
❌ **Not Worked**  

#### Pass/Fail:  
✅ **PASS** 

---  

### 3. Use an Entry in .env File to Store a Config and Use in File Connector to Get a File Location (Deployed via VS Code)  

#### Steps:  
- Add the following entry to the `.env` file:  
  ```
  LOCATION_PATH=/Users/dilanperera/files
  ```  
- In the file connector configuration, reference `LOCATION_PATH` from the `.env` file.  
- Deploy via VS Code.  

#### Expected Result:  
- The file connector should fetch the location from the `.env` file.  

#### Actual Result:  
✅ **Worked**  

#### Pass/Fail:  
✅ **PASS**  

---  

### 4. Use Both .env and Env-Set Variable, Fetch the Config in Payload Mediator (Check Override Behavior)  

#### Steps:  
- Set an environment variable:  
  ```bash
  export CONFIG_VALUE=env_config
  ```  
- Add an entry in the `.env` file:  
  ```
  CONFIG_VALUE=envfile_config
  ```  
- In the payload mediator, reference `CONFIG_VALUE`.  
- Deploy and observe which value is picked up.  

#### Expected Result:  
- The payload mediator should fetch `CONFIG_VALUE`.  
- The environment variable should override the `.env` value.  

#### Actual Result:  
❓ **Not Sure**  

#### Pass/Fail:  
❓ **PASS** (Further verification needed.)  

---  

### 5. Use .env Config in Variable Mediator  

#### Steps:  
- Add the following entry to the `.env` file:  
  ```
  CUSTOM_VAR=some_value
  ```  
- In the variable mediator, reference `CUSTOM_VAR` and set it as a new property.  

#### Expected Result:  
- The variable mediator should correctly set `CUSTOM_VAR` from the `.env` file.  

#### Actual Result:  
✅ **Working**  

#### Pass/Fail:  
✅ **PASS**  

---  

### 6. Use a Config in DS Configs  

#### Steps:  
- Try using an environment-configured value in a DS (Data Service) configuration.  

#### Expected Result:  
- The configuration should support environment variables.  

#### Actual Result:  
🚫 **Not Available**  

#### Pass/Fail:  
❌ **Fail**  

Created an issue: https://github.com/wso2/mi-vscode/issues/889
