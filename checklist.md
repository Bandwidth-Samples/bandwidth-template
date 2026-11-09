# Sample App Checklist

## README

 - Is README title correct?
 - Does the README content match that of other sample apps of the same type?
 - Is the correct image in the README and repo?
   - Image should link to product specific Quick Start Guide/About Page
   - Voice:
     - Copy `icons/icon-voice.svg` from this repo to `icon-voice.svg` in the sample's root
     - Header should be:

       ```html
       <a href="https://dev.bandwidth.com/docs/voice/programmable-voice/quickStart/">
         <img src="./icon-voice.svg" title="Voice Quick Start Guide" alt="Voice Quick Start Guide"/>
       </a>
       ```
   - Messaging:
     - Copy `icons/icon-messaging.svg` from this repo to `icon-messaging.svg` in the sample's root
     - Header should be:

       ```html
       <a href="https://dev.bandwidth.com/docs/messaging/quickStart">
         <img src="./icon-messaging.svg" title="Messaging Quick Start Guide" alt="Messaging Quick Start Guide"/>
       </a>
       ```
   - MFA:
     - Copy `icons/icon-mfa.svg` from this repo to `icon-mfa.svg` in the sample's root
     - Header should be:

       ```html
       <a href="https://dev.bandwidth.com/docs/mfa/">
         <img src="./icon-mfa.svg" title="Multi-Factor Auth About Page" alt="Multi-Factor Auth About Page"/>
       </a>
       ```
 - Does the TOC match the template and rest of README? A leading space before `# Table of Contents` is fine
 - Is description correct?
   - phone numbers to use in order: +19195551234, +19195554321
   - sample text should be "Hello World!"
   - callbacks should match those in callback section
   - descriptions should match those from other samples of the same feature
   - language specific reference to error catching method
 - Running the Application should have language specific command
 - Environmental Variables should match template order and only include those used in the sample
   - Auth is OAuth only: `BW_CLIENT_ID` and `BW_CLIENT_SECRET`, never `BW_USERNAME`/`BW_PASSWORD`
 - Callback URL Link should link to product specific webhooks page
   - callback paths should be `/callbacks/{direction}/{service}`, with events as sub-paths (e.g. `/callbacks/outbound/voice/gather`, `/callbacks/inbound/voice/recordingAvailable`)
   - callbacks should be ordered: outbound>inbound>others
 - Ngrok section shows language specific port information

## LICENSE

 - Should have MIT LICENSE
 - LICENSE should be up to date with current year

## .gitignore

 - Should contain only language specific files/folders
 - Should match other gitignores for the same language, regardless of usage

## Package Requirement File

 - Should only reference packages required by the specific sample app
 - Don't hand-pick versions. Copy the requirement file from the most recently migrated sample of the same language, since Dependabot keeps those current
 - Java: dependencies should only be `bandwidth-sdk` and `spring-boot-starter-web`. No `commons-io`, `javax.activation-api`, `spring-boot-starter-test` or `lombok`; use a `record` for model classes

## Dependabot

 - Copy `.github/dependabot.template.yml` to `.github/dependabot.yml` and fill in the placeholders
 - Only SDK major versions get their own PR, all other dependencies are grouped monthly
 - Placeholder values by language:

   | Language | `<ecosystem>` | `<directory>` | `<sdk-package>` |
   |---|---|---|---|
   | Ruby | `bundler` | `/` | `bandwidth-sdk` |
   | Node | `npm` | `/` | `bandwidth-sdk` |
   | Python | `pip` | `/` | `bandwidth-sdk` |
   | C# | `nuget` | the project folder, e.g. `/VoiceRecord` | `Bandwidth.Sdk` |
   | Java | `maven` | `/` | `com.bandwidth.sdk:bandwidth-sdk` |
   | PHP | `composer` | `/` | `bandwidth/sdk` |

## Contract Test

 - Should have `.github/workflows/test.yml` calling the language's workflow from `Bandwidth-Samples/sample-app-tooling`, with `sample` set to the sample type
 - See the `sample-app-tooling` README for the caller template and inputs

## Sample App

 - Must pass its contract test (`sample-app-tooling/contracts/<type>.yml`), which covers routes, status codes, BXML and env var handling. The rules below cover what the contract can't check
 - contains correct imports/requirements
 - environment variables should match the order in the README
 - missing environment variables, or a non-integer `LOCAL_PORT`, should exit with a message pointing to the README
 - SDK config and api instances come after imports and environmental variables, but before rest of sample app
 - Text responses should resemble sentences and end in periods.
 - Messaging:
    - Message Status Callback should print:
      - `message-sending` -> `message-sending type is only for MMS.`
      - `message-delivered` -> `Your message has been handed off to the Bandwidth's MMSC network, but has not been confirmed at the downstream carrier.`
      - `message-failed` -> `For MMS and Group Messages, you will only receive this callback if you have enabled delivery receipts on MMS.`
    - Inbound Message Callback:
      - Should print the following in order with newlines in between: callback description, To: "", From: "", Text: ""
      - Media should be saved with original media name in a `media/` folder in the project root, and `media/` should be in the `.gitignore`
    - Auto Response Callback:
      - Response Map should be:
        - stop: "STOP: OK, you'll no longer receive messages from us.",
        - quit: "QUIT: OK, you'll no longer receive messages from us.",
        - help: "Valid words are: STOP, QUIT, HELP, and INFO. Reply STOP or QUIT to opt out.",
        - info: "INFO: This is the test responder service. Reply STOP or QUIT to opt out.",
        - default: "Please respond with a valid word. Reply HELP for help."

## Language Specific Rules

   - Ruby
      - user created variables should be in snake_case
      - hashes should use symbols as keys

   - Python
      - user created variables should be in snake_case
      - 2 newlines between code blocks
      
   - C#
      - will eventually be renamed to .NET for accuracy
      - Running the Application should include: `Or open the project in Microsoft Visual Studio and run using the button in the toolbar.`