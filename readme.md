# Component-driven Avatar

Hey, I'm [chan](https://chan.dev/twitter) 👋

This repo is setup for a stream with [Nick Taylor](https://twitter.com/nickytonline), on 2022-09-06, at https://www.twitch.tv/nickytonline/.

The goal of this stream is to build up a basic avatar component (using CSS and React) in Storybook and Chromatic.

This doc provides a decent amount of guidance for every step of the process.

## `npx storybook repro`

`npx storybook repro` is designed for setting up reproductions.

I like it because it's a great way to start a single component with Storybook.

The CLI will ask you which `view-layer` and `builder` you'd like to use.

*For this example, select `React` and `webpack`*

## Understand Storybook Scripts

Open `package.json` or run `yarn run` to see the available Storybook scripts

### `yarn storybook`

This script runs the Storybook server at `localhost:6006`.
It's used for regular development and will — in most cases — update with code changes.
### `yarn build-storybook`

This script compiles Storybook into static assets for online hosting.

A compiled Storybook can be hosted anywhere (Netlify, Vercel, AWS, etc.). But Chromatic comes with a few nice features. The most noteable upgrade of using Chromatic's free hosting is the ability to Embed stories.

Run `yarn storybook` to see the Storybook running with the standard set of generated components in the `/stories` directory.

## Set up Chromatic

Reference: [Setup and publish Storybook](https://www.chromatic.com/docs/setup)

[Personal story]:
As a frontend developer, I like to dial in experiences and add new features. Figuring out deployment and integration is a bit of a slog.

So, I do it all up front. And I get to validate that CI worked as I naturally do the part that I like.

That's what we'll do today.

### 1. Create an account at [chromatic.com](https://www.chromatic.com/start)

You can sign up with whatever method you like.

My preference is to SSO with whichever git provider I'm using.
For me that's GitHub.

It just saves a few steps as you'll need to connect your git provider anyway.

### 2. Push project to GitHub

### 3. Add project in Chromatic

### 4. Publish Storybook to Chromatic (locally)

Add `chromatic` as dev dependency:

`yarn add --dev chromatic`

Publish to chromatic using global `chromatic` script and provided project token:
`npx chromatic --project-token=85b6db193be3`

This script will build storybook, using the default `yarn build-storybook command` (configurable via CLI, for existing projects).

Once the `chromatic` successfully builds and uploads to Chromatic (using your project-token), the page will automatically refresh with details about your first Chromatic build.

Decide how to send builds to Chromatic.

The command line tool will ask if you want to add a `chromatic` script to `package.json` scripts for future use.
Go with this for now and we can make it more secure before committing it (as the warning suggests).

```
Your project token was added to the script via the --project-token flag.
If you're running Chromatic via continuous integration, we recommend setting
the CHROMATIC_PROJECT_TOKEN environment variable in your CI environment.
You can then remove the --project-token from your package.json script.
```

Catch UI changes, by sending a second build.

Chromatic will require that you send a second build for comparison. This doesn't have to be committed into code. You can make a local changes here and send it as a build using the global chromatic script.

To get thru this quickly, change the text on one of these buttons to get a diff.

```js
export const Small = Template.bind({});
Small.args = {
  size: 'small',
  label: 'Small',
};
```

Run `yarn chromatic` (the new script that was added after initial run)

See that Chromatic spotted your changes.

## Explore the UI with Nick

[Open space to explore the partso of the Chromatic UI]

## Understand builds

One of the hardest parts for me to understand about CI is that *builds are not branches*.

This is confusing to a lot of folks getting started with CI.
So Chromatic has a doc explaining exactly how baselines and diffs are determined.

https://www.chromatic.com/docs/branching-and-baselines

What we need to understand now is that `Build 1` is our is our baseline. Every build will compare to that.

What we're doing in Chromatic is determining if the artifact of that build should update the baseline.

In this case, we made arbitrary changes. So we're going to reject them.

Let's change our `Small` component back.

Publish a new build that matches the initial to see a build with another green bubble.

## Possible next steps
- [Automate Chromatic with GitHub Actions](https://www.chromatic.com/docs/github-actions)
  - This will let us see changes in GitHub
  - [PRs page](https://www.chromatic.com/pullrequests?appId=63160b911cb40b4b2177896e)
- Add basic Avatar
  - This results in a new story but no changes
- Delete `/stories` directory
  - This will result in a number of changes
- Interpret component interfaces with [Storybook docs](https://storybook.js.org/addons/@storybook/addon-docs) and (in our case) `prop-types`
- interaction-testing with [Play functions](https://storybook.js.org/docs/react/writing-stories/play-function)
- Storybook features
  - Viewport, Measure, Outline
  - addon-accessibility   
- Chromatic features
  - Embed (works well in Notion)
  - Enable various browsers (https://www.chromatic.com/docs/browsers) — not available in free plan
  - Add [Slack intergration](https://www.chromatic.com/docs/integrations) or [WebHooks](https://www.chromatic.com/docs/integrations)
  - [UI Review](https://www.chromatic.com/pullrequests?appId=63160b911cb40b4b2177896e) and how it difers from UI Test
