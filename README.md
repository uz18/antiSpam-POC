# antiSpam (Proof of Concept)
## https://antibot.fly.dev 

This is a proof-of-concept project that aims to detect and prevent automated bots from accessing protected pages on a website. \
* It uses a series of randomly sorted JavaScript challenges to identify the presence of headless browsers, such as Puppeteer, Puppeteer Stealth, Selenium, and others. \
* My goal with this project is to be able to prevent automated requests on my personal projects while capturing and storing as little personally identifiable information as possible. :) 

A big inspiration for this project has been https://github.com/wwhtrbbtt/Challenger

## How it Works
- Challenge Generation: The system utilizes the cy_jsvmp library to compile and obfuscate a set of JavaScript challenges. These challenges are designed to detect the presence of automated browsers.
- Challenge Retrieval: The compiled challenges, along with a unique challengeID, are exposed through the /challenges endpoint. Clients can retrieve the challenges by making a request to this endpoint.
- Challenge Execution: The client-side application executes the received compiled challenges on the user's device. The challenges produce a result based on the detected browser environment.
- Result Submission: The client submits the challenge result, along with the corresponding challengeID, to the /submit endpoint.
- Result Validation: The server compares the submitted challenge result with the expected result associated with the challengeID. If the submitted result matches the expected result, the server generates a valid cookie.
- Access Control: The generated cookie can be used to grant access to protected pages or resources on the website. This ensures that only clients who have successfully passed the challenge are allowed access.
- Attempt Limit: To prevent brute-force attempts, the system imposes a maximum limit of three attempts to solve each challenge. If a client fails to provide the correct result within three attempts, the challenge becomes unsolvable, and the client must restart the process.
  
## Privacy and Security
The client's IP address is logged when retrieving challenges from the /challenges endpoint and compared against the IP address during result submission at the /submit endpoint.
No other personally identifiable information is collected or stored by the system.

## Disclaimer
Please note that the GIFs used in this project are sourced from Tenor and do not belong to the project owner.
