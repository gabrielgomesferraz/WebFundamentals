project_path: /web/tools/_project.yaml
book_path: /web/tools/_book.yaml
description: Learn how to log messages to the Console.

{# wf_updated_on: 2019-04-19 #}
{# wf_published_on: 2019-04-19 #}
{# wf_blink_components: Platform>DevTools #}

[expand]: /web/tools/chrome-devtools/images/shared/expand.png

# Get Started With Logging Messages In The Console {: .page-title }

{% include "web/_shared/contributors/kaycebasques.html" %}

This interactive tutorial shows you how to log and filter messages in the [Chrome DevTools](/web/tools/chrome-devtools/) Console.

<figure>
  <img src="/web/tools/chrome-devtools/console/images/logexample.png"
       alt="Messages in the Console.">
  <figcaption>
    <b>Figure X</b>. Messages in the Console.
  </figcaption>
</figure>

This tutorial is intended to be completed in order. It assumes that you understand the fundamentals of web
development, such as how to use JavaScript to add interactivity to a page.

## Set up the demo and DevTools {: #setup }

This tutorial is designed so that you can open up the demo and try all the features yourself.
This type of hands-on experience makes it more likely that you'll remember the features when you
really need them.

1. Open the demo.
1. Optional: Move the demo to a separate window.
1. Focus the demo and then press <kbd>Control</kbd>+<kbd>Shift</kbd>+<kdb>J</kbd> or
   <kbd>Control</kbd>+<kbd>Shift</kbd>+<kdb>J</kbd> (Mac) to open DevTools. By default DevTools opens to the
   right of the demo.

[placement]: /web/tools/chrome-devtools/ui#placement

1. Optional: [Dock DevTools to the bottom of the window or undock it into a separate window][placement].

## View messages logged from JavaScript {: #javascript }

Most messages that you see in the Console come from the web developers who wrote the page's JavaScript.
The goal of this section is to introduce you to the different message types that you're likely to see in the Console, and
explain how you can log each message type yourself from your own JavaScript.

1. Click the **Log Info** button in the demo. `Hello, Console!` gets logged to the Console.

1. Next to the `Hello, Console!` message in the Console click **log.js:2**. The Sources panel opens and highlights the
   line of code that caused the message to get logged to the Console. The message was logged when the page's JavaScript
   called `console.log('Hello, Console!')`.

1. Navigate back to the Console using any of the following workflows:

     * Click the **Console** tab.
     * Press <kbd>Control</kbd>+<kbd>[</kbd> or <kbd>Command</kbd>+<kbd>[</kbd> (Mac) until the Console panel is in focus.
     * [Open the Command Menu](/web/tools/chrome-devtools/command-menu), start typing `Console`, select the
       **Show Console Panel** command, and then press <kbd>Enter</kbd>.

1. Click the **Log Warning** button in the demo. `Abandon Hope All Ye Who Enter` gets logged to the Console.
   Messages formatted like this are warnings.

1. Optional: Click **log.js:12** to view the code that caused the message to get formatted like this, and then navigate
   back to Console when you're finished. Do this whenever you want to see the code that caused a message to get
   logged a certain way.

[trace]: https://en.wikipedia.org/wiki/Stack_trace

1. Click the **Expand** ![Expand][expand]{: .inline-icon } icon in front of `Abandon Hope All Ye Who Enter`. DevTools
   shows the [stack trace][trace]{: .external } leading up to the call.

     The stack trace is telling you that a function named `logWarning`, which in turn called a
     function named `quoteDante`. In other words, the call that happened first is at the bottom of the
     stack trace. You can manually log stack traces at any time by calling `console.trace()`.

1. Click **Log Error**. The following error message gets logged: `I'm sorry, Dave. I'm afraid I can't do that.`

1. Click **Log Table**. A table about famous artists gets logged to the Console.
   Note how the `birthday` column is only populated for one row. Check the code to figure out why that is.

1. Click **Log Group**. 4 messages are grouped under the `Adolescent Irradiated Espionage Tortoises` label.

1. Click **Log Custom**. A message with a red border and blue background gets logged to the Console.

## View messages logged by the browser {: #browser }

The browser logs messages to the Console, too. This usually happens when there's a problem with the page.

1. Click **Cause 404**. The browser logs a `404` network error because the page's JavaScript tried to
   fetch a file that doesn't exist.

1. Click **Cause Error**. The browser logs an uncaught `TypeError` because the JavaScript is trying to update
   a DOM node that doesn't exist.

1. Click the **Log Levels** dropdown and enable the **Verbose** option if it's disabled. You'll learn more
   about filtering in the next section. You need to do this to make sure that the next message you log
   is visible.

1. Click **Cause Violation**. The page becomes unresponsive for a few seconds and then the browser logs
   the message `[Violation] 'click' handler took 2999ms` to the Console. The exact duration may vary.

## Filter messages {: #filter }

On some pages you'll see the Console get flooded with messages. DevTools provides
many different ways to filter out messages that aren't relevant to the task at hand.

### Filter by log level {: #level }

Each `console` method is assigned a severity level: `Verbose`, `Info`, `Warning`, or `Error`. For example,
`console.log()` is an `Info`-level message, whereas `console.error()` is an `Error`-level message.

1. Click the **Log Levels** dropdown and disable **Errors**. A level is disabled when there is no longer a
   checkmark next to it. The `Error`-level messages disappear.
1. Click the **Log Levels** dropdown again and re-enable **Errors**. The `Error`-level messages reappear.

### Filter by text {: #text }

When you want to only view messages that include an exact string, type that string into the **Filter** text box.

1. Type `Dave` into the **Filter** text box. All messages that do not include the string `Dave` are hidden.
   You might also see the `Adolescent Irradiated Espionage Tortoises` label. That's a bug.
1. Delete `Dave` from the **Filter** text box. All the messages reappear.

### Filter by regular expression {: #regex }

[regex]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions

When you want to show all messages that include a pattern of text, rather than a specific string, use a
[regular expression][regex]{: .external }.

1. Type `/^[AH]/` into the **Filter** text box. Type this pattern into [RegExr](https://regexr.com) for an
   explanation of what it's doing.
1. Delete `/^[AH]/` from the **Filter** text box. All messages are visible again.

### Filter by message source {: #source }

When you want to only view the messages that came from a certain URL, use the **Sidebar**.

[sidebar]: /web/tools/chrome-devtools/images/shared/show-console-sidebar.png

1. Click **Show Console Sidebar** ![Show Console Sidebar][sidebar]{: .inline-icon }.
1. Click the **Expand** ![Expand][expand]{: .inline-icon } icon next to **12 Messages**. The
   **Sidebar** shows a list of URLs that caused messages to be logged. For example, `log.js`
   caused 11 messages.

### Filter by user messages {: #user }

Earlier, when you clicked **Log Info**, a script called `console.log('Hello, Console!')` in order to log
the message to the Console. Messages logged from JavaScript like this are called *user messages*. In contrast,
when you clicked **Cause 404**, the browser logged an `Error`-level message stating that the requested
resource could not be found. Messages like that are considered *browser messages*. You can use the **Sidebar**
to filter out browser messages and only show user messages.

1. Click **9 User Messages**. The browser messages are hidden.
1. Click **12 Messages** to show all messages again.

## Console Drawer {: #drawer }

What if you're editing styles, but you need to quickly check the Console log for something? Use the Drawer.

1. Click the **Elements** tab.
1. Press <kbd>Escape</kbd>. The Console tab of the **Drawer** opens. It has all of the features
   of the Console panel that you've been using throughout this tutorial.

## Next steps {: #next }

Congratulations, you have completed the tutorial. Click **Dispense Trophy** to receive your
trophy.

{% framebox width="auto" height="auto" enable_widgets="true" %}
<style>
  .note::before {
    content: "";
  }
</style>
<script>
  var label = '/web/tools/chrome-devtools/console/log';
  var feedback = {
    "category": "Completion",
    "choices": [
      {
        "button": {
          "text": "Dispense Trophy"
        },
        "response": "🏆",
        "analytics": {
          "label": label
        }
      }
    ]
  };
</script>
{% include "web/_shared/multichoice.html" %}
{% endframebox %}

* See [Console Reference](/web/tools/chrome-devtools/console/reference) to explore more features and
  workflows related to the Console UI.
* See [Console API Reference](/web/tools/chrome-devtools/console/api) to learn more about all of the
  `console` methods that were demonstrated in [View messages logged from JavaScript](#javascript).

## Feedback {: #feedback }

{% include "web/_shared/helpful.html" %}
