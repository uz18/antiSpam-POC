# antiSpam (Proof of Concept)
## [https://antibot.dev/](https://antibot.dev/)

This is a proof-of-concept project that aims to detect and prevent automated bots from accessing protected pages on a webpage. 
* It uses a series of randomly sorted JavaScript challenges to identify the presence of headless browsers, such as Puppeteer, Puppeteer Stealth, Selenium, etc.
* My goal with this project is to be able to prevent automated requests on my personal projects while capturing and storing as little personally identifiable information as possible :)

This project was largely inspired by [Challenger](https://github.com/wwhtrbbtt/Challenger), [CreepJS](https://abrahamjuliot.github.io/creepjs/) and [Browserscan](https://www.browserscan.net/en)

## How it Works
- Challenge Generation: This project uses the [cy_jsvmp](https://github.com/2833844911/cy_jsvmp) library to compile and further obfuscate a randomly ordered and obfuscated set of JavaScript challenges (currently 50 total). These challenges are designed specifically to detect the presence of automated browsers.
- Challenge Retrieval: The compiled challenges, which contain a unique challengeID, are exposed through the [/challenges](https://antibot.fly.dev/challenges) endpoint which is automatically called when the gif on the homepage is loaded.
- Challenge Execution: The client-side (webpage) executes the received compiled challenges on the user's device. The challenges produce a result based on the detected browser environment and the unique order of the challenges.
- Result Submission: The client submits the challenge result, along with the corresponding challengeID, to the [/submit](https://antibot.fly.dev/submit) endpoint.
- Result Validation: The server compares the submitted challenge result with the expected result associated with the challengeID. If the submitted result matches the expected result, the server generates a valid cookie.
- Access Control: The generated cookie can be used to grant access to protected pages or resources on the website. This ensures that only clients who have successfully passed the challenge are allowed access.
- Attempt Limit: To prevent brute-force attacks, there is a maximum limit of three attempts to solve each challenge. If a client fails to provide the correct result within three attempts, the challenge and all of its associated data are deleted, thus making it unsolvable, and the client must restart the process.

## Future Plans 
- A "weighting" system similar to [Challenger](https://github.com/wwhtrbbtt/Challenger) which attributes a certain "weight" value to each challenge. This would allow for a valid cookie to be generated even if certain challenges fail (either for compatibility or low/medium/high security designation for different endpoints)
- More obfuscation, randomization and encryption for the payload
- More JS challenges (including WebRTC checks, WebGL Checks, etc)
- IP reputation logic
- Randomization of the VM that the payload runs on
- Better support for use on external sites/apps

## Privacy and Security
The client's IP address, JA3 fingerprint, and user-agent are logged when retrieving challenges from the /challenges endpoint and compared against the IP address, JA3 fingerprint, and user-agent during result submission and any protected endpoints.
No other personally identifiable information is collected or stored by the system and all information stored is displayed to the user.

## Disclaimer
Please note that the GIFs used in this project are sourced from [Tenor](https://tenor.com/) and do not belong to the project owner.
