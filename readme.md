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
