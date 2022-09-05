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