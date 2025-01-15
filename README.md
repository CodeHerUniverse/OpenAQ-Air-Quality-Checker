# Air Quality Checker

## Project Overview

The **Air Quality Checker** is a console-based application designed to evaluate air quality in a UK user-specified postcode (excluding Scotland). By entering a postcode, users receive:
- An overall Air Quality Score for the location.
- Identification of the pollutant with the highest concentration, along with its individual score.
- Explanations of the identified pollutant.

Additionally, the app generates logs to document API request statuses and flags negative pollutant readings, which could indicate faulty measurement equipment.

## APIs Used

The application integrates the following APIs:

- **OpenAQ:** Provides data on pollutant concentration and presence in specific areas.
- **Postcodes.io:** Supplies geographical details, including latitude and longitude, for UK postcodes.
- **OS Names:** Offers detailed location names and administrative details, such as boroughs and counties.

## API Key Acquisition

### OpenAQ

- Create an account (free) by following this [link](https://explore.openaq.org/register)
- Register for an API Key in the **OpenAQ Register**.
- Access your API Key via the **OpenAQ Explorer Account Settings**.
- Include the key in API requests using the **X-API-Key header**.

### OS Names

- Sign up by following this [link](https://osdatahub.os.uk/).
- Choose the "OS OpenData Plan" (Free).
- Create an account and verify it.
- Add the "OS Names API" to a new API Project via the "API Dashboard" to obtain your key.

### Postcodes.io

- This API does not require an API key.

***Note:*** API keys are securely stored in a .env file and excluded from version control using .gitignore.

## Application Features



### Setup:

- Import required libraries (see requirements.txt).
- Load API keys from the .env file.
- Define the output directory.

### User Input: 
- Prompt the user to input a postcode.
- Format the input for API queries.

### API Queries:

- Use the OS Names API to retrieve location names, postcodes, and county details.
- Query Postcodes.io for latitude and longitude.
- Fetch air quality data from OpenAQ for the provided coordinates.

### Data Processing:

- Analyze the last 30 days of hourly pollutant data.
- Group pollutants by average concentration and score them based on the European CAQI system:

![European CAQI AQI](https://github.com/user-attachments/assets/559f9af3-2e4c-4092-a20f-13e67fc28029)

- Compute the overall Air Quality Score and provide a descriptive rating.
- Identify and score the highest pollutant.
- Generate user-friendly explanations for pollutants.

### Error Handling:

- Log discrepancies or errors, such as mismatched postcodes, missing data, or negative pollutant values.
- Provide clear error messages to the user.

### Output Generation:

- Log events with timestamps in a .txt file.
- Save a detailed report for each location.
- Example Postcode Scenarios:
  - **BH9 2DH (Bournemouth):** Successful execution.
  - **BH1 2AT (Poole):** Success with data from the nearest location.
  - **B1 1AY (Birmingham):** Flags negative measurements.
  - **NG1 1AP (Nottingham):** Successful execution.
  - **DT6 6JQ (Chideock):** No data available, demonstrating error handling and logging.

### Expected Outputs

**Console Messages:**
- Location data based on the provided postcode.
- Nearest available location from OpenAQ if exact data is unavailable.
- Overall Air Quality Score for the selected area.
- Pollutant with the highest concentration and its associated score.
- Explanation of the identified pollutant.
- Error messages specifying reasons for unsuccessful requests.

**Log File:**
- Status of API requests with timestamps.
- Notes on negative pollutant readings for technical investigation.
- Details of successful and unsuccessful program executions.

**Output Files:**

- Individual .txt files for each location containing detailed user messages and outputs.
- Program Workflow

### Issues Encountered and Solutions

**Inconsistent Postcode Matching (OS Names API):**

- Verified user input against retrieved data to ensure accuracy.
- Stopped the program with a logged error if mismatched.

**Unfriendly Location Names:**

- Augmented results with county names for clarity (e.g., "Hampton - Greater London").

**Missing County Data (OS Names API):**

- Used the DISTRICT_BOROUGH field as a fallback, appending "Borough" to the name.

**Missing Coordinates:**

- Queried Postcodes.io for latitude and longitude when unavailable in OS Names API.

**Unavailable Air Quality Data (OpenAQ):**

- Used the "nearest" option to retrieve data from the closest available location.

**Long Explanatory Paragraphs:**

- Reformatted text into readable blocks for better presentation in .txt files.

## Additional Resources

- **Screenshots:** Terminal outputs and log files are included for validation.
- **Test Outputs:** Files for the example postcodes demonstrate the program's functionality.

This project showcases robust API integration, error handling, and data processing techniques, providing a user-friendly tool for evaluating air quality in specific locations.
