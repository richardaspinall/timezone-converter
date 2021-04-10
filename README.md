> **Date started**: (Sep 2019)

> **Date ended**:

## Description

Time Zone converter is a Chrome extension that converts time to a time zone of the user's choice. Specifically it automatically converts any times of: YYYY-MM-DD HH:MM:SS [Time Zone Abbreviation] format to the user's default. It also has a manual converter if the page hasn't automatically converted (can also convert Unix time).

The target element on a page is a table data cell (`'td'`) and format of: `YYYY-MM-DD HH:MM:SS` or Unix Time, however this should be somewhat easily extended for other formats and target elements on specific pages. See [Production](##production) for more information

## Goals

## Requirements

- Node
- NPM

## Install

1. Clone repo
2. Run `npm run install`

## Development

Run `npm run build`

## Production

1. Run `npm run build-production`

2. Production usage is through a Chrome extension. It will run / show on any page that you have configured against `matches` under `content_scripts`in the `dist/manifest.json` file. The current `manifest` defaults to all `https://` websites (but won't convert anything unless there are table cells with the specific format as per: [insert link ] ).

See here for matching: https://developer.chrome.com/docs/extensions/mv2/match_patterns/

3. For local testing, the `dist` folder can be added into your extensions in Chrome [chrome://extensions/](chrome://extensions/). You will need to turn on `developer mode` before you can add an extension this way, see [Developer Mode](https://developer.chrome.com/docs/extensions/mv3/faq/#:~:text=You%20can%20start%20by%20turning,right%2Dhand%20corner%20is%20checked)

4. After `developer mode` has been turned on, simply drag the `dist` folder or load unpacked here: [chrome://extensions/](chrome://extensions/)

5. Date times on websites you are probably wanting to convert might not be formatted or within table elements, you can extend `libs/conversion/getUnixTimeFromString.js` with new regex checks (adding to`libs/timeZoneRegex.js` and `libs/conversion/momentInterface.js`) ensuring you return a Unix Time. Then change `ELEMENT_TO_CONVERT` in `src/convertPage.js` to the element that your date times are within.

**Note:** the page default (that the page converter converts from automatically) is set to "America/Los_Angeles" which can be changed via `PAGE_DEFAULT_TIMEZONE` in `src/main.js`.
**Note:** the elements inner html are converted and formatted to: `YYYY-MM-DD HH:MM:SS [Time Zone Abbreviation]` / `2021-01-01 09:00:00 PDT`

## Usage

1. Open `tests/mock-site/index-dev.html` in a Chrome browser
2. Click the clock icon that should appear up the top right
3. Change the page Time Zone and click Convert
4. Manually enter a Date Time or Unix Time with from - to Time Zones via text input or through the picker, and click Convert

## Production usage

1. Same as ## Usage above
2. There should also be the clock icon in your Chrome extensions tray (you may need to pin it), this can be used to manually convert whereever you are in Chrome regardless of the `manifest.json`

---

## Resources

- Link to resource