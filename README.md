# semantic-release-weapp

[![npm](https://img.shields.io/npm/v/semantic-release-weapp.svg)](https://www.npmjs.com/package/semantic-release-weapp)
---

> Post feishu(飞书) notifications to a webhook on success or failure of a semantic-release job

| Step               | Description                                                                                            |
| ------------------ | ------------------------------------------------------------------------------------------------------ |
| `verifyConditions` | Verify the `FEISHU_WEBHOOK_URL` environment variable is set.                                           |
| `success`          | Send a formatted message to the feishu webhook provided with information about the most recent release |
| `fail`             | Send a formatted message to the feishu webhook if the release fails                                    |

## Installation

```sh
yarn add --dev semantic-release-weapp
```

## Usage

Add the following to your `release.config.js`

```js
  "plugins": [
    // ...
   ["semantic-release-weapp", {
       // These are the available platforms that the package can be downloaded from
       "platforms": ["brew", "npm", "docker"]
   }]
  ],
```

Ensure you have a webhook url in your `process.env` under the name `FEISHU_WEBHOOK_URL`. The hook is
expected to contain `https://open.feishu.cn/open-apis/bot/v2/hook/` in the URL. Without this, your release will fail
because the plugin won't know where to post to.

## Options

| Property           | Type       | Default                       | Example                              | Description                                                                                                                |
| ------------------ | ---------- | ----------------------------- | ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| `platforms`        | `String[]` | `undefined`                   | `"platforms": ["brew", "npm"]`       | Available platforms that the package can be downloaded from. Can be anything. [Supported emoji](src/get-platform-emoji.js) |
| `skipCommit`       | `String`   | `undefined`                   | `"skipCommit": "^fix\\(deps\\):"`    | Skips notifying when `regex` matches at least one commit in the release                                                    |
| `semverFilter`     | `String[]` | `["major", "minor", "patch"]` | `"semverFilter": ["major", "minor"]` | Skips releases that do not match one of the configured types                                                               |
| `fullReleaseNotes` | `Boolean`  | `true`                        | `"fullReleaseNotes": false`          | Provides the full release notes in feishu instead of a link to the release notes                                           |
| `failureMessage`   | `Boolean`  | `false`                       | `"failureMessage": true`             | Sends message when the release failed                                                                                      |
