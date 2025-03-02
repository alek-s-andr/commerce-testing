---
title: Interactive pause | Commerce Testing
description: Learn how to use the pause execution at any point and enter an interactive shell with the Functional Testing Framework for Adobe Commerce and Magento Open Source projects.
---

# Interactive pause

It can be difficut to write a successful test on the first attempt. You will need to try different commands, with different arguments, before you find the correct path.

Since Codeception 3.0, you can pause execution in any point and enter an interactive shell where you will be able to try commands in action.

Now this `Interactive Pause` feature is available in MFTF. All you need to do is to set `ENABLE_PAUSE` to `true` in `.env`.

Check [pause on codeception.com][] for documentation and a video to see `Interactive Pause` in action.

In short, when a test gets to `$I->pause()` step, it stops and shows a console where you can try all available commands with auto-completion, stash commands, save screenshots, etc.

## How to Configure Interactive Pause

To be able to use Interactive console you need to install `hoa/console` library by running `composer require hoa/console` command in your project. This will allow `<pause />` action to work.
The Functional Testing Framework supports `Interactive Pause` when `ENABLE_PAUSE` is set to `true` in `<project_root>/dev/tests/acceptance/.env` file.

## Functional Testing Framework run commands

```bash
vendor/bin/mftf run:group
```

```bash
vendor/bin/mftf run:test
```

```bash
vendor/bin/mftf run:manifest
```

```bash
vendor/bin/mftf run:failed
```

### Use `Interactive Pause` during test development

Here is a typical work flow for this use case:

- Set `ENABLE_PAUSE` to `true` under `.env`
- Add `<pause>` action in a test where you want to pause execution for debugging
- Run test
- Execution should pause at `<pause>` action and invoke interactive console
- Try out commands in interactive console
- Resume test execution by pressing `ENTER`

### Use `Pause` on test failure

When `ENABLE_PAUSE` is set to `true`, the Functional Testing Framework automatically generates `pause()` action in `_failed()` hook for tests and in `_failed()` function in `MagentoWebDriver`.
This allows you to use `pause` to debug test failure for a long running test. The work flow might look like:

- Set `ENABLE_PAUSE` to `true` under `.env`
- Run test
- Execution pauses and invokes interactive console right after test fails
- Examine and debug on the spot of failure

## Functional Testing Framework Codecept run command

You can also use MFTF's wrapper command to run Codeception directly and activate `Interactive Pause` by passing `--debug` option.
You do not need to set `ENABLE_PAUSE` to `true` for this command if you don't want to pause on test failure.

```bash
vendor/bin/mftf codecept:run --debug
```

<InlineAlert variant="warning" slots="text" />

The Functional Testing Framework command "--debug" option has different meaning than Codeception command "--debug" mode option.

<!-- Link definitions -->

[pause on codeception.com]: https://codeception.com/docs/02-GettingStarted#Interactive-Pause
